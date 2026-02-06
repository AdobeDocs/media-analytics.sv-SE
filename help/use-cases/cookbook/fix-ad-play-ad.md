---
title: Lösa huvudspel som visas mellan annonser
description: Lär dig hur du hanterar oväntade huvud:uppspelningssamtal mellan annonser.
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Hantera luckor mellan annonser{#resolving-main-play-appearing-between-ads}

## PROBLEM

I vissa annonsspårningsscenarier kan `main:play` anrop inträffa oväntat mellan slutet av en annons och början av nästa annons. Om fördröjningen mellan det fullständiga annonsanropet och nästa annonsöppningsanrop är större än 250 millisekunder återgår Media SDK till att skicka `main:play` samtal. Om det här återfallet till `main:play` inträffar under en annonsbrytning före rullning kan innehållets startmått anges tidigt.

En lucka mellan annonser som beskrivs ovan tolkas av Media SDK som huvudinnehåll eftersom det inte finns någon överlappning med något annonsinnehåll. Media SDK har ingen annonsinformation och spelaren är i uppspelningsläge. Om det inte finns någon annonsinformation, och spelarläget spelas upp, tilldelar Media SDK som standard längden på mellanrummet mot huvudinnehållet. Det går inte att kreditera uppspelningens varaktighet mot annonsen som är null.

## IDENTIFIERING

När du använder Adobe Debug eller en nätverkspaketsniffer som Charles, om du ser följande pulsslagsanrop i den här ordningen under en annonsbrytning före rullning:

* Sessionsstart: `s:event:type=start` &amp; `s:asset:type=main`
* Annonsstart: `s:event:type=start` &amp; `s:asset:type=ad`
* Annonsuppspelning: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Huvudinnehåll spelas: `s:event:type=play` &amp; `s:asset:type=main` **(oväntat)**

* Annonsstart: `s:event:type=start` &amp; `s:asset:type=ad`
* Annonsuppspelning: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Huvudinnehåll spelas: `s:event:type=play` &amp; `s:asset:type=main` **(förväntades)**

## UPPLÖSNING

***Fördröjning som utlöser anropet för att slutföra annonsering.***

Hantera gapet inifrån spelaren genom att anropa `trackEvent:AdComplete` sent för den första annonsen, omedelbart följt av `trackEvent:AdStart` för den andra annonsen. Appen bör vänta med att anropa `AdComplete`-händelsen när den första annonsen är klar. Se till att du ringer `trackEvent:AdComplete` för den sista annonsen i annonsbrytningen. Om spelaren kan identifiera att den aktuella annonsresursen är den sista i annonsbrytningen ska du omedelbart ringa `trackEvent:AdComplete`. Upplösningen resulterar i att mindre än en sekund extra annonstid tillskrivs föregående annonsenhet.

**Vid annonsradbrytning, inklusive pre-roll:**

* Skapa objektinstansen `adBreak` för annonsbrytningen, till exempel `adBreakObject`.

* Ring `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**För varje annonsresurs som startar:**

* **Ring`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >Ring bara detta om föregående annons inte är fullständig. Överväg ett booleskt värde om du vill behålla tillståndet `isinAd` för föregående annons.

* Skapa annonsobjektsinstansen för annonsresursen, till exempel `adObject`.
* Fyll i annonsmetadata, `adCustomMetadata`.
* Ring `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Anropa `trackPlay()` om det här är den första annonsen i en annonsbrytning före registrering.

**För varje annonsresurs som har slutförts:**

* **Ring inte**

  >[!NOTE]
  >
  >Om programmet vet att det är den sista annonsen i annonsbrytningen ringer du `trackEvent:AdComplete` här och hoppar över inställningen `trackEvent:AdComplete` i `trackEvent:AdBreakComplete`

**I annonshoppa:**

* Ring `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**En annonsbrytning slutförd:**

* **Ring`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >Om det här steget redan har utförts ovan som en del av det senaste `trackEvent:AdComplete`-anropet kan det här hoppas över.

* Ring `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

---
title: Lösa huvudspel som visas mellan annonser
description: "Lär dig hur du hanterar oväntade huvud:uppspelningssamtal mellan annonser."
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Hantera luckor mellan annonser{#resolving-main-play-appearing-between-ads}

## PROBLEM

I vissa annonsspårningsscenarier kan du stöta på `main:play` anrop som inträffar oväntat mellan slutet av en annons och början av nästa annons. Om fördröjningen mellan det fullständiga annonsanropet och nästa annonsöppningsanrop är längre än 250 millisekunder återgår Media SDK till att skicka `main:play` samtal. Om detta alternativ `main:play` när en annonsbrytning pågår kan innehållets startmått anges tidigt.

Ett mellanrum mellan annonser som beskrivs ovan tolkas av Media SDK som huvudinnehåll, eftersom det inte finns någon överlappning där med något annonsinnehåll. Media SDK har ingen annonsinformation och spelaren är i uppspelningsläge. Om det inte finns någon annonsinformation, och spelarläget spelas upp, kommer Media SDK som standard att identifiera längden på mellanrummet mot huvudinnehållet. Det går inte att kreditera uppspelningens varaktighet mot annonsen som är null.

## IDENTIFIERING

När du använder Adobe Debug eller en nätverkspaketsniffer som Charles, om du ser följande pulsslagsanrop i den här ordningen under en annonsbrytning före rullning:

* Sessionsstart: `s:event:type=start` &amp; `s:asset:type=main`
* Annonsstart: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Huvudinnehåll spelas upp: `s:event:type=play` &amp; `s:asset:type=main` **(oväntat)**

* Annonsstart: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Huvudinnehåll spelas upp: `s:event:type=play` &amp; `s:asset:type=main` **(förväntades)**

## UPPLÖSNING

***Fördröjning som utlöser anropet till Ad Complete.***

Hantera mellanrummet inifrån spelaren genom att ringa `trackEvent:AdComplete` sent till första annansen, följt av `trackEvent:AdStart` för den andra annonsen. Appen bör vänta med att anropa `AdComplete` -händelsen när den första annonsen är klar. Se till att du ringer `trackEvent:AdComplete` för den sista annonsen i annonsbrytningen. Om spelaren kan identifiera att den aktuella annonsresursen är den sista i annonsbrytningen ringer du `trackEvent:AdComplete` omedelbart. Upplösningen resulterar i att mindre än en sekund extra annonstid tillskrivs den föregående annonsenheten.

**Vid start av annonsbrytning, inklusive pre-roll:**

* Skapa `adBreak` objektinstans för annonsbrytningen, till exempel `adBreakObject`.

* Utlysning `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**För varje annonsresurs:**

* **Utlysning`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Ring bara detta om föregående annons inte är fullständig. Överväg ett booleskt värde om du vill behålla ett`isinAd`&quot; för föregående annons.

* Skapa ad-objektinstansen för annonsresursen: till exempel `adObject`.
* Fyll i annonsens metadata, `adCustomMetadata`.
* Utlysning `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Utlysning `trackPlay()` om detta är den första annonsen i en annonsbrytning före rullning.

**För varje annonsmaterial:**

* **Ring inte**

   >[!NOTE]
   >
   >Om programmet vet att det är den sista annonsen i annonsbrytningen ringer du `trackEvent:AdComplete` här och hoppa över inställning `trackEvent:AdComplete` i `trackEvent:AdBreakComplete`

**On ad skip:**

* Utlysning `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Vid annonsbrytning:**

* **Utlysning`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Om det här steget redan utförs ovan som en del av det sista `trackEvent:AdComplete` så kan detta hoppas över.

* Utlysning `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

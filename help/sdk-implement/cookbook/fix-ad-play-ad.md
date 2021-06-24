---
title: Lösa huvudspel som visas mellan annonser
description: '"Lär dig hur du hanterar oväntade huvud:uppspelningssamtal mellan annonser."'
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# Lösa main:play mellan annonser{#resolving-main-play-appearing-between-ads}

## PROBLEM

I vissa annonsspårningsscenarier kan du stöta på `main:play` samtal som inträffar oväntat mellan slutet av en annons och början av nästa annons. Om fördröjningen mellan det fullständiga annonsanropet och nästa annonsöppningsanrop är större än 250 millisekunder återgår Media SDK till att skicka `main:play`-anrop. Om det här återfallet till `main:play` inträffar under en annonsbrytning före rullning kan innehållets startmått ställas in tidigt.

Ett mellanrum mellan annonser som beskrivs ovan tolkas av Media SDK som huvudinnehåll, eftersom det inte finns någon överlappning där med något annonsinnehåll. Media SDK har ingen annonsinformation och spelaren är i uppspelningsläge. Om det inte finns någon annonsinformation, och spelarläget spelas upp, kommer Media SDK som standard att identifiera längden på mellanrummet mot huvudinnehållet. Det går inte att kreditera uppspelningens varaktighet mot annonsen som är null.

## IDENTIFIERING

När du använder Adobe Debug eller en nätverkspaketsniffer som Charles, om du ser följande pulsslagsanrop i den här ordningen under en annonsbrytning före rullning:

* Sessionsstart: `s:event:type=start` &amp; `s:asset:type=main`
* Annonsstart: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Huvudinnehåll spelas upp: `s:event:type=play` &amp; `s:asset:type=main` **(oväntat)**

* Annonsstart: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` &amp; `s:asset:type=ad`
* Huvudinnehåll spelas upp: `s:event:type=play` &amp; `s:asset:type=main` **(förväntades)**

## UPPLÖSNING

***Fördröjning som utlöser anropet till Ad Complete.***

Hantera gapet inifrån spelaren genom att ringa `trackEvent:AdComplete` sent för den första annonsen, omedelbart följt av `trackEvent:AdStart` för den andra annonsen. Appen bör vänta med att anropa händelsen `AdComplete` när den första annonsen är klar. Se till att du ringer `trackEvent:AdComplete` för den sista annonsen i annonsuppdelningen. Om spelaren kan identifiera att den aktuella annonsresursen är den sista i annonsbrytningen ska du omedelbart ringa `trackEvent:AdComplete`. Upplösningen resulterar i att mindre än en sekund extra annonstid tillskrivs den föregående annonsenheten.

**Vid start av annonsbrytning, inklusive pre-roll:**

* Skapa objektinstansen `adBreak` för annonsbrytningen; till exempel `adBreakObject`.

* Ring `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**För varje annonsresurs:**

* **Utlysning`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Ring bara detta om föregående annons inte är fullständig. Överväg ett booleskt värde om du vill behålla läget `isinAd` för föregående annons.

* Skapa ad-objektinstansen för annonsresursen: till exempel `adObject`.
* Fyll i annonsmetadata, `adCustomMetadata`.
* Ring `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Ring `trackPlay()` om detta är den första annonsen i en annonsbrytning före registrering.

**För varje annonsmaterial:**

* **Ring inte**

   >[!NOTE]
   >
   >Om programmet vet att det är den sista annonsen i annonsbrytningen ringer du `trackEvent:AdComplete` här och hoppar över inställningen `trackEvent:AdComplete` i `trackEvent:AdBreakComplete`

**On ad skip:**

* Ring `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Vid annonsbrytning:**

* **Utlysning`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Om det här steget redan utförs ovan som en del av det sista `trackEvent:AdComplete`-anropet kan det här hoppas över.

* Ring `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

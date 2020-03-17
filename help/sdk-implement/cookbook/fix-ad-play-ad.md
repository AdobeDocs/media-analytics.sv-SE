---
title: Lösa huvudspel som visas mellan annonser
description: Så här hanterar du oväntade huvud:uppspelningsanrop mellan annonser.
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Lösa huvudspel:uppspelning mellan annonser{#resolving-main-play-appearing-between-ads}

## PROBLEM

I vissa annonsspårningsscenarier kan du råka ut för `main:play` samtal som inträffar oväntat mellan slutet av en annons och början av nästa annons. Om fördröjningen mellan det fullständiga annonsanropet och nästa annonsöppningsanrop är längre än 250 millisekunder återgår Media SDK till att skicka `main:play` samtal. Om detta fel inträffar `main:play` under en annonsbrytning före rullning kan innehållets startmått ställas in tidigt.

Ett mellanrum mellan annonser som beskrivs ovan tolkas av Media SDK som huvudinnehåll, eftersom det inte finns någon överlappning där med något annonsinnehåll. Media SDK har ingen annonsinformation och spelaren är i uppspelningsläge. Om det inte finns någon annonsinformation, och spelarläget spelas upp, kommer Media SDK som standard att identifiera längden på mellanrummet mot huvudinnehållet. Det går inte att kreditera uppspelningens varaktighet mot annonsen som är null.

## IDENTIFIERING

När du använder Adobe Debug eller en nätverkspaketsniffer som Charles, om du ser följande pulsslagsanrop i den här ordningen under en annonsbrytning före rullning:

* Sessionsstart: `s:event:type=start` och `s:asset:type=main`
* Annonsstart: `s:event:type=start` och `s:asset:type=ad`
* Ad Play: `s:event:type=play` och `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` och `s:asset:type=ad`
* Huvudinnehåll spelas upp: `s:event:type=play` &amp; `s:asset:type=main`**(oväntat)**

* Annonsstart: `s:event:type=start` och `s:asset:type=ad`
* Ad Play: `s:event:type=play` och `s:asset:type=ad`
* Ad Complete: `s:event:type=complete` och `s:asset:type=ad`
* Huvudinnehåll spelas upp: `s:event:type=play` &amp; `s:asset:type=main`**(förväntas)**

## UPPLÖSNING

***Fördröjning som utlöser anropet till Ad Complete.***

Hantera gapet inifrån spelaren genom att ringa `trackEvent:AdComplete` för sent till den första annonsen, omedelbart följt av `trackEvent:AdStart` den andra annonsen. Appen bör vänta med att anropa `AdComplete` händelsen när den första annonsen är klar. Var noga med att ringa `trackEvent:AdComplete` den sista annonsen i annonsbrytningen. Om spelaren kan identifiera att den aktuella annonsresursen är den sista i annonsbrytningen ska du ringa `trackEvent:AdComplete` omedelbart. Upplösningen resulterar i att mindre än en sekund extra annonstid tillskrivs den föregående annonsenheten.

**Vid start av annonsbrytning, inklusive pre-roll:**

* Skapa `adBreak` objektinstansen för annonsbrytningen, till exempel `adBreakObject`.

* Ring `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**För varje annonsresurs:**

* **Utlysning`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Ring bara detta om föregående annons inte är fullständig. Överväg ett booleskt värde om du vill behålla läget&quot;`isinAd`&quot; för föregående annons.

* Skapa ad-objektinstansen för annonsresursen: till exempel `adObject`.
* Fyll i annonsmetadata `adCustomMetadata`.
* Ring `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Ring `trackPlay()` om det här är den första annonsen i en annonsrast före rullning.

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
   >Om det här steget redan utförs ovan som en del av det senaste `trackEvent:AdComplete` samtalet kan det hoppas över.

* Ring `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.


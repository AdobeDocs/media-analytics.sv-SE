---
title: Beräknade värden
description: Läs mer om beräknade mätvärden och mätformler för Adobe Streaming Media.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 5%

---

# Beräknade värden{#calculated-metrics}

>[!NOTE]
>
>Dessa beräknade värden infördes den 13 mars 2018.

| Mått | Beskrivning | Formel |
|---|---|---|
| Medel Ads per Media Stream | Komma igång med annonser per media | `Ad Starts / Media Starts` |
| Medel Kapitel per medieström | Kapitelstart per media börjar | `Chapter Start / Media Starts` |
| Medel Medietid tillagd | Total tid per mediestart (HH:MM:SS) | `Media Time Spent / Media Starts` |
| Medel Innehållstid | Innehållstid som använts per innehållsuppstart (HH:MM:SS) | `Content Time Spent / Content Start` |
| Medel Annonstid | Annonstid per annonsstart (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| Medel Kapiteltid spenderad | Kapiteltid som spenderats per kapitel startar (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| Slutförandefrekvens för media | Frekvens för slutfört innehåll kontra initierat media (%) | `Content Completes/ Media Starts` |
| Slutförandefrekvens för innehåll | Frekvens för slutfört innehåll jämfört med innehåll som börjar (%) | `Content Completes / Content Starts` |
| Annonsslutförandefrekvens | Antal slutförda annonser jämfört med annonsstart (%) | `Ad Completes / Ad Starts` |
| Slutförandefrekvens för kapitel | Frekvens för slutförda kapitel jämfört med början av kapitel (%) | `Chapter Completes / Chapter Starts` |
| Släpp före startfrekvens | Frekvens för släppningar innan start kontra mediestart startar (%) | `Drops before Starts / Media Starts` |
| Varaktighet för innehållspaus | Frekvens för total paus-varaktighet jämfört med innehållstid (%) | `Total Pause Duration / Content Time Spent` |
| Varaktighet för innehållsbuffert | Frekvens för total buffertvaraktighet kontra använd innehållstid (%) | `Total Buffer Duration / Content Time Spent` |
| Startfrekvens för innehåll | Frekvens för tid att starta jämfört med innehållstid som använts (%) | `Time to Start / Content Time Spent` |
| Utnyttjad annonstid | Utnyttjad annonstid kontra använd innehållstid (%) | `Ad Time Spent / Content Time Spent` |

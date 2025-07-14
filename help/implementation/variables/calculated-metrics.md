---
title: Beräknade mätvärden
description: Lär dig mer om beräknade mätvärden och mätformler i Streaming Media Collection.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 3%

---

# Beräknade mått{#calculated-metrics}

Beräknade mätvärden för Adobe Streaming Media Collection är anpassade mätvärden som gör att ni kan få fram riktade data för direktuppspelande media, som genomsnittlig annonstid eller genomsnittliga annonser per medieström.

Mer information om Adobe Analytics beräknade mått finns i [Beräknade och avancerade beräknade (härledda) mått](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=sv-SE) i Adobe Analytics Components Guide.

>[!NOTE]
>
>Dessa beräknade värden infördes den 13 mars 2018.

| Mått | Beskrivning | Formel |
|---|---|---|
| Medel Ads per Media Stream | Komma igång med annonser per media | `Ad Starts / Media Starts` |
| Medel Kapitel per medieström | Kapitelstart per media börjar | `Chapter Start / Media Starts` |
| Medel Medietid tillagd | Total tid som tillbringats per mediematerial startar (`HH:MM:SS`) | `Media Time Spent / Media Starts` |
| Medel Innehållstid | Innehållstid per innehåll börjar (`HH:MM:SS`) | `Content Time Spent / Content Start` |
| Medel Annonstid | Lägg till tid per annonsstart (`HH:MM:SS`) | `Ad Time Spent / Ad Start` |
| Medel Kapiteltid spenderad | Kapiteltid per kapitel börjar (`HH:MM:SS`) | `Chapter Time Spent / Chapter Start` |
| Slutförandefrekvens för media | Frekvens för slutfört innehåll kontra initierat media (%) | `Content Completes/ Media Starts` |
| Slutförandefrekvens för innehåll | Frekvens för slutfört innehåll jämfört med innehåll som börjar (%) | `Content Completes / Content Starts` |
| Annonsslutförandefrekvens | Antal slutförda annonser jämfört med annonsstart (%) | `Ad Completes / Ad Starts` |
| Slutförandefrekvens för kapitel | Frekvens för slutförda kapitel jämfört med början av kapitel (%) | `Chapter Completes / Chapter Starts` |
| Antal släppningar före start | Frekvens för släppningar innan start kontra mediestart startar (%) | `Drops before Starts / Media Starts` |
| Varaktighet för innehållspaus | Frekvens för total paus-varaktighet jämfört med innehållstid (%) | `Total Pause Duration / Content Time Spent` |
| Varaktighet för innehållsbuffert | Frekvens för total buffertvaraktighet kontra använd innehållstid (%) | `Total Buffer Duration / Content Time Spent` |
| Startfrekvens för innehåll | Frekvens för tid att starta jämfört med innehållstid som använts (%) | `Time to Start / Content Time Spent` |
| Utnyttjad annonstid | Utnyttjad annonstid kontra använd innehållstid (%) | `Ad Time Spent / Content Time Spent` |

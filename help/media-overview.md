---
title: Adobe Analytics for Streaming Media - översikt
description: Använd Streaming Media Analytics för att få kraftfulla insikter om innehåll, ljud och annonser.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 9%

---

# Adobe Analytics for Streaming Media - översikt

![Banderoll](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media är ett tillägg till Adobe Analytics som innehåller kraftfulla mätverktyg för ljud, video och reklam. Med Analytics for Streaming Media får ni nästan detaljrika detaljer om varaktighet, stopp och start i realtid så att ni kan utvärdera och kombinera video- och ljudmätvärden. Med dessa insikter kan ni förstå kundernas tittande och avlyssningsvanor och öka engagemanget med personaliserade rekommendationer.

Med Adobe Analytics for Streaming Media kan ni spåra hela kundresan på hela webbplatsen och i direktuppspelningsappar. Ni kan kombinera Streaming Media-statistik med andra Adobe Analytics-funktioner, som Audience Analytics, Mobile eller Cross-Device Analytics. Mätvärdena kan enkelt integreras i Adobe Analytics Reports och andra Adobe Experience Platform-produkter. Med mediemätning kan ni kategorisera data i flera dimensioner och segment och samla in alla metadata ni behöver för att göra en fullständig och detaljerad analys. Sedan kan ni analysera data och attribuera framgångsmått för helt konsumerad media, genomsnittlig tid som tillbringats på platsen och slutförda annonser.

Ni kan mäta viktiga leveransvärden som är relaterade till Experience Quality of Experience (QoE), till exempel uteslutna bildrutor, tidsåtgången för buffring och genomsnittlig bithastighet. Och mätvärdena kan kombineras med era webbplats- eller appdata för att visualisera kundens väg och intressen, för att ge förbättrade rekommendationer och personalisera kundupplevelser med Adobe Experience Platform.

## Så här fungerar det

Spårningsdata för direktuppspelande media samlas in från en spelare med Media SDK, Media Collection API:er eller Media Extensions (med taggar). Alla detaljerade data (upp till 10 sekunder) skickas till tjänsten Media Analytics som samlar in och bearbetar data för varje enskild uppspelningssession. När uppspelningssessionen är slut skickas de beräknade spårningsdata till Adobe Analytics för lagring och rapportering. Med Adobe Customer Journey Analytics (CJA)-implementeringar kan data skickas till CJA med hjälp av ADC (Analytics Data Connector) så att kunderna kan använda CJA som rapporteringsverktyg.

<!-- ![streaming media process](./assets/streaming-process1.png) -->

<div style="text-align: center;">
<img src="./assets/streaming-process1.png" alt="Direktuppspelande medieprocess" width="75%">
</div>

## Funktioner

Fördelarna med Adobe Analytics för Streaming Media är bland annat övervakning i realtid, detaljerad analys, användbara insikter och möjligheter till intäktsgenerering.

* **Realtidsanalys**: Fatta konkreta beslut i realtid med nyckeltal som mediestart, över flera kanaler.

* **Öka engagemanget**: Engagera användarna med färre buffringshändelser och förstå var och när annonserna ska spelas upp i innehållet för att skapa en smidig och mindre påträngande upplevelse som levererar återkommande besök.

* **Holistisk bild**: Kombinera flera datapunkter för alla era innehållsdistributörer för att få en fullständig bild av alla era medieaktiviteter. Mät engagemanget och se/lyssna på alla möjliga kanaler via Federated Analytics.

* **Ökad granularitet**: Utvärdera tittarnas beteende på den mest detaljerade nivån, inklusive besökarnas tid på dygnet, samtidigt tittande eller avlyssnare per minut, och den genomsnittliga tid som innehållet förbrukades.

* **Exakt mätning**: Mät på olika enheter som används för mediekonsumtion, inklusive OTT, smarttelefon, surfplatta, dator med mera, för att övervaka användarnas engagemangsmönster och vanor.

* **Segmentering**: Använd klassificeringar på era spelare, enheter, genrer, kapitel och bildspel för att se hur de påverkar era övergripande vyer/avlyssningar och kundernas engagemang med innehåll, ljud, annonser och kombinationer.

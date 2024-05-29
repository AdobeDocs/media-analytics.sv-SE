---
title: Versionsinformation för Adobe Analytics per contenuti in streaming
description: Se versionsinformationen för Adobe Analytics.
feature: Release Notes
role: User, Admin, Data Engineer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: 9c138248ed8494aa5edb398370ac0100f8cdaa49
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 6%

---

# Versionsinformation om Adobe Analytics per contenuti in streaming (maj 2023)

**Senaste uppdatering**: 12 maj 2023

## Relaterade resurser

Mer information om nya funktioner, korrigeringar och viktig information för administratörer finns i följande resurser.

* [Versionsinformation för Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=en)
* [Versionsinformation för Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html)
* Den senaste releaseuppdateringen för [Adobe Experience Cloud](https://business.adobe.com/products/adobe-experience-cloud-products.html)

* [Adobe Analytics självstudiekurser](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en)

## *Aktuell versionsinformation*

## Nya och uppdaterade funktioner i Adobe Customer Journey Analytics för direktuppspelande media {#cja-features}

| Funktion | Beskrivning | Måldatum |
| ----------- | ---------- | ------- |
| Skicka webbdata till Adobe Experience Platform Edge Network med Web SDK | Nu kan du [använda Adobe Experience Platform Web SDK för att skicka Streaming Media-webbdata till Adobe Experience Platform Edge Network](/help/implementation/edge/edge-web-sdk.md)så att ni kan skapa mer personaliserade kampanjer och leverera mer personaliserat innehåll, vilket resulterar i mer spårningsdata att rapportera om.<p>Den här förbättringen erbjuder en enhetlig insamlingsmetod för webblösningar i alla plattformslösningar, till exempel Customer Journey Analytics, RT-CDP, AJO och händelsevidarebefordran. Tidigare var det enda sättet att skicka Streaming Media-webbdata till Edge Network att använda Media Edge API. | 29 maj 2024 |
| Skicka Roku-data till Adobe Experience Platform Edge | Nu när [installera Media Analytics med Experience Platform Edge](/help/implementation/edge/implementation-edge.md)kan du använda Adobe Experience Platform Roku SDK för att skicka direktuppspelningsmediedata till Adobe Experience Platform. | 12 april 2024 |
| Media Collection: Integrering med Experience Edge (API och Mobile SDK) | Nu kan ni använda Experience Edge API och Mobile SDK för att implementera Streaming Media, vilket gör att ni kan skapa mer personaliserade kampanjer och leverera mer personaliserat innehåll, vilket resulterar i mer spårningsdata att rapportera om.<p>Den här förbättringen ger en enhetlig insamlingsmetod för alla lösningar, som Customer Journey Analytics, RT-CDP, AJO och händelsevidarebefordran.  [Läs mer](/help/implementation/edge/implementation-edge.md) | 12 maj 2023 |
| Media Concurrent Viewer-panel | Förstå var maximal samtidighet inträffade eller var bortfall inträffade. Få värdefulla insikter om innehållets och tittarnas engagemang och hjälp med felsökning eller planering av volym och skala. [Läs mer](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=en) | 9 augusti 2022 |
| Medieuppspelningstid spenderad panel | Media Playback Time Spent ger värdefull insikt i tittarnas engagemang och gör det möjligt för medieorganisationer att få djupare och mer detaljerade insikter med användarengagemang varje minut genom avancerad tidsanalys med delningsfunktioner. Du kan se hur mycket tid du har lagt på att visa medieströmmar vid en viss tidpunkt. Du kan dela uppspelningens längd med olika granulariteter, inklusive nya 5- minuters-, 15- och 30-minutersgranulariteter. [Läs mer](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html) | 9 augusti 2022 |
| Dela anteckningar i Mobile Scorecards | Du kan visa anteckningar som har skapats i Workspace - i Mobile Scorecards. På så sätt kan ni dela kontextuella datanunkter och insikter om organisationen och kampanjer direkt i Mobile Scorecard-projekt, som kan visas i mobilappen för kontrollpaneler i Analytics. [Läs mer](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=en) | 15 juni 2022 |
| Report Builder för Customer Journey Analytics-uppdateringar | Innehåller funktioner som schemaläggning och hantering av datablockering. [Läs mer](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html) | 18 maj 2022 |
| Anteckningar i arbetsytan | Anteckningar i Workspace gör att du effektivt kan kommunicera kontextuella datanunkter och insikter till din organisation. [Läs mer](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html) | gradvis utrullning börjar 23 mars 2022 |
| Förhandsgranskningsläge för mobilstyrda projekt | Starta en förhandsgranskning av hur ditt mobilstyrkort kommer att se ut i kontrollpanelsappen för Analytics, direkt från styrkortsverktyget. I förhandsgranskningsläget kan användarna interagera med filter och diagram på samma sätt som i appen, vilket gör att de kan förhandsgranska upplevelsen innan de sparar och delar styrkortet. Användare kan också använda enhetsväljaren i förhandsgranskningsläge för att se hur styrkortet kommer att se ut på olika enheter. [Läs mer](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html#preview) | 16 februari 2022 |


## Nya och uppdaterade funktioner i Adobe Analytics per contenuti in streaming {#sm-features}

| Funktion | Beskrivning | Måldatum |
| ----------- | ---------- | ------- |
| Spårning av flera spelartillstånd | Använd API:t för Media Collection för att implementera spårning av flera spelarlägen. [Läs mer](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html) | September 2022 |
| Namnändrade XDM-fält | Namnet på XDM-fältnamnen har ändrats för att bli konsekvent:<br>* Parametrar för ljud och video<br>* Ad-parametrar<br>* Kapitelparametrar<br>* Parametrar för spelartillstånd<br>* Kvalitetsparametrar | September 2022 |
| Device Co-op-referens | Borttagen referens till Adobe Experience Cloud Device Co-op och Experience Cloud ID-tjänstens krav. | Augusti 2022 |
| Uppdaterade fältnamn och XDM-sökvägar för insamling och rapportering | Uppdaterade följande:<br>* Parametrar för ljud och video<br>* Ad-parametrar<br>* Kapitelparametrar<br>* Parametrar för spelartillstånd<br>* Kvalitetsparametrar | Augusti 2022 |
| Genomsnittlig målgrupp i minuter | Media Analytics-kunder kan använda panelen för normal målgrupp för att få en bättre förståelse för den genomsnittliga materialförbrukningen. <br>Den genomsnittliga minuten-målgruppen möjliggör jämförelser av programmering oavsett längd eller genre. Dessutom kan ni jämföra eller lägga till den digitala genomsnittliga minuten-publiken med den linjära minuten-mätningen för tv. Panelen ger större flexibilitet för att mäta den genomsnittliga publiken för anpassade tidsperioder samt när tidsklassificeringen har uppdaterats.  [Läs mer](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=en) | 16 mars 2022 |
| Medieuppspelningstid spenderad panel | Lär dig hur mediaanvändarna kan se hur mycket tid de tittar på medieuppspelningstiden är, baserat på hur lång tid de tittar på under dagen och på en vald granularitet. <br>[Media Playback Time Spent Panel (självstudiekurs)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=en) | Januari 2022 |


## *Tidigare versionsinformation*

| Funktion | Beskrivning | Måldatum eller uppdateringsdatum |
| ----------- | ---------- | -------------- |
| Medieuppspelningstid spenderad | Adobe Streaming Media Playback Time Spent ger värdefull insikt i tittarnas engagemang och gör det möjligt för medieorganisationer att få djupare och mer detaljerade insikter med användarinteraktion varje minut genom avancerad tidsanalys med delningsfunktioner. Du kan se hur mycket tid du har lagt på att visa medieströmmar vid en viss tidpunkt. Du kan dela uppspelningens längd med olika granulariteter, inklusive nya 5-, 15- och 30-minutersgranulariteter. [Läs mer …](/help/reporting/workspace/media-playback-time-spent.md) | September 2021 |
| Media Concurrent Viewer panel i Analytics Workspace | Förstå var maximal samtidighet inträffade eller var bortfall inträffade. Få värdefulla insikter om innehållets och tittarnas engagemang och hjälp med felsökning eller planering av volym och skala. [Läs mer...](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Media Concurrent Viewers Panel i Analytics Workspace (självstudiekurs)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=en#analysis-workspace) | September 2020 <br><br><br>Januari 2021 |
| Enheter och plattformar som stöds | Media Launch Extension med AEP SDK har nu stöd för följande OTT-enheter: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | Juni 2020 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->

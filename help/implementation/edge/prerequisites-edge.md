---
title: Förutsättningar för implementering av endast Adobe Analytics
description: Lär dig om förutsättningarna för att använda tillägget Streaming Media Collection med implementeringar som endast gäller för Adobe Analytics eller Edge
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Krav för Edge-implementeringar

De krav som beskrivs i det här avsnittet gäller specifikt för implementering av tillägget Adobe Streaming Media Collection med Edge-implementeringar.

1. **Slutför de allmänna kraven**<br>
Oavsett om du implementerar tillägget Streaming Media Collection för Adobe Analytics eller för Edge måste du se till att du uppfyller [allmänna krav](/help/getting-started/prereqs.md).

1. **Bekräfta att du implementerar en Adobe-lösning som är kompatibel med Edge Network och tillägget Streaming Media Collection**<br>
När du implementerar tillägget Streaming Media Collection med Edge måste du också ha en fungerande Customer Journey Analytics-, Adobe Analytics-, Adobe Journey Optimizer- eller Real-time Customer Data Platform-implementering. Mer information finns i följande dokumentationsresurser:
   * [Customer Journey Analytics guide](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=en)
   * [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
   * [Adobe Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer.html)
   * [Real-time Customer Data Platform-dokumentation](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **Hämta URL:en för mediespårningsservern**<br>
Be din Customer Journey Analytics-representant om URL:en för mediespårningsservern. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementera tillägget Streaming Media Collection med Edge Network**<br>
Följ stegen i [Implementera tillägget Streaming Media Collection med Edge Network](/help/implementation/edge/implementation-edge.md).

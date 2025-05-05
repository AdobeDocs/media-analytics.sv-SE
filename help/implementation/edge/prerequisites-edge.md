---
title: Förutsättningar för implementering av endast Adobe Analytics
description: Lär dig om förutsättningarna för att använda Streaming Media Collection med implementeringar som endast gäller för Adobe Analytics eller Edge
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Krav för Edge-implementeringar

De krav som beskrivs i det här avsnittet gäller specifikt för implementering av Adobe Streaming Media Collection med Edge-implementeringar.

1. **Slutför de allmänna kraven**<br>
Oavsett om du implementerar Streaming Media Collection för implementeringar av endast Adobe Analytics eller för Edge måste du se till att du uppfyller de [allmänna kraven ](/help/getting-started/prereqs.md) .

1. **Bekräfta att du implementerar en Adobe-lösning som är kompatibel med Edge Network och direktuppspelningsmediesamlingen**<br>
När du implementerar Streaming Media Collection med Edge måste du också ha en fungerande Customer Journey Analytics-, Adobe Analytics-, Adobe Journey Optimizer- eller Real-time Customer Data Platform-implementering. Mer information finns i följande dokumentationsresurser:
   * [Guiden Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=sv-SE)
   * [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=sv-SE)
   * [Adobe Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=sv-SE)
   * [Real-time Customer Data Platform-dokumentation](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=sv-SE)

1. **Hämta URL:en för mediespårningsservern**<br>
Be din Customer Journey Analytics-representant om URL:en för mediespårningsservern. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementera den direktuppspelande mediesamlingen med Edge Network**<br>
Följ stegen i [Implementera den direktuppspelade mediesamlingen med Edge Network](/help/implementation/edge/implementation-edge.md).

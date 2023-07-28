---
title: Förutsättningar för implementering av endast Adobe Analytics
description: Lär dig om förutsättningarna för att använda direktuppspelningsmedia med implementeringar som endast är för Adobe Analytics
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# Krav för Edge-implementeringar

De krav som beskrivs i det här avsnittet är specifika för implementering av Streaming Media med Edge-implementeringar.

1. **Slutför de allmänna kraven**<br>
Oavsett om du implementerar Streaming Media för implementeringar av endast Adobe Analytics eller för Edge-implementeringar måste du se till att du uppfyller [allmänna krav](/help/getting-started/prereqs.md).

1. **Bekräfta att du implementerar en Adobe-lösning som är kompatibel med Edge och Streaming Media**<br>
När du implementerar Streaming Media med Edge måste du också ha en fungerande Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer eller en Real-time Customer Data Platform-implementering. Mer information finns i följande dokumentationsresurser:
   * [Customer Journey Analytics guide](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=en)
   * [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
   * [Adobe Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer.html)
   * [Real-time Customer Data Platform-dokumentation](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **Hämta URL:en för mediespårningsservern**<br>
Be din Customer Journey Analytics-representant om URL:en för mediespårningsservern. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Installera Media Analytics med Edge**<br>
Följ stegen i [Installera Media Analytics med Experience Platform Edge](/help/implementation/edge/implementation-edge.md).
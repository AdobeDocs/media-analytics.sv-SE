---
title: Få tillgång till länkar för att hämta SDK:er för medieanalys
description: Länkar till SDK nedladdningar för tillgängliga plattformar, inklusive Android, iOS, JavaScript, Chromecast och Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 9%

---

# Hämta SDK:er för media, tillägg med taggar och OTT SDK:er {#download-sdks}

Informationen på den här sidan innehåller länkar för att hämta aktuella media-SDK:er och hämta medietillägg som använder taggar.

Taggar i Adobe Experience Platform är nästa generation av funktioner för hantering av webbplatstaggar och mobiler i SDK från Adobe. Taggar är ett enkelt sätt att driftsätta och hantera de analyser-, marknadsförings- och annonslösningar som behövs för att skapa relevanta kundupplevelser. Mer information om taggar finns i [Översikt över taggar](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=en).


>[!NOTE]
>
>Mer information om hur du hämtar äldre SDK:er finns i [Äldre - Hämta SDK:er](/help/legacy/legacy-download-sdks.md).<br>
>&#x200B;>Viktig information om att supporten upphör finns i [Vanliga frågor om supporten](/help/additional-resources/end-of-support-faqs.md).

## Media SDK och mobila bibliotek {#media-sdks-libraries}

### Webbimplementering {#download-web-sdk}

| Plattform som stöds | Lösningar | Implementeringsmetod | Version |  API:er   |  Dokumentation  |  Exempel  |
|:---:|---|---|---|---| ---| ---|
| ![JavaScript-ikon ](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | Endast analyser | Webb - [Media SDK för JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [API-referens för JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Installera Media SDK med JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Media SDK för JS v3.0.2 - exempel](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript-ikon ](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | Endast analyser | Webb - Medietillägg |  | [Adobe Media Analytics (3.x SDK) för ljud- och videotillägg - med taggar (datainsamling)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=en) | [Adobe Media Analytics (3.x SDK) for Audio and Video Extension Sample](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Webb** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Webb - Experience Platform Edge |  | [Implementera Customer Journey Analytics Streaming Media Collection med Edge Network](/help/implementation/edge/implementation-edge.md) <p>och</p><p>[Skicka webbdata till Edge med Adobe Experience Platform Web SDK](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Mobilimplementering {#get-mobile-extension}

| Plattform som stöds | Lösningar | Implementeringsmetod | Version |  Dokumentation   |  Exempel  |
|:---:|---|---|---|---|---|
| ![Android, ikon ](assets/android-icon.png)</br>**Android** | Adobe Analytics | Endast analyser | Android - Media Extension | [Mobile SDK-dokumentation](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Exempel på medieanalys för ljud och video](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS, ikon ](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Endast analyser | iOS/tvOS - medietillägg | [Mobile SDK-dokumentation](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Exempel på medieanalys för ljud och video](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Android, ikon ](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | ANDROID - EXPERIENCE PLATFORM EDGE | [Installera Media SDK med JavaScript](/help/implementation/edge/implementation-edge.md) | |
| ![Apple iOS, ikon ](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS / tvOS - Experience Platform Edge | [Installera Media SDK med JavaScript](/help/implementation/edge/implementation-edge.md) |  |

### Ovanför implementering {#download-ott-libraries}

| Plattform som stöds | Lösningar | Implementeringsmetod | Version |  API:er   |  Dokumentation  |
|:---:|---|---|---|---|---|
| ![Chromecast, ikon ](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Endast analyser | [SDK för Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [API-referens för Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Konfigurera Mobile SDK v3.x för Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku, ikon ](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | Endast analyser | [SDK för Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [Konfigurera Mobile SDK v2.x för Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![Roku, ikon ](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [Installera Media SDK med JavaScript](/help/implementation/edge/implementation-edge.md) |

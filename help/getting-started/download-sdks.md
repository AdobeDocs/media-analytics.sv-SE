---
title: Få tillgång till länkar för att ladda ned SDK:er för Media Analytics
description: Länkar till SDK-nedladdningar för tillgängliga plattformar, inklusive Android, iOS, JavaScript, Chromecast och Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 1%

---

# Hämta SDK:er för media, tillägg med hjälp av taggar och OTT SDK:er {#download-sdks}

Informationen på den här sidan innehåller länkar för att hämta aktuella media-SDK:er och hämta medietillägg.

Informationen på den här sidan innehåller länkar för att hämta aktuella SDK:er för media och för att hämta medietillägg som använder taggar.

Taggar i Adobe Experience Platform är nästa generation av funktioner för hantering av webbplatstaggar och SDK för mobila enheter från Adobe. Taggar är ett enkelt sätt att driftsätta och hantera de analyser-, marknadsförings- och annonslösningar som behövs för att skapa relevanta kundupplevelser. Mer information om taggar finns i [Översikt över taggar](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=sv)


>[!NOTE]
>
>Mer information om hur du hämtar äldre SDK:er finns i [Äldre - Hämta SDK:er](/help/legacy/legacy-download-sdks.md).<br>
>Viktig information om att supporten upphör finns i [Vanliga frågor och svar om supporten upphör](/help/additional-resources/end-of-support-faqs.md).

## Media SDK och Mobile Libraries {#media-sdks-libraries}

### Webbimplementering {#download-web-sdk}

| Plattform som stöds | Version |  API:er   |  Dokumentation  |  Exempel  |
|:---:|---|---|---|---|
| ![JavaScript-ikon](assets/javascript-icon.png) | Webb - [Media SDK för JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [JavaScript API-referens](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Konfigurera Media SDK v3.x för JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Media SDK för JS v3.0.2 - exempel](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript-ikon](assets/javascript-icon.png) | Webb - Medietillägg |  | [Adobe Media Analytics (3.x SDK) for Audio and Video extension - using Tags (Data Collection)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=en) | [Adobe Media Analytics (3.x SDK) for Audio and Video Extension Sample](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |

### Mobilimplementering {#get-mobile-extension}

| Plattform som stöds | Version |  Dokumentation   |  Exempel  |
|:---:|---|---|---|
| ![Android-ikon](assets/android-icon.png) | Android - medietillägg | [Mobile SDK-dokumentation](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Media Analytics for Audio and Video Sample](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS, ikon](assets/ios-icon.png)<br>lägg till tvOS-ikon | iOS/tvOS - medietillägg | [Mobile SDK-dokumentation](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Media Analytics for Audio and Video Sample](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |

### Ovanför implementering {#download-ott-libraries}

| Plattform som stöds | Version |  API:er   |  Dokumentation  |
|:---:|---|---|---|
| ![Chromecast-ikon](assets/chromecast-icon.png) | [SDK för Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [API-referens för Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Konfigurera Mobile SDK v3.x för Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku-ikon](assets/roku-icon.png) | [SDK för Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) | [Referens för Roku-API](/help/implementation/media-sdk/setup/set-up-roku.md) | [Konfigurera Mobile SDK v2.x för Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |

## Adobe Extensions {#adobe-extensions}

### Direktuppspelande medietillägg {#streaming-media-extension}

The **Adobe Media Analytics för ljud- och videotillägg** kräver Adobe Analytics for Media-tillägget SKU. Om du vill ha mer information kan du kontakta din säljare, kontoansvarige eller kundansvarige på Adobe.

Detaljerad information om hur du installerar, konfigurerar och implementerar **Adobe Media Analytics för ljud- och videotillägg**, se [Adobe Media Analytics för ljud- och videotillägg - översikt](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) och [Konfigurera Media Analytics-tillägget](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics#configure-the-media-analytics-extension).

### Analystillägg {#analytics-extension}

[Analytics Extension v1.6 eller senare](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en)- Med det här tillägget kan du läsa in JavaScript-biblioteket för Adobe Experience Platform Web SDK för att skicka data till lösningar från Adobe. The **Analystillägg** v1.6 eller senare krävs.

Mer information om hur du konfigurerar det här tillägget finns i [Konfigurera Adobe Analytics-tillägget](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en).

### Experience Cloud ID-tillägg {#cloud-id-extension}

[Experience Cloud ID-tillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)- Det här tillägget implementerar Experience Cloud ID-tjänsten som identifierar besökare över alla Experience Cloud-lösningar. Experience Cloud ID-tjänsten är ett personaliseringstillägg i Adobe Experience Platform.

Använd det här tillägget om du vill integrera Experience Cloud Identity Service med din egendom. Med Experience Cloud Identity Service kan ni skapa och lagra unika och beständiga identifierare för era webbplatsbesökare.

Mer information om hur du konfigurerar det här tillägget finns i [Konfigurera Experience Cloud ID-tillägget](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)

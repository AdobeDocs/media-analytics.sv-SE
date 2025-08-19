---
title: Skicka webbdata till Edge med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar Adobe direktuppspelade mediedata till Experience Platform Edge med Adobe Experience Platform Web SDK.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Skicka webbdata till Edge med Adobe Experience Platform Web SDK

Från och med version 2.20.0 gör komponenten `streamingMedia` i Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) att du kan samla in data relaterade till mediesessioner på din webbplats. De insamlade data kan innehålla information om medieuppspelningar, pauser, slutföranden och andra relaterade händelser.

När data har samlats in kan du skicka dem till Adobe Experience Platform och/eller Adobe Analytics för att generera rapporter. Den här funktionen är en heltäckande lösning för att spåra och förstå hur medieanvändningen fungerar på din webbplats.

För kunder som använder Media JS SDK erbjuder Web SDK en migreringsväg för att gå från Media JS SDK till Web SDK, med stöd för befintliga Media JS-funktioner, som hantering av mediahändelser.

## Förutsättningar {#prerequisites}

Om du vill använda komponenten `streamingMedia` i Web SDK måste du uppfylla följande krav:

* Innan du kan skicka strömmande mediedata till Edge måste du först slutföra stegen i [Implementera Adobe direktuppspelade medietjänster med Edge Network](/help/implementation/edge/implementation-edge.md).
* Kontrollera att du har tillgång till Adobe Experience Platform och/eller Adobe Analytics.
* Du måste använda Web SDK version 2.20.0 eller senare. Se [installationsöversikten för Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) om du vill veta hur du installerar den senaste versionen.
* Aktivera alternativet **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** för den datastream du använder.
* Kontrollera att schemat som används av din datastream innehåller schemafälten för mediesamlingen.
* Konfigurera direktuppspelande medietjänster i Web SDK-konfigurationen, vilket visas på den här sidan, antingen med [taggtillägget](#tag-extension) eller via [JavaScript-biblioteket](#library).

Följ stegen som beskrivs på den här sidan för att migrera implementeringen av dina tjänster för direktuppspelande media från Media JS till Web SDK.

### Steg 1: Installera Experience Platform Web SDK

Läs den [dedikerade dokumentationen](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) om du vill veta hur du installerar Web SDK på dina webbegenskaper.

### Steg 2: Konfigurera Web SDK `streamingMedia`-komponenten.

**Exempel**

I utdraget nedan visas hur du konfigurerar mediesamlingen i Media JS.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

I stället måste du konfigurera komponenten `streamingMedia` i Web SDK enligt exemplet nedan.

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Mer information om hur du konfigurerar den finns i Web SDK `streamingMedia`-komponenten [documentation](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia).

### Steg 3: Hämta instansen av mediespåraren när du migrerar från Media JS SDK

För kunder som använder Media JS SDK erbjuder Web SDK en migreringsväg för att gå från Media JS SDK till Web SDK, med stöd för befintliga Media JS-funktioner, som hantering av mediahändelser.

[!DNL Web SDK] innehåller ett kommando för att hämta en Media Analytics-spårare. Du kan använda det här kommandot för att skapa en objektinstans och sedan, med samma API:er som de som finns i [Media JS-biblioteket](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), spåra mediahändelser.

Mer information om vilka metoder som stöds finns i dokumentationen för [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker).

I kodutdraget nedan visas hur du hämtar mediaspårningsinstansen i Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

Använd i stället kommandot `getMediaAnalyticsTracker` i Web SDK för att uppnå samma resultat, vilket visas nedan.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Alla hjälpmetoder är tillgängliga för objektet `Media`. Spårningsmetoderna är tillgängliga för spårningsinstansen, vilket visas nedan.

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```

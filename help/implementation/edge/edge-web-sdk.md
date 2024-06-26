---
title: Skicka webbdata till Edge med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar Adobe Streaming Media-data till Experience Platform Edge med Adobe Experience Platform Web SDK.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Skicka webbdata till Edge med Adobe Experience Platform Web SDK

Från och med version 2.20.0 är `streamingMedia` Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) gör att du kan samla in data om mediesessioner på din webbplats. De insamlade data kan innehålla information om medieuppspelningar, pauser, slutföranden och andra relaterade händelser.

När data har samlats in kan du skicka dem till Adobe Experience Platform och/eller Adobe Analytics för att generera rapporter. Den här funktionen är en heltäckande lösning för att spåra och förstå hur medieanvändningen fungerar på din webbplats.

För kunder som använder Media JS SDK erbjuder Web SDK en migreringsväg från Media JS SDK till Web SDK, med stöd för befintliga Media JS-funktioner, som hantering av mediahändelser.

## Förutsättningar {#prerequisites}

Använd `streamingMedia` som ingår i Web SDK, måste du uppfylla följande krav:

* Innan du kan skicka strömmande mediedata till Edge måste du slutföra stegen i [Installera tillägget Streaming Media Collection med Experience Platform Edge](/help/implementation/edge/implementation-edge.md).
* Kontrollera att du har tillgång till Adobe Experience Platform och/eller Adobe Analytics.
* Du måste använda Web SDK version 2.20.0 eller senare. Se [Web SDK - installationsöversikt](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) om du vill lära dig hur du installerar den senaste versionen.
* Aktivera **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** för den datastream du använder.
* Kontrollera att schemat som används av din datastream innehåller schemafälten för mediesamlingen.
* Konfigurera funktionen Direktuppspelning av media i Web SDK-konfigurationen, som visas på den här sidan, antingen via [taggtillägg](#tag-extension) eller via [JavaScript-bibliotek](#library).

Följ stegen som beskrivs på den här sidan för att migrera implementeringen av tillägget Streaming Media Collection från Media JS till Web SDK.

### Steg 1: Installera Experience Platform Web SDK

Se [dedikerad dokumentation](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) om du vill lära dig hur du installerar Web SDK på dina webbegenskaper.

### Steg 2: Konfigurera Web SDK `streamingMedia` -komponenten.

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

Istället måste du konfigurera `streamingMedia` i Web SDK enligt exemplet nedan.

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

Se Web SDK `streamingMedia` komponent [dokumentation](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) om du vill ha fullständig information om hur du konfigurerar den.

### Steg 3: Hämta instansen av mediespåraren när du migrerar från mediets JS SDK

För kunder som använder Media JS SDK erbjuder Web SDK en migreringsväg från Media JS SDK till Web SDK, med stöd för befintliga Media JS-funktioner, som hantering av mediahändelser.

[!DNL Web SDK] innehåller ett kommando för att hämta en Media Analytics-spårare. Du kan använda det här kommandot för att skapa en objektinstans och sedan använda samma API:er som de som finns i [Media JS-bibliotek](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), spåra mediahändelser.

Se [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) dokumentation för fullständig information om vilka metoder som stöds.

I kodutdraget nedan visas hur du hämtar mediaspårningsinstansen i Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

Använd i stället `getMediaAnalyticsTracker` i Web SDK för att uppnå samma resultat, vilket visas nedan.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Alla hjälpmetoder är tillgängliga på `Media` -objekt. Spårningsmetoderna är tillgängliga för spårningsinstansen, vilket visas nedan.

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

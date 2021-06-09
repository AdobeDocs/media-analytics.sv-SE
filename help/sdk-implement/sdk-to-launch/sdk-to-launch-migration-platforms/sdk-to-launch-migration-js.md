---
title: Migrera från det fristående medie-SDK:t till Adobe Launch - webben (JS)
description: Instruktioner och kodexempel som hjälper dig att migrera från Media SDK till Launch.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 3%

---

# Migrera från det fristående medie-SDK:t till Adobe Launch - webben (JS)

## Skillnader i funktioner

* *Launch*  - Launch ger dig ett användargränssnitt som hjälper dig att konfigurera, konfigurera och driftsätta dina webbaserade mediespårningslösningar. Launch förbättrar Dynamic Tag Management (DTM).
* *Media SDK*  - Media SDK innehåller bibliotek för mediespårning som utformats för särskilda plattformar (t.ex.: Android, iOS osv.). Adobe rekommenderar Media SDK för att spåra medieanvändning i dina mobilappar.

## Konfiguration

### Fristående media SDK

I det fristående Media SDK:t konfigurerar du spårningskonfigurationen i appen
och skicka det till SDK när du skapar spåraren.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

Förutom `MediaHeartbeat`-konfigurationen måste sidan konfigurera och skicka
instansen `AppMeasurement` och instansen `VisitorAPI` för mediespårning i ordning
att fungera som det ska.

### Starta tillägg

1. Klicka på fliken [!UICONTROL Extensions] i Experience Platform Launch för
web-egenskap.
1. På fliken [!UICONTROL Catalog] letar du reda på Adobe Media Analytics for Audio och
Videotillägg och klicka på [!UICONTROL Install].
1. Konfigurera spårningsparametrarna på sidan för tilläggsinställningar.
Media-tillägget använder de konfigurerade parametrarna för spårning.

   ![](assets/launch_config_js.png)

[Starta användarhandboken - Installera och konfigurera medietillägget](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## Skillnader mellan att skapa spårare

### Media SDK

1. Lägg till biblioteket Media Analytics i utvecklingsprojektet.
1. Skapa ett config-objekt (`MediaHeartbeatConfig`).
1. Implementera delegatprotokollet och visa funktionerna `getQoSObject()` och `getCurrentPlaybackTime()`.
1. Skapa en instans av pulsslag för media (`MediaHeartbeat`).

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

<!--  Dead Link - from 2019 - can't locate where this should go
[Media SDK - Tracker Creation](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html) -->

### Starta

Launch erbjuder två sätt att skapa spårningsinfrastrukturen. Båda metoderna använder startalternativet för Media Analytics:

1. Använd API:erna för mediespårning från en webbsida.

   I det här scenariot exporterar Media Analytics-tillägget API:erna för mediespårning till en konfigurerad variabel i det globala fönsterobjektet:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Använd API:erna för mediespårning från ett annat Launch-tillägg.

   I det här scenariot använder du API:erna för mediespårning som visas av de delade modulerna `get-instance` och `media-heartbeat`.

   >[!NOTE]
   >
   >Delade moduler är inte tillgängliga för användning på webbsidor. Du kan bara använda delade moduler från andra tillägg.

   Skapa en `MediaHeartbeat`-instans med den delade modulen `get-instance`.
Skicka ett delegatobjekt till `get-instance` som visar funktionerna `getQoSObject()` och `getCurrentPlaybackTime()`.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Få åtkomst till `MediaHeartbeat`-konstanter via den delade modulen `media-heartbeat`.

## Relaterad dokumentation

### Media SDK

* [Konfigurera JavaScript 2.x](/help/sdk-implement/setup/setup-javascript/set-up-js-2.md)
* [Konfigurera JavaScript 3.x](/help/sdk-implement/setup/setup-javascript/set-up-js-3.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Starta

* [Översikt över Launch](https://experienceleague.adobe.com/docs/launch/using/overview.html)
* [Media Analytics-tillägg](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

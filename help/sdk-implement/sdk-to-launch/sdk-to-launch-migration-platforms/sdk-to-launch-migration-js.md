---
title: Migrera från fristående Media SDK till Adobe Launch - webben (JS)
description: Instruktioner och kodexempel som hjälper dig att migrera från Media SDK till Launch.
translation-type: tm+mt
source-git-commit: 0f9a985d04969eeca837a2655c666259ce30aee4
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 2%

---


# Migrera från fristående Media SDK till Adobe Launch - webben (JS)

## Skillnader i funktioner

* *Launch* - Launch ger dig ett användargränssnitt som hjälper dig att konfigurera, konfigurera och driftsätta dina webbaserade mediespårningslösningar. Launch förbättrar Dynamic Tag Management (DTM).
* *Media SDK* - Media SDK innehåller bibliotek för mediespårning som är utformade för särskilda plattformar (t.ex.: Android, iOS osv.). Adobe rekommenderar Media SDK för att spåra medieanvändning i dina mobilappar.

## Konfiguration

### Fristående media SDK

I det fristående Media SDK konfigurerar du spårningskonfigurationen i appen och skickar den till SDK när du skapar spåraren.

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

Förutom `MediaHeartbeat` konfigurationen måste sidan konfigurera och skicka `AppMeasurement` instans och `VisitorAPI` instans för mediespårning för att fungera korrekt.

### Starta tillägg

1. Klicka på fliken för din webbegenskap i Experience Platform Launch [!UICONTROL Extensions] .
1. På [!UICONTROL Catalog] fliken letar du reda på Adobe Media Analytics för ljud och video och klickar på [!UICONTROL Install].
1. Konfigurera spårningsparametrarna på sidan för tilläggsinställningar.
Media-tillägget använder de konfigurerade parametrarna för spårning.

   ![](assets/launch_config_js.png)

[Starta användarhandboken - Installera och konfigurera medietillägget](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## Skillnader mellan att skapa spårare

### Media SDK

1. Lägg till biblioteket Media Analytics i utvecklingsprojektet.
1. Skapa ett config-objekt (`MediaHeartbeatConfig`).
1. Implementera delegatprotokollet, så att funktionerna `getQoSObject()` och `getCurrentPlaybackTime()` visas.
1. Skapa en instans av pulsslag (`MediaHeartbeat`).

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
[Media SDK - Tracker Creation](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html) -->

### Starta

Launch erbjuder två sätt att skapa spårningsinfrastrukturen. Båda metoderna använder startalternativet för Media Analytics:

1. Använd API:erna för mediespårning från en webbsida.

   I det här scenariot exporterar Media Analytics-tillägget API:erna för mediespårning till en konfigurerad variabel i det globala fönsterobjektet:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Använd API:erna för mediespårning från ett annat Launch-tillägg.

   I det här scenariot använder du API:erna för mediespårning som visas av modulerna `get-instance` och `media-heartbeat` Delade.

   >[!NOTE]
   >
   >Delade moduler är inte tillgängliga för användning på webbsidor. Du kan bara använda delade moduler från andra tillägg.

   Skapa en `MediaHeartbeat` instans med hjälp av den `get-instance` delade modulen.
Skicka ett delegatobjekt till `get-instance` som visar `getQoSObject()` och `getCurrentPlaybackTime()` funktioner.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Få åtkomst till `MediaHeartbeat` konstanter via den `media-heartbeat` delade modulen.

## Relaterad dokumentation

### Media SDK

* [Konfigurera JS](/help/sdk-implement/setup/set-up-js.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Starta

* [Översikt](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Media Analytics-tillägg](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

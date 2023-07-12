---
title: "Migrering från det fristående mediet-SDK till Adobe Launch - webben (JS)"
description: Lär dig hur du migrerar från Media SDK till Launch for JS.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 73ef5e55c9ab57a5a2ba22aa1e4b646c530cc53f
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---

# Migrera från det fristående medie-SDK:t till Adobe Launch - webben (JS)

>[!NOTE]
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) för en konsoliderad hänvisning till terminologiska förändringar.

## Skillnader i funktioner

* *Starta* - Launch ger dig ett användargränssnitt som hjälper dig att konfigurera, konfigurera och driftsätta dina webbaserade mediespårningslösningar. Launch är bättre än Dynamic Tag Management (DTM).
* *Media SDK* - Med Media SDK får du mediespårningsbibliotek som är utformade för särskilda plattformar (t.ex.: Android, iOS osv.). Adobe rekommenderar Media SDK för att spåra medieanvändning i dina mobilappar.

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

Förutom `MediaHeartbeat` måste sidan konfigurera och skicka `AppMeasurement` instans och `VisitorAPI` instans för mediespårning för att fungera korrekt.

### Starta tillägg

1. I Experience Platform Launch klickar du på [!UICONTROL Extensions] -fliken för din webbegenskap.
1. På [!UICONTROL Catalog] går du till Adobe Media Analytics för ljud- och videotillägg och klickar på [!UICONTROL Install].
1. Konfigurera spårningsparametrarna på sidan för tilläggsinställningar.
Media-tillägget använder de konfigurerade parametrarna för spårning.

   ![](assets/launch_config_js.png)

[Starta användarhandboken - Installera och konfigurera medietillägget](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html#install-and-configure-the-ma-extension)

## Skillnader mellan att skapa spårare

### Media SDK

1. Lägg till biblioteket Media Analytics i utvecklingsprojektet.
1. Skapa ett config-objekt (`MediaHeartbeatConfig`).
1. Implementera delegatprotokollet, visa `getQoSObject()` och `getCurrentPlaybackTime()` funktioner.
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

### Starta

Launch erbjuder två sätt att skapa spårningsinfrastrukturen. Båda metoderna använder startalternativet för Media Analytics:

1. Använd API:erna för mediespårning från en webbsida.

   I det här scenariot exporterar Media Analytics-tillägget API:erna för mediespårning till en konfigurerad variabel i det globala fönsterobjektet:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Använd API:erna för mediespårning från ett annat Launch-tillägg.

   I det här scenariot använder du API:erna för mediespårning som visas av `get-instance` och `media-heartbeat` Delade moduler.

   >[!NOTE]
   >
   >Delade moduler är inte tillgängliga för användning på webbsidor. Du kan bara använda delade moduler från andra tillägg.

   Skapa en `MediaHeartbeat` -instans med `get-instance` Delad modul.
Skicka ett delegatobjekt till `get-instance` som exponeras `getQoSObject()` och `getCurrentPlaybackTime()` funktioner.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Åtkomst `MediaHeartbeat` konstanter via `media-heartbeat` Delad modul.

## Relaterad dokumentation

### Media SDK

* [Konfigurera JavaScript 2.x](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Starta

* [Översikt över Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
* [Media Analytics-tillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)

---
title: Migrera från fristående Media SDK till Adobe Launch - Android
description: Instruktioner och kodexempel som hjälper dig att migrera från Media SDK till Launch för Android.
translation-type: tm+mt
source-git-commit: bc896cc403923e2f31be7313ab2ca22c05893c45

---


# Migrera från fristående Media SDK till Adobe Launch - Android

## Konfiguration

### Fristående media SDK

I det fristående Media SDK konfigurerar du spårning i appen och skickar den till SDK när du skapar spåraren.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeat tracker = new MediaHeartbeat(... , config);
```

### Starta tillägg

1. Klicka på fliken för din mobila egenskap i Experience Platform Launch [!UICONTROL Extensions] .
1. Gå till fliken [!UICONTROL Catalog] , leta upp Adobe Media Analytics för ljud- och videotillägg och klicka på [!UICONTROL Install].
1. Konfigurera spårningsparametrarna på sidan för tilläggsinställningar.
Media-tillägget använder de konfigurerade parametrarna för spårning.

![](assets/launch_config_mobile.png)

[Använda mobiltillägg](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## Skapa spårare

### Fristående media SDK

I den fristående Media SDK skapar du objektet manuellt och konfigurerar spårningsparametrarna `MediaHeartbeatConfig` . Implementera delegatgränssnittet för att visa`getQoSObject()` och `getCurrentPlaybackTime()functions.`skapa en `MediaHeartbeat` instans för spårning.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeatDelegate delegate = new MediaHeartbeatDelegate() {
    @Override 
    public MediaObject getQoSObject() {
        // When called should return the latest qos values.
        return MediaHeartbeat.createQoSObject(<bitrate>,  
                                              <startupTime>,  
                                              <fps>,  
                                              <droppedFrames>); 
    } 

    @Override 
    public Double getCurrentPlaybackTime() { 
        // When called should return the current player time in seconds.
        return <currentPlaybackTime>; 
    }

    MediaHeartbeat tracker = new MediaHeartbeat(delegate, config);
}
```

### Starta tillägg

[Media API-referens - Skapa en mediaspårare](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Innan du skapar spåraren bör du registrera medietillägget och de beroende tilläggen med mobilkärnan.

```java
// Register the extension once during app launch
try {
    // Media needs Identity and Analytics extension 
    // to function properly
    Identity.registerExtension();
    Analytics.registerExtension();

    // Initialize media extension.
    Media.registerExtension();                
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            // Launch mobile property to pick extension settings.
            MobileCore.configureWithAppID("LAUNCH_MOBILE_PROPERTY");
        }
    });
} catch (InvalidInitException ex) {
    ...
}
```

När du har registrerat medietillägget skapar du spåraren med följande API.
Spåraren väljer automatiskt konfigurationen från den konfigurerade startegenskapen.

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

## Uppdaterar värden för spelhuvud och upplevelsekvalitet.

### Fristående media SDK

I den fristående Media SDK:n skickar du ett delegatobjekt som implementerar gränssnittet när`MediaHeartbeartDelegate` spåraren skapas.  Implementeringen bör returnera den senaste QoE-koden och spelhuvudet när spåraren anropar metoderna för`getQoSObject()` gränssnitt och `getCurrentPlaybackTime()` gränssnitt.

### Starta tillägg

Implementeringen bör uppdatera spelarens spelhuvud genom att`updateCurrentPlayhead` anropa metoden som exponeras av spåraren. För korrekt spårning bör du anropa den här metoden minst en gång per sekund.

[Media API-referens - Uppdatera aktuell spelare](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

Implementeringen bör uppdatera QoE-informationen genom att anropa den `updateQoEObject`metod som exponeras av spåraren. Vi förväntar oss att den här metoden anropas närhelst det finns en ändring i kvalitetsmåtten.

[Media API-referens - Uppdatera QoE-objekt](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## Skicka standardmedier/annonsmetadata

### Fristående media SDK

* Standardmetadata för media:

   ```java
   MediaObject mediaInfo = 
     MediaHeartbeat.createMediaObject("media-name", 
                                      "media-id", 
                                      60D, 
                                      MediaHeartbeat.StreamType.VOD, 
                                      MediaHeartbeat.MediaType.Video);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardVideoMetadata = 
     new HashMap<String, String>(); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, 
                             "Sample Episode"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, 
                             "Sample Show"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, 
                             "Sample Season"); 
   mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata, 
                      standardVideoMetadata);
   
   // Custom metadata keys
   HashMap<String, String> mediaMetadata = new HashMap<String, String>();
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Standardmetadata för annonsering:

   ```java
   MediaObject adInfo = 
     MediaHeartbeat.createAdObject("ad-name", 
                                   "ad-id", 
                                   1L, 
                                   15D);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardAdMetadata = 
     new HashMap<String, String>(); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, 
                          "Sample Advertiser"); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, 
                          "Sample Campaign"); 
   adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, 
                   standardAdMetadata); 
   
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   
   tracker.trackEvent(MediaHeartbeat.Event.AdStart, 
                      adObject, 
                      adMetadata);
   ```

### Starta tillägg

* Standardmetadata för media:

   ```java
   HashMap<String, Object> mediaObject = 
     Media.createMediaObject("media-name", 
                             "media-id", 
                             60D, 
                             MediaConstants.StreamType.VOD, 
                             Media.MediaType.Video);
   
   HashMap<String, String> mediaMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE, 
                     "Sample Episode");
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW, 
                     "Sample Show");
   
   // Custom metadata keys
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Standardmetadata för annonsering:

   ```java
   HashMap<String, Object> adObject = 
     Media.createAdObject("ad-name", 
                          "ad-id", 
                          1L, 
                          15D);
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER, 
                  "Sample Advertiser");
   adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID, 
                  "Sample Campaign");
   
   // Custom metadata keys
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   _tracker.trackEvent(Media.Event.AdStart, 
                       adObject, 
                       adMetadata);
   ```

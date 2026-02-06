---
title: Migrera från fristående media SDK till Adobe Launch - Android
description: Lär dig hur du migrerar från Media SDK till Launch för Android.
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 7%

---

# Migrera från fristående Media SDK till Adobe Launch - Android

>[!NOTE]
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) för en konsoliderad referens av terminologiändringarna.


## Konfiguration

### Fristående media SDK

I det fristående Media SDK konfigurerar du spårning i appen och skickar den till
SDK när du skapar spåraren.

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

1. I Experience Platform Launch klickar du på fliken [!UICONTROL Extensions] för
mobil egenskap.
1. På fliken [!UICONTROL Catalog] letar du reda på Adobe Media Analytics for Audio
och videotillägg och klicka på [!UICONTROL Install] .
1. Konfigurera spårningsparametrarna på sidan för tilläggsinställningar.
Media-tillägget använder de konfigurerade parametrarna för spårning.

![](assets/launch_config_mobile.png)

[Använda mobiltillägg](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

## Skapa spårare

### Fristående media SDK

I den fristående Media SDK skapar du `MediaHeartbeatConfig`-objektet manuellt
och konfigurera spårningsparametrarna. Implementera delegatgränssnittets exponering
`getQoSObject()` och `getCurrentPlaybackTime()functions.`
Skapa en `MediaHeartbeat` -instans för spårning.

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

[Media API-referens - Skapa en mediespårare](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createtracker)

Innan du skapar spåraren bör du registrera medietillägget och
beroende tillägg till mobilbasen.

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

I det fristående Media SDK skickar du ett delegatobjekt som implementerar
`MediaHeartbeartDelegate`-gränssnittet när spåraren skapas.  Implementeringen
ska returnera det senaste QoE-numret och spelhuvudet när spåraren anropar
Gränssnittsmetoderna `getQoSObject()` och `getCurrentPlaybackTime()`.

### Starta tillägg

Implementeringen bör uppdatera spelarens spelhuvud genom att anropa
Metoden `updateCurrentPlayhead` som exponeras av spåraren. För korrekt spårning
anropa den här metoden minst en gång per sekund.

[Media API-referens - Uppdatera aktuell spelare](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#updatecurrentplayhead)

Implementeringen bör uppdatera QoE-informationen genom att anropa `updateQoEObject`
metod som exponeras av spåraren. Vi förväntar oss att den här metoden anropas när det finns
är en förändring av kvalitetsstatistik.

[Media API-referens - Uppdatera QoE-objekt](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createqoeobject)

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

---
title: Återupptar inaktiva sessioner
description: Lär dig hur du återtar en inaktiv session.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Återuppta inaktiva sessioner{#resuming-inactive-sessions}

## Långa pauser

Media SDK spårar automatiskt hur lång medieuppspelningen är i ett av följande inaktiva lägen:

* Pausad
* Söker
* Stängd
* Buffring

Om en mediespårningssession är inaktiv i mer än 30 minuter stängs sessionen automatiskt. Om användaren återupptar efter en tidigare inaktiv videospårningssession (`trackPlay`) skapar Media Heartbeat automatiskt en ny videosession med den videoinformation och de metadata som användes tidigare och skickar en CV-händelse (CV). Mer information finns i [Parametrar för ljud och video.](/help/implementation/variables/audio-video-parameters.md)


## Återuppta tidigare stängd session manuellt

Media SDK återupptar endast sessioner automatiskt om programmet inte stängs. Om programmet lagrar användardata och har möjlighet att återuppta ett tidigare stängt medium, är det möjligt att manuellt utlösa en resume-händelse. När du startar videospårningssessionen anger du den valfria egenskapen Videoåterupptagen.

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true
public void onmediaLoad(Observable observable, Object data) {

  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD
  );

  // Set to true if this is a resume playback scenario
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);

  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification {
  //Replace <MEDIA_NAME> with the media name.
  //Replace <MEDIA_ID> with a media unique identifier.
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                       mediaId:<MEDIA_ID>
                       length:<MEDIA_LENGTH>
                       streamType:ADBMediaHeartbeatStreamTypeVOD];

  //Set to YES if this user is resuming a previously closed media session
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata];
}
```

### JavaScript

```js
_onmediaLoad = function () {
  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session
  mediaObject.setValue(MediaObjectKey.mediaResumed, true);
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```

---
title: Implementera standardmetadata med JavaScript 2.x
description: Beskriver hur du ställer in standardmetadata för video och annonsering som ska skickas med spårningsanrop i webbläsarappar (JS).
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 4%

---


# Implementera standardmetadata med JavaScript 2.x{#implement-standard-metadata-on-javascript}

## Metadatakonstant

| Konstantnamn | Beskrivning   |
| --- | --- |
| `StandardMediaMetadata` | Konstant för att bifoga standardmetadata på `MediaObject` |

## Implementering

Instansiera ett metadataobjekt av standardtyp, fyll i önskade variabler och ange metadataobjektet i objektet Mediepulsslag. Exempel:

```js
_onVideoLoad = function () {
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                       <MEDIA_ID,  
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";

    //Set standard Audio Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label";

    mediaInfo.setValue(MediaObjectKey.StandardMediaMetadata, standardMediaMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

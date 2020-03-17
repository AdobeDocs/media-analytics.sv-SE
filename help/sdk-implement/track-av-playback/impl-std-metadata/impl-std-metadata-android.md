---
title: Implementera standardmetadata på Android
description: Beskriver hur du ställer in standardmetadata för video och annonsering som ska skickas med spårningsanrop på Android.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementera standardmetadata på Android{#implement-standard-metadata-on-android}

## Standardmetadatakonstanter

| Konstantnamn | Beskrivning |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Konstant för att bifoga standardmetadata på `MediaObject`. |

## API-referens för metadatanycklar

* Skapa ett `HashMap` standardpar med metadatanyckelvärden.
   * [Metadatanycklar för video](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Tangenter för ljudmetadata](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Ange standardmetadata `HashMap` för `MediaInfo` att använda konstanten Standard Metadata för metadata.
* Ange det här `MediaInfo` objektet när du anropar `trackSessionStart()` API:t.

## Exempel på implementeringar

### Video

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### Ljud

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```

---
title: Lär dig hur du implementerar standardmetadata i Android
description: Lär dig hur du ställer in standardmetadata för video och annonsering som ska skickas med spårningsanrop till Android.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 1%

---

# Implementera standardmetadata på Android{#implement-standard-metadata-on-android}

## Standardmetadatakonstanter

| Konstantnamn | Beskrivning   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Konstant för att bifoga standardmetadata på `MediaObject`. |

## API-referens för metadatanycklar

* Skapa `HashMap` standardvärdepar för metadata.
   * [Metadatanycklar för video](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Tangenter för ljudmetadata](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Ange standardmetadata `HashMap` på `MediaInfo` med standardmetadatakonstanten för metadata.
* Ange det här `MediaInfo`-objektet när `trackSessionStart()`-API:t anropas.

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

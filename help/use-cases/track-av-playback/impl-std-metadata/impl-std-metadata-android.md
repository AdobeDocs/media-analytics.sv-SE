---
title: Lär dig hur du implementerar standardmetadata på Android
description: Lär dig hur du ställer in standardmetadata för video och annonsering som ska skickas med spårningsanrop på Android.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 6%

---

# Implementera standardmetadata i Android{#implement-standard-metadata-on-android}

## Standardmetadatakonstanter

| Konstantnamn | Beskrivning   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Konstant för att bifoga standardmetadata på `MediaObject`. |

## API-referens för metadatanycklar

* Skapa en `HashMap` av nyckelvärdepar för standardmetadata.
   * [Metadatanycklar för video](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Tangenter för ljudmetadata](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Ange standardmetadata `HashMap` på `MediaInfo` med standardmetadatakonstanten för metadata.
* Ange detta `MediaInfo` när objektet anropades `trackSessionStart()` API.

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

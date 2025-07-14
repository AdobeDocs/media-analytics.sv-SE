---
title: Lär dig hur du implementerar standardmetadata i Chromecast
description: Lär dig hur du ställer in standardmetadata för video och annonsering på Chromecast.
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
exl-id: 052ede4b-ea8a-4ca6-bf02-0aab22a8bcda
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 3%

---

# Implementera standardmetadata på Chromecast{#implement-standard-metadata-on-chromecast}

Instansiera ett metadataobjekt av standardtyp, fyll i önskade variabler och ange metadataobjektet i objektet Mediepulsslag. Exempel:

```js
var standardVideoMetadata = {};
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show";
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season";

mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {};
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist";
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album";

mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

Se den omfattande listan med ljud- och videometadata här: [Parametrar för ljud och video.](/help/implementation/variables/audio-video-parameters.md)

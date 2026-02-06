---
title: Lär dig hur du implementerar standardmetadata på Roku
description: Lär dig hur du ställer in standardmetadata för video och annonsering som ska skickas med spårningsanrop på Roku.
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Implementera standardmetadata på Roku{#implement-standard-metadata-on-roku}

Instansiera ett standardmetadataobjekt, fyll i de önskade variablerna och ange metadataobjektet i Media Heartbeat-objektet.

**Video:**

```
standardMetadata = {}
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show"
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season"
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata
```

**Ljud:**

```
standardMetadata = {}
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist"
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album"
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata
```

Se den omfattande listan med videometadata här: [Parametrar för ljud och video](/help/implementation/variables/audio-video-parameters.md)

---
title: Lär dig implementera standardmetadata med JavaScript 3.x
description: Lär dig hur du ställer in standardmetadata för video och annonsering som ska skickas med spårningsanrop i webbläsarappar (JS 3.x).
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 6%

---

# Implementera standardmetadata med JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Implementering

Instansiera ett kontextdataobjekt och fyll i önskade standardmetadatavariabler. Exempel:

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```

---
title: Version 1.x till 2.x API-konvertering
description: Utforska API-referenser och listor över obligatoriska och valfria API:er för spårning för version 1.x och 2.x av Media SDK.
uuid: 6e619288-c082-4cb4-8685-e90823dadf4a
exl-id: 8d06b7df-f246-49e6-aa58-91a9d6fa889a
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# Äldre API - konvertering från 1.x till 2.x {#one-x-to-two-x-conv}

## Media SDK 2.x API-referenser

* [API-referens för Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [API-referens för iOS](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [JS API-referens](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [API-referens för Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## Nödvändiga spår*-API:er:

|  VHL 1.x  | VHL 2.x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | Ej tillämpligt |
| `videoPlayerPlugin.trackSessionStart()` | [mediaHeartbeat.trackSessionStart(mediaObject, mediaCustomMetadata)](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [mediaHeartbeat.trackPlay()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [mediaHeartbeat.trackPause()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [mediaHeartbeat.trackComplete()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [mediaHeartbeat.trackSessionEnd()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | Ej tillämpligt |
| `videoPlayerPlugin.trackVideoPlayerError()` | [mediaHeartbeat.trackError()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

Alla valfria API:er för spårning, till exempel (annonser, kapitel, ändring av bithastighet, sökning och buffring), ingår nu i ett enda `trackEvent`-API. API:t [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent) tar emot en konstant parameter som representerar den typ av händelse som ska spåras:

## Valfria trackEvent-API:er:

| VHL 1.x | VHL 2.x |
|---|---|
| Returnera en giltig `AdBreakInfo` i `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakStart)` |
| Returnera null i `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakComplete)` |
| `playerPlugin.trackAdStart()` | `trackEvent(Event.AdStart, adObject, adCustomMetadata)` |
| `playerPlugin.trackAdComplete()` | `trackEvent(Event.AdComplete)` |
| Returnera null i `VideoPlayerPlugin.getAdInfo()` | `trackEvent(Event.AdSkip)` |
| `playerPlugin.trackChapterStart()` | `trackEvent(Event.ChapterStart, chapterObject, chapterCustomMetadata)` |
| `playerPlugin.trackChapterComplete()` | `trackEvent(Event.ChapterComplete)` |
| Returnera null i `VideoPlayerPlugin.getChapterInfo()` | `trackEvent(Event.ChapterSkip)` |
| `playerPlugin.trackSeekStart()` | `trackEvent(Event.SeekStart)` |
| `playerPlugin.trackSeekComplete()` | `trackEvent(Event.SeekComplete)` |
| `playerPlugin.trackBufferStart()` | `trackEvent(Event.BufferStart)` |
| `playerPlugin.trackBufferComplete()` | `trackEvent(Event.BufferComplete)` |
| `playerPlugin.trackBitrateChange()` | `trackEvent(Event.BitrateChange)` |
| `playerPlugin.trackTimedMetadata()` | `trackEvent(Event.TimedMetadataUpdate)` |

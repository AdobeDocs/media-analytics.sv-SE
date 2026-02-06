---
title: Kodjämförelse v1.x till v2.x
description: Lär dig skillnaden mellan kod i 1.x- och 2.x-versionerna av Media SDK.
uuid: 9f0a1660-2100-446d-ab75-afdf966478b3
exl-id: c2324c6a-329f-44e2-bea0-9d43ef9c6ef7
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 2%

---

# Jämför äldre kod - 1.x till 2.x {#code-comparison-x-to-x}

Alla konfigurationsparametrar och API:er för spårning konsolideras nu i klasserna `MediaHeartbeats` och `MediaHeartbeatConfig`.

**Ändringar i konfigurations-API:**

* `AdobeHeartbeatPluginConfig.sdk` - har ändrat namn till `MediaConfig.appVersion`
* `MediaHeartbeatConfig.playerName` - Nu inställt genom `MediaHeartbeatConfig` i stället för `VideoPlayerPluginDelegate`
* (Endast för JavaScript): Instansen `AppMeasurement` - skickas nu via konstruktorn `MediaHeartbeat`.

**Ändringar av konfigurationsegenskaper:**

* `sdk` - har ändrat namn till `appVersion`
* `publisher` - Borttagen; Experience Cloud Org ID används i stället som utgivare
* `quiteMode` - Borttagen

**Länkar till exempelspelare för 1.x och 2.x:**

* [1.x Exempelspelare](https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L58)
* [2.x Exempelspelare](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/2.x/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L47)

I följande avsnitt finns kodjämförelser mellan 1.x och 2.x, som omfattar initiering, Core Playback, Ad Playback, Chapter PlayPlayback och några andra händelser.

## VHL-kodjämförelse: INITIALISERING

### Objektinitiering

| 1.x API | 2.x API |
| --- | --- |
| `Heartbeat()` | `MediaHeartbeat()` |
| `VideoPlayerPlugin()` | `MediaHeartbeatConfig()` |
| `AdobeAnalyticsPlugin()` | |
| `HeartbeatPlugin()` | |

#### Initiering av plugin-program för videospelare (1.x) {#plugin-init-1.x}

```js
this._playerPlugin = new VideoPlayerPlugin( new SampleVideoPlayerPluginDelegate(this._player));
var playerPluginConfig = new VideoPlayerPluginConfig();
playerPluginConfig.debugLogging = true;

// Set up the AppMeasurement plugin
this._aaPlugin = new AdobeAnalyticsPlugin( appMeasurement, new SampleAdobeAnalyticsPluginDelegate());
var aaPluginConfig = new AdobeAnalyticsPluginConfig();
aaPluginConfig.channel = Configuration.HEARTBEAT.CHANNEL;
aaPluginConfig.debuglogging = true;
this._aaPlugin.configure(aaPluginConfig);

// Set up the AdobeHeartbeat plugin
var ahPlugin = new AdobeHeartbeatPlugin( new SampleAdobeHeartbeatPluginDelegate());
var ahPluginConfig = new AdobeHeartbeatPluginConfig( configuration.HEARTBEAT.TRACKING_SERVER, configuration.HEARTBEAT.PUBLISHER);
ahPluginConfig.ovp = configuration.HEARTBEAT.OVP;
ahPluginConfig.sdk = configuration.HEARTBEAT.SDK;
ahPluginConfig.debugLogging = true;
ahPlugin.configure(ahPluginConfig);
var plugins = [this._playerPlugin, this._aaPlugin, ahPlugin];

// Set up and configure the heartbeat library this._heartbeat = new Heartbeat(new SampleHeartbeatDelegate(), plugins);
var configData = new HeartbeatConfig();
configData.debugLogging = true;
this._heartbeat.configure(configData);
```

#### Initiering av pulsslag i media (2.x) {#mh-init-2.x}

```js
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
mediaConfig.playerName = Configuration.PLAYER.NAME;
mediaConfig.debugLogging = true;
mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL;
mediaConfig.ssl = false;
mediaConfig.ovp = Configuration.HEARTBEAT.OVP;
mediaConfig.appVersion = Configuration.HEARTBEAT.SDK;
this._mediaHeartbeat = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

### Delegater

| 1.x API | 2.x API |
| --- | --- |
| `VideoPlayerPluginDelegate()` | `MediaHeartbeatDelegate()` |
| `VideoPlayerPluginDelegate().getVideoInfo` | `MediaHeartbeatDelegate().getCurrentPlaybackTime` |
| `VideoPlayerPluginDelegate().getAdBreakInfo` | `MediaHeartbeatDelegate().getQoSObject` |
| `VideoPlayerPluginDelegate().getAdInfo` | |
| `VideoPlayerPluginDelegate().getChapterInfo` | |
| `VideoPlayerPluginDelegate().getQoSInfo` | |
| `VideoPlayerPluginDelegate().get.onError` | |
| `AdobeAnalyticsPluginDelegate()` | |

#### VideoPlayerPluginDelegate (1.x) {#player-plugin-delegate-1.x}

```js
$.extend(SampleVideoPlayerPluginDelegate.prototype, VideoPlayerPluginDelegate.prototype);

function SampleVideoPlayerPluginDelegate(player) {
    this._player = player;
}

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() {
    return this._player.getVideoInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdBreakInfo = function() {
    return this._player.getAdBreakInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() {
    return this._player.getAdInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() {
    return this._player.getChapterInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getQoSInfo = function() {
    return this._player.getQoSInfo();
};
```

#### AdobeAnalyticsPluginDelegate (1.x) {#analytics-plugin-delegate-1.x}

```js
$.extend(SampleAdobeAnalyticsPluginDelegate.prototype, AdobeAnalyticsPluginDelegate.prototype);

function SampleAdobeAnalyticsPluginDelegate() {}

SampleAdobeAnalyticsPluginDelegate.prototype.onError = function(errorInfo) {
    console.log("AdobeAnalyticsPlugin error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### HeartbeatDelegate (1.x) {#hb-delegate-1.x}

```js
$.extend(SampleHeartbeatDelegate.prototype, HeartbeatDelegate.prototype);

function SampleHeartbeatDelegate() {}

SampleHeartbeatDelegate.prototype.onError = function(errorInfo) {
    console.log("Heartbeat error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### MediaHeartbeatDelegate (2.x) {#mh-delegate-2.x}

```js
ADB.core.extend(SampleMediaHeartbeatDelegate.prototype, MediaHeartbeatDelegate.prototype);

function SampleMediaHeartbeatDelegate(player) {
    this._player = player;
}

SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() {
    return this._player.getCurrentPlaybackTime();
};

SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() {
    return this._player.getQoSInfo();
};

this._mediaHeartbeat = new MediaHeartbeat(new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

## VHL-kodjämförelse: CORE PLAYBACK

### Sessionsstart

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.trackVideoLoad()` | `MediaHeartbeat.createMediaObject()` |
| `VideoPlayerPluginDelegate.getVideoInfo()` | `MediaHeartbeat.trackSessionStart()` |

#### Sessionsstart (1.x) {#session-start-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    this._playerPlugin.trackVideoLoad();
};

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() {
    return this._player.getVideoInfo();
};

VideoPlayer.prototype.getVideoInfo = function() {
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Sessionsstart (2.x) {#session-start-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

### Standardmetadata för video

| 1.x API | 2.x API |
| --- | --- |
| `VideoMetadataKeys()` | `MediaHeartbeat.createMediaObject()` |
| `AdobeAnalyticsPlugin.setVideoMetadata()` | `MediaHeartbeat.trackSessionStart()` |

#### Standardmetadata (1.x) {#std-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');

    var contextData = {};

    // Setting Standard Video Metadata
    contextData[VideoMetadataKeys.SEASON] = "sample season";
    contextData[VideoMetadataKeys.SHOW] = "sample show";
    contextData[VideoMetadataKeys.EPISODE] = "sample episode";
    contextData[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    contextData[VideoMetadataKeys.GENRE] = "sample genre";
    contextData[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";

    // Etc.
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Standardmetadata (2.x) {#std-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');
    var contextData = {};
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);

    // Set standard Video Metadata
    var standardVideoMetadata = {};
    standardVideoMetadata[VideoMetadataKeys.SEASON] = "sample season";
    standardVideoMetadata[VideoMetadataKeys.SHOW] = "sample show";
    standardVideoMetadata[VideoMetadataKeys.EPISODE] = "sample episode";
    standardVideoMetadata[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    standardVideoMetadata[VideoMetadataKeys.GENRE] = "sample genre";
    standardVideoMetadata[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";

    // Etc.
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>I stället för att ange standardvideometadata via `AdobeAnalyticsPlugin.setVideoMetadata()`-API:t anges standardvideometadata i VHL 2.0 med MediaObject-nyckeln `MediaObject.MediaObjectKey.StandardVideoMetadata()`.

### Egna videometadata

| 1.x API | 2.x API |
| --- | --- |
| `VideoMetadataKeys()` | `MediaHeartbeat.createMediaObject()` |
| `AdobeAnalyticsPlugin.setVideoMetadata()` | `MediaHeartbeat.trackSessionStart()` |

#### Egna metadata (1.x) {#custom-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    var contextData = {
        isUserLoggedIn: "false",
        tvStation: "Sample TV station",
        programmer: "Sample programmer"
    };
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Egna metadata (2.x) {#custom-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    var contextData = {
        isUserLoggedIn: "false",
        tvStation: "Sample TV station",
        programmer: "Sample programmer"
    };
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>I stället för att ställa in anpassade videometadata via `AdobeAnalyticsPlugin.setVideoMetadata()`-API:t anges standardvideometadata i VHL 2.0 via `MediaHeartbeat.trackSessionStart()`-API:t.


### Uppspelning

| 1.x API | 2.x API |
| --- | --- |
| `VideoPlayerPlugin.trackPlay()` | `MediaHeartbeat.trackPlay()` |

#### Uppspelning (1.x) {#playback-1.x}

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() {
    console.log('Player event: SEEK_START');
    this._playerPlugin.trackSeekStart();
};
```

#### Uppspelning (2.x) {#playback-2.x}

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() {
    console.log('Player event: SEEK_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};
```

### Pausa

| 1.x API | 2.x API |
| --- | --- |
| `VideoPlayerPlugin.trackPause()` | `MediaHeartbeat.trackPausel()` |

#### Pausa (1.x) {#pause-1.x}

```js
VideoAnalyticsProvider.prototype._onPause = function() {
    console.log('Player event:X PAUSE');
    this._playerPlugin.trackPause();
};
```

#### Pausa (2.x) {#pause-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() {
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Sökning slutförd

| 1.x API | 2.x API |
| --- | --- |
| `VideoPlayerPlugin.trackSeekComplete()` | `MediaHeartbeat.`<br/>  `trackEvent(MediaHeartbeat.Event.SeekComplete)` |

#### Söker (1.x) {#seek-1.x}

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() {
    console.log('Player event: SEEK_COMPLETE');
    this._playerPlugin.trackSeekComplete();
};
```

#### Söker (2.x) {#seek-2.x}

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() {
    console.log('Player event: SEEK_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};
```

### Buffertstart

| 1.x API | 2.x API |
| --- | --- |
| `VideoPlayerPlugin.trackBufferStart()` | `MediaHeartbeat.trackEvent(`<br/>  `MediaHeartbeat.Event.BufferStart)` |

#### Buffertstart (1.x) {#buffer-start-1.x}

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() {
    console.log('Player event: BUFFER_START');
    this._playerPlugin.trackBufferStart();
};
```

#### Buffertstart (2.x) {#buffer-start-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() {
    console.log('Player event: BUFFER_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};
```

### Bufferten är klar

| 1.x API | 2.x API |
| --- | --- |
| `VideoPlayerPlugin.trackBufferComplete()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.BufferComplete)` |

#### Bufferten är klar (1.x) {#buffer-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() {
    console.log('Player event: BUFFER_COMPLETE');
    this._playerPlugin.trackBufferComplete();
};
```

#### Bufferten är klar (2.x) {#buffer-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() {
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Uppspelningen är klar

| 1.x API | 2.x API |
| --- | --- |
| `VideoPlayerPlugin.trackComplete()` | `MediaHeartbeat.trackComplete()` |

#### Uppspelningen är klar (1.x) {#playback-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onComplete = function() {
    console.log('Player event: COMPLETE');
    this._playerPlugin.trackComplete(function() {
        console.log( "The completion of the content has been tracked.");
    });
};
```

#### Uppspelningen är klar (2.x) {#playback-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onComplete = function() {
    console.log('Player event: COMPLETE');
    this._mediaHeartbeat.trackComplete();
};
```

## VHL-kodjämförelse: AD PLAYBACK

### Annonsstart

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackAdStart()` | `MediaHeartbeat.createAdBreakObject()` |
| `VideoPlayerPluginDelegate.getAdBreakInfo()` | `MediaHeartbeat.createAdObject()` |
| `VideoPlayerPluginDelegate.getAdInfo()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdBreakStart)` |
| | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdStart)` |

#### Ad Start (1.x) {#ad-start-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    this._playerPlugin.trackAdStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() {
    return this._player.getAdInfo();
};
```

#### Ad Start (2.x) {#ad-start-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var adContextData = {};

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

### Standard-annonsmetadata

| 1.x API | 2.x API |
| --- | --- |
| `AdMetadataKeys()` | `MediaHeartbeat.createAdObject()` |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.trackAdStart()` |

#### Standard Ad Metadata (1.x) {#ad-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var contextData = {};

    // setting Standard Ad Metadata
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Standard Ad Metadata (2.x) {#ad-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var adContextData = { };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);

    // Set standard Ad Metadata
    var standardAdMetadata = {};
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
    adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>I stället för att ställa in standardmetadata för annonsering via `AdobeAnalyticsPlugin.setVideoMetadata()`-API:t anges standardmetadata i VHL 2.0 via `AdMetadata` key `MediaObject.MediaObjectKey.StandardVideoMetadata`

### Anpassade annonseringsmetadata

| 1.x API | 2.x API |
| --- | --- |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.createAdObject()` |
| | `MediaHeartbeat.trackAdStart()` |

#### Anpassade annonseringsmetadata (1.x) {#custom-ad-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var contextData = {};

    // Setting Standard Ad Metadata
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Anpassade annonseringsmetadata (2.x) {#custom-ad-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var adContextData = {
        affiliate: "Sample affiliate",
        campaign: "Sample ad campaign"
    };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>I stället för att ställa in anpassade annonseringsmetadata via `AdobeAnalyticsPlugin.setVideoMetadata`-API:t anges standardprogrammeringsmetadata i VHL 2.0 via `MediaHeartbeat.trackAdStart()`-API:t.

### Ad Hoppa över

| 1.x API | 2.x API |
| --- | --- |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.createAdObject()` |
| | `MediaHeartbeat.trackAdStart()` |

#### Annonsväxling (1.x) {#ad-skip-1.x}

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() {
    return this._player.getAdInfo();
};
```

#### Annonsväxling (2.x) {#ad-skip-2.x}

```js
VideoAnalyticsProvider.prototype._onAdSkip = function() {
    console.log('Player event: AD_SKIP');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
};
```

>[!NOTE]
>I API:er för VHL 1.5.X måste `getAdinfo()` och `getAdBreakInfo()` returnera null om spelaren är utanför annonsbrytningsgränserna.

### Ad Complete

| 1.x API | 2.x API |
| --- | --- |
| `VideoPlayerPlugin.trackAdComplete()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdComplete)` |
| | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdBreakComplete)` |

#### Ad Complete (1.x) {#ad-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() {
    console.log('Player event: AD_COMPLETE');
    this._playerPlugin.trackAdComplete();
};
```

#### Ad Complete (2.x) {#ad-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() {
    console.log('Player event: AD_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
};
```

## Jämförelse av VHL-kod: KAPITEL PLAYBACK

### Kapitelstart

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.getChapterInfo()` | `MediaHeartbeat.createChapterObject` |
| `VideoPlayerPlugin.trackChapterStart()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterStart)` |

#### Kapitelstart (1.x) {#chap-start-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() {
    console.log('Player event: CHAPTER_START');
    this._playerPlugin.trackChapterStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() {
    return this._player.getChapterInfo();
};
```

#### Kapitelstart (2.x) {#chap-start-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() {
    console.log('Player event: CHAPTER_START');
    var chapterContextData = { };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Hoppa över kapitel

| 1.x API | 2.x API |
| --- | --- |
| `VideoPlayerPluginDelegate.getChapterInfo()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterSkip)` |

#### Hoppa över kapitel (1.x) {#chap-skip-1.x}

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() {
    return this._player.getChapterInfo();
};
```

>[!NOTE]
>I VHL 1.5.X-API:er måste `getChapterinfo()` returnera null om spelaren är utanför kapitelgränserna.

#### Hoppa över kapitel (2.x) {#chap-skip-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterSkip = function() {
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```

### Egna metadata för kapitel

| 1.x API | 2.x API |
| --- | --- |
| `VideoPlayerPlugin.trackChapterStart()` | `MediaHeartbeat.createChapterObject()` |
| `AdobeAnalyticsPlugin.setChapterMetadata()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterStart)` |

#### Egna metadata för kapitel (1.x) {#chap-cust-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() {
    console.log('Player event: CHAPTER_START');
    this._aaPlugin.setChapterMetadata({
        segmentType: "Sample segment type"
    });
    this._playerPlugin.trackChapterStart();
};
```

#### Egna metadata för kapitel (2.x) {#chap-cust-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() {
    console.log('Player event: CHAPTER_START');
    var chapterContextData = {
        segmentType: "Sample segment type"
    };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Kapitel slutfört

| 1.x API | 2.x API |
| --- | --- |
| `trackChapterComplete()` | `trackEvent(MediaHeartbeat.Event.ChapterComplete)` |

#### Fullständigt kapitel (1.x) {#chap-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() {
    console.log('Player event: CHAPTER_COMPLETE');
    this._playerPlugin.trackChapterComplete();
};
```

#### Kapitel fullständigt (2.x) {#chap-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() {
    console.log('Player event: CHAPTER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};
```

## VHL-kodjämförelse: ANDRA HÄNDELSER

### Bithastighetsändring

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBitrateChange()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.BitrateChange)` |

#### Ändra bithastighet (1.x) {#bitrate-chg-1.x}

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() {
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosInfo to return the updated bitrate
    this._playerPlugin.trackBitrateChange();
};
```

#### Ändra bithastighet (2.x) {#bitrate-chg-2.x}

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() {
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosObject to return the updated bitrate
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange);
};
```

### Återuppta video

| 1.x API | 2.x API |
| --- | --- |
| `VideoInfo.resumed()` | `MediaObject()` |
| `VideoPlayerPluginDelegate.getVideoInfo()` | `MediaHeartbeat.trackSessionStart()` |
| `VideoPlayerPlugin.trackVideoLoad()` | |

#### Återuppta video (1.x) {#video-resume-1.x}

```js
this._videoInfo.resumed=true;
```

```js
VideoPlayer.prototype.getVideoInfo = function() {
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Återuppta video (2.x) {#video-resume-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.playerName, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed, true);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

Mer information om att spåra video med 2.x finns i [Spåra videouppspelning i kärna](/help/use-cases/track-av-playback/track-core-overview.md).

---
title: Förklaring av metadata för Chromecast
description: Lär dig hur du ställer in standardmetadata för video och annonsering som ska skickas med spårningsanrop på Chromecast.
uuid: c446ad41-51b8-46d6-9bc1-abfae866023f
exl-id: ccc717ae-d846-4349-8282-5e3511ddeb9b
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# Chromecast-metadatanycklar{#chromecast-metadata-keys}

Standardmetadata för video och annonser kan anges för medie- respektive annonsinformation. Använd konstanterna för video-/annonsmetadata för att ange den ordlista som innehåller standardmetadata för info-objektet innan du anropar spårnings-API:erna. Se tabellerna nedan för hela listan med standardmetadatakonstanter, följt av exempel.

## Metadatakonstanter {#video-metadata-constants}

| Metadatanamn | Kontextdatanyckel | Konstantnamn |
| --- | --- | --- |
| Visa | `a.media.show` | `ADBMobile.media.VideoMetadataKeys.SHOW` |
| Säsong | `a.media.season` | `ADBMobile.media.VideoMetadataKeys.SEASON` |
| Episod | `a.media.episode` | `ADBMobile.media.VideoMetadataKeys.EPISODE` |
| Tillgång | `a.media.asset` | `ADBMobile.media.VideoMetadataKeys.TMS_ID` |
| Genre | `a.media.genre` | `ADBMobile.media.VideoMetadataKeys.GENRE` |
| Första AIR-datum | `a.media.airDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE` |
| Första datum för digital AIR | `a.media.digitalDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE` |
| Klassificering | `a.media.rating` | `ADBMobile.media.VideoMetadataKeys.RATING` |
| Originator | `a.media.originator` | `ADBMobile.media.VideoMetadataKeys.ORIGINATOR` |
| Nätverk | `a.media.network` | `ADBMobile.media.VideoMetadataKeys.NETWORK` |
| Visa typ | `a.media.type` | `ADBMobile.media.VideoMetadataKeys.SHOW_TYPE` |
| Ad Load | `a.media.adLoad` | `ADBMobile.media.VideoMetadataKeys.AD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `ADBMobile.media.VideoMetadataKeys.MVPD` |
| Auktoriserad | `a.media.pass.auth` | `ADBMobile.media.VideoMetadataKeys.AUTHORIZED` |
| Dag - del | `a.media.dayPart` | `ADBMobile.media.VideoMetadataKeys.DAY_PART` |
| Feed | `a.media.feed` | `ADBMobile.media.VideoMetadataKeys.FEED` |
| Strömformat | `a.media.format` | `ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT` |

## Lägg till metadatakonstanter {#ad-metadata-constants}

| Metadatanamn | Kontextdatanyckel | Konstantnamn |
| --- | --- | --- |
| Annonsör | `a.media.ad.advertiser` | `ADBMobile.media.AdMetadataKeys.ADVERTISER` |
| Kampanj-ID | `a.media.ad.campaign` | `ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID` |
| CREATIVE ID | `a.media.ad.creative` | `ADBMobile.media.AdMetadataKeys.CREATIVE_ID` |
| Placement-ID | `a.media.ad.placement` | `ADBMobile.media.AdMetadataKeys.PLACEMENT_ID` |
| Plats-ID | `a.media.ad.site` | `ADBMobile.media.AdMetadataKeys.SITE_ID` |
| CREATIVE URL | `a.media.ad.creativeURL` | `ADBMobile.media.AdMetadataKeys.CREATIVE_URL` |

## Exempelimplementeringar för Chromecast {#sample-implementations-for-chromecast}

### Video

```js
// setting Standard Video Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["videotype"] = "episode"; 
 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "sample show"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "sample season"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.EPISODE] = "sample episode"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.TMS_ID] = "sample tms_id"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "sample genre"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "sample first_air_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "sample first_digital_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.RATING] = "sample rating"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.ORIGINATOR] = "sample originator"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.NETWORK] = "sample network"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "sample show type"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "sample ad load"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "sample mvpd"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "sample authorized"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.DAY_PART] = "sample day_part"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FEED] = "sample feed"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT] = "sample format"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### Ljud

```js
// setting Standard Audio Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["audiotype"] = "podcast"; 
var standardAudioMetadata = {}; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ARTIST] = "sample artist"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ALBUM] = "sample album" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.LABEL] = "sample label"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.AUTHOR] = "sample author" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.STATION] = "sample station " ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.PUBLISHER] = "sample publisher"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType, content.mediaType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudiooMetadata] = standardAudiooMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### Annonser

```js
// setting Standard Ad Metadata as context data on ad start event 
var standardAdMetadata = {}; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = "sample campaign"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.ADVERTISER] = "sample advertiser" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "sample creativeid"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.PLACEMENT_ID] = "sample placement id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.SITE_ID] = "sample site id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "sample creative url"; 
 
var adObject = ADBMobile.media.createAdObject(ad.name, ad.id, ad.position, ad.length); 
adObject[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardVideoMetadata; 
 
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, this._player.getAdInfo(), adContextData);
```

---
title: Förklaring av Roku-metadatanycklar
description: Lär dig mer om de tillgängliga Roku-metadatanycklarna och visa hela listan med standardmetadatakonstanter.
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
exl-id: 687dbaa5-4723-4b3f-ab1e-4d5bf447cddf
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Roku-metadatanycklar{#roku-metadata-keys}

Standardmetadata för video, ljud och annonser kan anges för medie- respektive annonsinformationsobjekt. Använd konstanterna för video-/annonsmetadata för att ange den ordlista som innehåller standardmetadata för info-objektet innan du anropar spårnings-API:erna. Se tabellerna nedan för hela listan med standardmetadatakonstanter, följt av exempel.

## Metadatakonstanter för video {#video-metadata-constants}

| Metadatanamn | Kontextdatanyckel | Konstantnamn |
| --- | --- | --- |
| Visa | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Säsong | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Episod | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Tillgång | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Genre | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| Första AIR-datum | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| Första datum för digital AIR | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Klassificering | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Originator | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Nätverk | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Visa typ | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Ad Load | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Auktoriserad | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Dag - del | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Feed | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Strömformat | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Konstanter för ljudmetadata {#audio-metadata-constants}

| Metadatanamn | Kontextdatanyckel | Konstantnamn |
| --- | --- | --- |
| Konstnär | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Album | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Etikett | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Upphovsman | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Station | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Utgivare | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Lägg till metadatakonstanter {#ad-metadata-constants}

| Metadatanamn | Kontextdatanyckel | Konstantnamn |
| --- | --- | --- |
| Annonsör | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| Kampanj-ID | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| CREATIVE ID | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| Placement-ID | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| Plats-ID | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| CREATIVE URL | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## Konstanter {#constants}

Du kan använda följande konstanter för att spåra mediahändelser:

### Andra konstanter

| Konstant | Beskrivning   |
|---|---|
| `ERROR_SOURCE_PLAYER` | Konstant för att felkällan ska spelas upp |

### MediaObjectKey-konstanter (används som nycklar i MediaObject-instanser)

| Konstant | Beskrivning   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Konstant för att ange metadata för `MediaInfo` `trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Konstant för att ange annonsmetadata för `EventData` `trackEvent` |
| `MEDIA_RESUMED` | Konstant för sändning av videoåterupptagen hjärtfrekvens. Om du vill återuppta videospårning av innehåll som tidigare stoppats måste du ange egenskapen `MEDIA_RESUMED` för objektet `mediaInfo` när du anropar `mediaTrackLoad`. (`MEDIA_RESUMED` är inte en händelse som du kan spåra med `mediaTrackEvent` API.) `MEDIA_RESUMED` bör anges till true när ett program vill fortsätta spåra innehåll som en användare har slutat titta på men nu vill återuppta tittandet. <br/><br/>Anta till exempel att en användare tittar på 30 % av innehållet och sedan stänger programmet. Detta leder till att sessionen avslutas. Om samma användare senare återgår till samma innehåll, och programmet tillåter användaren att återuppta från den punkt där han/hon slutade, bör programmet ange `MEDIA_RESUMED` till &quot;true&quot; när API:t `mediaTrackLoad` anropas. Resultatet är att dessa två olika mediesessioner för samma videoinnehåll kan länkas tillsammans. Följande är implementeringsexemplet: <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>Detta skapar en ny session för videon, men det gör även att SDK skickar en pulsslagsförfrågan med händelsetypen &quot;resume&quot;, som kan användas för rapportering för att knyta ihop två olika mediesessioner. |

### Konstanter för innehållstyp

| Konstant | Beskrivning   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | Konstant för strömningstyp LIVE |
| `MEDIA_STREAM_TYPE_VOD` | Konstant för strömtyp VOD |

### Händelsetypskonstanter (används för trackEvent-anropet)

| Konstant | Beskrivning   |
|---|---|
| `MEDIA_BUFFER_START` | Händelsetyp för buffertstart |
| `MEDIA_BUFFER_COMPLETE` | Händelsetyp för slutförd buffert |
| `MEDIA_SEEK_START` | Händelsetyp för sökstart |
| `MEDIA_SEEK_COMPLETE` | Händelsetyp för slutförd sökning |
| `MEDIA_BITRATE_CHANGE` | Händelsetyp för bithastighetsändring |
| `MEDIA_CHAPTER_START` | Händelsetyp för kapitelstart |
| `MEDIA_CHAPTER_COMPLETE` | Händelsetyp för slutfört kapitel |
| `MEDIA_CHAPTER_SKIP` | Händelsetyp för annonsstart |
| `MEDIA_AD_BREAK_START` | Händelsetyp för annonsstart |
| `MEDIA_AD_BREAK_COMPLETE` | Händelsetyp för AdBreak Complete |
| `MEDIA_AD_BREAK_SKIP` | Händelsetyp för AdBreak Hoppa över |
| `MEDIA_AD_START` | Händelsetyp för annonsstart |
| `MEDIA_AD_COMPLETE` | Händelsetyp för Ad Complete |
| `MEDIA_AD_SKIP` | Händelsetyp för Ad Hoppa över |

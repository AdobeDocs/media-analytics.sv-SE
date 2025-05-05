---
title: Information om provsamtal
description: Utforska de samtal du måste ringa för att validera implementeringen.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 8%

---

# Information om testsamtal{#test-call-details}

## Starta mediespelaren {#start-the-media-player}

### Adobe Analytics (AppMeasurement) Starta samtal {#aa-start-call}

| Parameter |  Värde (exempel)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Avsnittstitel |
| _&#x200B;**`a.media.name`**&#x200B;_ | _&#x200B;**123456**&#x200B;_ |
| _&#x200B;**`a.media.length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `a.media.playerName` | HTML5 |
| _&#x200B;**`a.media.view`**&#x200B;_ | _&#x200B;**true**&#x200B;_ |
| `a.contentType` | vod |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**Anpassade metadatafält**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**Standardmetadatafält**&#x200B;_ |

**Anteckningar:**

* Ytterligare kontextdatavariabler ska finnas och innehålla metadata. Se metadatainformation nedan.
* Längden för linjära strömmar bör anges till den bästa uppskattningen för det aktuella programmet.

### Standardmetadata i Adobe Analytics (AppMeasurement) Starta samtal {#std-metadata-aa}

| Parameter |  Värde (exempel)  |
|---|---|
| `a.media.show` | Visa titel |
| `a.media.season` | 6 |
| `a.media.episode` | Avsnittstitel |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | komedi |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | produktionsenhet |
| `a.media.network` | nätverk |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | olåst |
| `a.media.feed` | ingen feed |
| `a.media.stream_format` | 0 |

### Anpassade metadata i Adobe Analytics (AppMeasurement) Starta samtal {#custom-metadata-aa}

| Parameter |  Värde (exempel)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Starta samtal med Media Analytics (hjärtslag) {#ma-start-call}

| Parameter |  Värde (exempel)  |
|---|---|
| `s:event:type` | start |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**0**&#x200B;_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Avsnittstitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**Anpassade metadatafält**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**Standardmetadatafält**&#x200B;_ |

**Anteckningar:**

* Ytterligare kontextdatavariabler ska finnas och innehålla metadata. Se metadatainformation nedan.
* Spelhuvudspositionen för linjära direktuppspelningar vid videostart ska anges till sekunder som gått sedan början av det aktuella programmet, inte 0.

### Standardmetadata i Media Analytics (hjärtslag) Starta samtalet {#std-metadata-ma}

| Parameter |  Värde (exempel)  |
|---|---|
| `s:meta:a.media.show` | Visa |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Avsnittstitel |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | komedi |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | produktionsenhet |
| `s:meta:a.media.network` | nätverk |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | olåst |
| `s:meta:a.media.feed` | ingen feed |
| `s:meta:a.media.stream_format` | 0 |

### Anpassade metadata i Media Analytics (hjärtslag) Starta samtal {#custom-metadata-ma}

| Parameter |  Värde (exempel)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (hjärtslag) Adobe Analytics Start Call {#ma-aa-start}

| Parameter |  Värde (exempel)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Avsnittstitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Anteckningar:**

* Detta anrop anger att Media SDK har begärt att ett Adobe Analytics `pev2=ms_s`-anrop ska skickas till Adobe Analytics-servern (AppMeasurement).
* Anropet innehåller inte anpassade metadata.

## Visa och spela upp {#view-ad-playback}

### Adobe Analytics (AppMeasurement) Ad Start-samtal {#aa-ad-start-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _&#x200B;**`pev2`**&#x200B;_ | _&#x200B;**msa_s**&#x200B;_ |
| `a.media.name` | 123456 |
| _&#x200B;**`a.media.ad.name`**&#x200B;_ | _&#x200B;**9378**&#x200B;_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _&#x200B;**`a.media.ad.length`**&#x200B;_ | _&#x200B;**15**&#x200B;_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0,0 |
| _&#x200B;**`a.media.ad.view`**&#x200B;_ | _&#x200B;**Sant**&#x200B;_ |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**Metadatafält**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**Standardmetadatafält**&#x200B;_ |

**Anteckningar:**

* Ytterligare kontextdatavariabler ska finnas och innehålla metadata. Se metadatainformation nedan.
* Annonslängden kan anges till -1 om den inte är tillgänglig vid annonsstart.

### Standardmetadata i Adobe Analytics (AppMeasurement) Ad Start-anrop {#std-metadata-aa-ad-start}

| Parameter |  Värde (exempel)  |
|---|---|
| `a.media.show` | Visa titel |
| `a.media.season` | 6 |
| `a.media.episode` | Avsnittstitel |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | komedi |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | produktionsenhet |
| `a.media.network` | nätverk |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | olåst |
| `a.media.feed` | ingen feed |
| `a.media.stream_format` | 0 |

### Anpassade metadata i Adobe Analytics (AppMeasurement) Ad Start-anrop {#custom-metadata-aa-ad-start}

| Parameter |  Värde (exempel)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics (hjärtslag) och starta samtal {#ma-ad-start-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _&#x200B;**`l:asset:length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**Anpassade metadatafält**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**Standardmetadatafält**&#x200B;_ |

**Anteckningar:**

* Ytterligare kontextdatavariabler ska finnas och innehålla metadata. Se metadatainformation nedan.
* Annonslängden kan anges till -1 om den inte är tillgänglig vid annonsstart.

### Standardmetadata i Media Analytics (hjärtslag) och Starta samtal {#std-metadata-ma-ad-start}

| Parameter |  Värde (exempel)  |
|---|---|
| `s:meta:a.media.show` | Visa |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Avsnittstitel |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | komedi |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | produktionsenhet |
| `s:meta:a.media.network` | nätverk |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | olåst |
| `s:meta:a.media.feed` | ingen feed |
| `s:meta:a.media.stream_format` | 0 |

### Anpassade metadata i Media Analytics (hjärtslag) och Starta samtal {#custom-metadata-ma-ad-start}

| Parameter |  Värde (exempel)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (hjärtslag) - Adobe Analytics Ad Start-samtal {#ma-aa-ad-start-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_ad_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Anrop till Media Analytics (hjärtslag) och Play {#ma-ad-play-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**play**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

### Media Analytics (hjärtslag) och paus-samtal {#ma-ad-pause-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**paus**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

### Media Analytics (hjärtslag) Adobe Analytics Ad Complete call {#ma-aa-ad-complete-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**complete**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

## Spela upp huvudinnehåll {#play-main-content}

### Media Analytics (hjärtslag) Play-samtal {#ma-play-call}

| Parameter |  Värde (exempel)  |
|---|---|
| `s:event:type` | play |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| _&#x200B;**`l:event:duration`**&#x200B;_ | _&#x200B;**10189**&#x200B;_ |
| `s:asset:name` | Avsnittstitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Anteckningar:**

* Spelhuvudets position ska ökas med 10 sekunder för varje uppspelningsanrop.
* Värdet `l:event:duration` representerar antalet millisekunder sedan det senaste spårningsanropet och bör vara ungefär lika stort för varje 10-sekundersanrop.

## Pausa huvudinnehåll {#pause-main-content}

### Media Analytics (hjärtslag) Pausa samtal {#ma-pause-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**paus**&#x200B;_ |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Avsnittstitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

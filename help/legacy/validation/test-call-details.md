---
title: Information om provsamtal
description: Utforska de samtal du måste ringa för att validera implementeringen.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 11%

---

# Information om testsamtal{#test-call-details}

## Starta mediespelaren {#start-the-media-player}

### Starta Adobe Analytics (AppMeasurement) {#aa-start-call}

| Parameter |  Värde (exempel)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Avsnittstitel |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**sant**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**Anpassade metadatafält**_ |
| _**`a.media.[value]`**_ | _**Standardmetadatafält**_ |

**Anteckningar:**

* Ytterligare kontextdatavariabler ska finnas och innehålla metadata. Se metadatainformation nedan.
* Längden för linjära strömmar bör anges till den bästa uppskattningen för det aktuella programmet.

### Standardmetadata i Adobe Analytics (AppMeasurement) Starta anrop {#std-metadata-aa}

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

### Anpassade metadata i Adobe Analytics (AppMeasurement) - starta anrop {#custom-metadata-aa}

| Parameter |  Värde (exempel)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Starta samtal med Media Analytics (hjärtslag) {#ma-start-call}

| Parameter |  Värde (exempel)  |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Avsnittstitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**Anpassade metadatafält**_ |
| _**`s:meta:a.media.[value]`**_ | _**Standardmetadatafält**_ |

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
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Avsnittstitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Anteckningar:**

* Detta anrop anger att Media SDK har begärt att en Adobe Analytics `pev2=ms_s` anrop skickas till Adobe Analytics-servern (AppMeasurement).
* Anropet innehåller inte anpassade metadata.

## Visa och spela upp {#view-ad-playback}

### Adobe Analytics (AppMeasurement) Ad Start-anrop {#aa-ad-start-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0,0 |
| _**`a.media.ad.view`**_ | _**True**_ |
| _**`custom.[value]`**_ | _**Metadatafält**_ |
| _**`a.media.[value]`**_ | _**Standardmetadatafält**_ |

**Anteckningar:**

* Ytterligare kontextdatavariabler ska finnas och innehålla metadata. Se metadatainformation nedan.
* Annonslängden kan anges till -1 om den inte är tillgänglig vid annonsstart.

### Standardmetadata i Adobe Analytics (AppMeasurement) och Starta anrop {#std-metadata-aa-ad-start}

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

### Anpassade metadata i Adobe Analytics (AppMeasurement) och starta anrop {#custom-metadata-aa-ad-start}

| Parameter |  Värde (exempel)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics (hjärtslag) och starta samtal {#ma-ad-start-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**Anpassade metadatafält**_ |
| _**`s:meta:a.media.[value]`**_ | _**Standardmetadatafält**_ |

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
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Anrop till Media Analytics (hjärtslag) och Play {#ma-ad-play-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics (hjärtslag) och paus-samtal {#ma-ad-pause-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _**`s:event:type`**_ | _**paus**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics (hjärtslag) Adobe Analytics Ad Complete call {#ma-aa-ad-complete-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## Spela upp huvudinnehåll {#play-main-content}

### Media Analytics (hjärtslag) Play-samtal {#ma-play-call}

| Parameter |  Värde (exempel)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Avsnittstitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Anteckningar:**

* Spelhuvudets position ska ökas med 10 sekunder för varje uppspelningsanrop.
* The `l:event:duration` värdet representerar antalet millisekunder sedan det senaste spårningsanropet och bör vara ungefär lika stort för varje 10-sekundersanrop.

## Pausa huvudinnehåll {#pause-main-content}

### Media Analytics (hjärtslag) Pausa samtal {#ma-pause-call}

| Parameter |  Värde (exempel)  |
|---|---|
| _**`s:event:type`**_ | _**paus**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Avsnittstitel |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

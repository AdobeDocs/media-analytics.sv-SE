---
title: Migrera målgrupper till nya Adobe Analytics för Streaming Media-datatyp
description: Lär dig hur du migrerar målgrupper till den nya datatypen Adobe Analytics for Streaming Media
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 3056a384535b3f5f2a9bc2d950bd5ee3410ec0a5
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 0%

---

# Parametermappning för Media Analytics för Adobe Experience Platform och Customer Journey Analytics

Det här dokumentet innehåller en omfattande lista över alla Media Analytics-parametrar som används i Adobe Experience Platform och Customer Journey Analytics. Den är avsedd att stödja integrering av data som importeras från Adobe Analytics till plattformen via [Analytics Source Connector](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/analytics) eller [Analytics Source Connector for Classifications](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/classifications) och mappa varje parameter till motsvarande XDM-fältsökväg.

## Media Analytics-reserverade variabler

För alla variabler som är reserverade för Media Analytics finns data som importerats från Adobe Analytics till AEP fram till (och inklusive) maj 2025 under den aktuella sökvägen till XDM-fält som anges i tabellerna nedan.

I takt med att Media Analytics- och ADC-teamen för närvarande arbetar mot en fullständig migrering till &#39;Reporting XDM Field Path&#39;, delas en officiell kommunikation när migreringen är klar och &#39;Reporting XDM Field Path&#39; är tillgänglig för användning.

## Parametrar för direktuppspelande media

| Fältnamn | Aktuell XDM-fältsökväg (inaktuell) | Sökväg till XDM-fält | Datatyp | Härlett fält | Anteckningar |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| Strömtyp | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | Dimension | Strömtyp |                                                                       |
| Innehålls-ID | media.mediaTimed.primaryAssetReference._id | mediaReporting.sessionDetails.name | Dimension | Innehålls-ID |                                                                       |
| Innehållslängd | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | Dimension | Innehållslängd |                                                                       |
| Innehållstyp | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | Dimension | Innehållstyp |                                                                       |
| ID för mediesession | media.mediaTimed.primaryAssetViewDetails._id | mediaReporting.sessionDetails.ID | Dimension | ID för mediesession |                                                                       |
| Innehållsspelarens namn | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | Dimension | Innehållsspelarens namn |                                                                       |
| Innehållskanal | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | Dimension | Innehållskanal |                                                                       |
| Innehållssegment | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | Dimension | Innehållssegment |                                                                       |
| Innehållsnamn | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | Dimension | Innehållsnamn |                                                                       |
| Videosökväg | *Används inte i AEP/CJA* |                                                   |           |                   | Adobe Analytics-specifik egenskap |
| Visa | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | Dimension | Visa |                                                                       |
| Säsong | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | Dimension | Säsong |                                                                       |
| Episod | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | Dimension | Episod |                                                                       |
| Genre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | Dimension | stöds inte | Använd fältet MediaReporting |
| Nätverk | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | Dimension | Nätverk |                                                                       |
| Visa typ | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | Dimension | Visa typ |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | Dimension | MVPD |                                                                       |
| Auktoriserad | Stöds inte | mediaReporting.sessionDetails.authorized | Dimension | Auktoriserad |                                                                       |
| Dag - del | Stöds inte | mediaReporting.sessionDetails.dayPart | Dimension | Dag - del |                                                                       |
| Medieflödestyp | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | Dimension | Medieflödestyp |                                                                       |
| Konstnär | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | Dimension | Konstnär |                                                                       |
| Album | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | Dimension | Album |                                                                       |
| Etikett | Stöds inte | mediaReporting.sessionDetails.label | Dimension | Etikett |                                                                       |
| Upphovsman | Stöds inte | mediaReporting.sessionDetails.author | Dimension | Upphovsman |                                                                       |
| Station | media.mediaTimed.primaryAssetReference._id3.Ljud._id3.TRSN | mediaReporting.sessionDetails.station | Dimension | Station |                                                                       |
| Utgivare | media.mediaTimed.primaryAssetReference._id3.Ljud._id3.TPUB | mediaReporting.sessionDetails.publisher | Dimension | Utgivare |                                                                       |
| Media börjar | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | Mått | Media börjar |                                                                       |
| Innehållet börjar | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | Mått | Innehållet börjar |                                                                       |
| Innehållet har slutförts | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | Mått | Innehållet har slutförts |                                                                       |
| Innehållstid | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | Mått | Innehållstid |                                                                       |
| Medietid tillagd | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | Mått | Medietid tillagd |                                                                       |
| Unik uppspelningstid | Stöds inte | mediaReporting.sessionDetails.uniqueTimePlayed | Mått | Unik uppspelningstid |                                                                       |
| 10 % förloppsmärke | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | Mått | 10 % förloppsmärke |                                                                       |
| 25 % förloppsmärke | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | Mått | 25 % förloppsmärke |                                                                       |
| Förloppsmärke för 50 % | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | Mått | Förloppsmärke för 50 % |                                                                       |
| 75 % förloppsmärke | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | Mått | 75 % förloppsmärke |                                                                       |
| 95 % förloppsmärke | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | Mått | 95 % förloppsmärke |                                                                       |
| Genomsnittlig målgrupp i minuter | Stöds inte | mediaReporting.sessionDetails.averageMinuteAudience | Mått | Genomsnittlig målgrupp i minuter |                                                                  |
| Sekunder sedan senaste samtal | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | Mått | Sekunder sedan senaste samtal |                                                              |
| Pausade påverkade strömmar | Stöds inte | mediaReporting.sessionDetails.hasPauseImpactedStreams | Mått | Pausade påverkade strömmar | vi täcker mediaTimed genom att beräkna det här värdet från andra händelser |
| Pausa händelser | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | Mått | Pausa händelser |                                                                       |
| Total pausvaraktighet | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | Mått | Total pausvaraktighet |                                                                       |
| Återuppta innehåll | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | Mått | Återuppta innehåll |                                                                       |
| Vyer för innehållssegment | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | Mått | Vyer för innehållssegment |                                                                     |

{style="table-layout:auto"}

## Uppdatering av parametrar för spelartillstånd

| Fältnamn | Aktuell XDM-fältsökväg (inaktuell) | Sökväg till XDM-fält | Datatyp | Härlett fält | Anteckningar |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| Strömmar som påverkas av spelartillstånd | Stöds inte | mediaReporting.states.isSet | Mått | stöds inte | använd mediaReporting-fält |
| Antal spelarlägen | Stöds inte | mediaReporting.states.count | Mått | stöds inte | använd mediaReporting-fält |
| Spelarlägen, total varaktighet | Stöds inte | mediaReporting.states.time | Mått | stöds inte | använd mediaReporting-fält |
| Spelarlägesnamn | Stöds inte | mediaReporting.states.name | Dimension | stöds inte | använd mediaReporting-fält |

{style="table-layout:auto"}

## Kapitelparametrar

| Fältnamn | Aktuell XDM-fältsökväg (inaktuell) | Sökväg till XDM-fält | Datatyp | Härlett fält | Anteckningar |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| Kapitel | media.mediaTimed.mediaChapter.chapterAssetReference._id | mediaReporting.chapterDetails.ID | Dimension | Kapitel |           |
| Kapitelstart | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | Mått | Kapitelstart |           |
| Kapitel slutfört | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | Mått | Kapitel slutfört |          |
| Kapiteltid spenderad | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | Mått | Kapiteltid spenderad |        |

{style="table-layout:auto"}

## Annonsparametrar

| Fältnamn | Aktuell XDM-fältsökväg (inaktuell) | Sökväg till XDM-fält | Datatyp | Härlett fält | Anteckningar |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| Annons-ID | advertising.adAssetReference._id | mediaReporting.advertisingDetails.name | Dimension | Annons-ID |           |
| Lägg till i rutposition | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | Dimension | Lägg till i rutposition |     |
| Annonslängd | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | Mått | Annonslängd |           |
| Namn på annonsspelaren | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | Dimension | Namn på annonsspelaren |           |
| ID för annonsbrytning | advertising.adAssetViewDetails.adBreak._id | mediaReporting.advertisingPodDetails.ID | Dimension | ID för annonsbrytning |           |
| Annonsnamn | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | Dimension | Annonsnamn |           |
| Annonsör | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | Dimension | Annonsör |           |
| Kampanj-ID | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | Dimension | Kampanj-ID |           |
| Annonsstart | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | Mått | Annonsstart |           |
| Ad Complete | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | Mått | Ad Complete |           |
| Annonstid | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | Mått | Annonstid |           |

{style="table-layout:auto"}

## Kvalitetsparametrar

| Fältnamn | Aktuell XDM-fältsökväg (inaktuell) | Sökväg till XDM-fält | Datatyp | Härledda fält | Anteckningar |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| Genomsnittlig bithastighet | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage | Båda | Genomsnittlig bithastighet |           |
| Tid att starta | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart | Båda | Tid att starta |           |
| Släppta bildrutor | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames | Båda | Släppta bildrutor |           |
| Bufferthändelser | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount | Båda | Bufferthändelser |           |
| Buffertvaraktighet totalt | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime | Båda | Buffertvaraktighet totalt |     |
| Bithastighetsändringar | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount | Båda | Bithastighetsändringar |         |
| Fel-/felhändelser | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount | Båda | Fel-/felhändelser |  |
| Fel-ID för SDK Player | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | Dimension | stöds inte | använd mediaReporting-fält |
| Externa fel-ID | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | Dimension | stöds inte | använd mediaReporting-fält |
| Droppar före start | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | Mått | Droppar före start |     |
| Buffertpåverkade strömmar | Stöds inte | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | Mått | Buffertpåverkade strömmar | beräknas från andra händelser |
| Ändrade bithastighetsströmmar som påverkas | Stöds inte | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | Mått | Ändrade bithastighetsströmmar som påverkas | beräknas från andra händelser |
| Felpåverkade strömmar | Stöds inte | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | Mått | Felpåverkade strömmar | beräknas från andra händelser |
| Ignorerade bildrutepåverkade strömmar | Stöds inte | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | Mått | Ignorerade bildrutepåverkade strömmar | beräknas från andra händelser |

{style="table-layout:auto"}

## Klassifikationer för Media Analytics

Klassificeringar av Media Analytics hämtas in till AEP via ett separat flöde som kallas ACDC. Varje klassificeringsgrupp som anges i tabellen nedan motsvarar en unik datauppsättning inom AEP. I CJA är det nödvändigt att upprätta en anslutning mellan Media Analytics-händelsedatamängden och alla klassificeringsdatamängder.

### Ansluta datauppsättningar i Customer Journey Analytics

Så här konfigurerar du anslutningen i Customer Journey Analytics:

- Navigera till fliken **Anslutningar** och välj **Skapa ny anslutning**.
- I anslutningsgränssnittet väljer du **Lägg till datauppsättningar** och letar reda på händelsedatamängden för Media Analytics (som används för att importera mediedata via ADC), tillsammans med de fyra relevanta klassificeringsdatamängderna.

### Konfigurationsinformation

Konfigurera följande för varje uppslagsdatauppsättning (klassificeringsdatamängd):

- **videodatauppsättning**:
   - Nyckel: `_sandbox.key`
   - Matchande nyckel: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - Datakälltyp: `Web Data`

- **videoad, datauppsättning**:
   - Nyckel: `_sandbox.key`
   - Matchande nyckel: `Ad ID (advertising.adAssetReference._id)`
   - Datakälltyp: `Web Data`

- **videoadpod-datauppsättning**:
   - Nyckel: `_sandbox.key`
   - Matchande nyckel: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - Datakälltyp: `Web Data`

- **videokortdatauppsättning**:
   - Nyckel: `_sandbox.key`
   - Matchande nyckel: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - Datakälltyp: `Web Data`

### Rapporteringshändelser

När du arbetar med klassificeringsdatamängderna under rapporteringen måste du referera till de klassificeringsspecifika fältsökvägarna (`ACDC XDM Path`) i stället för standardfälten för Media Analytics XDM.

## Klassificeringstabell

| Klassificeringsnamn (grupp) | Fältnamn | ACDC XDM-sökväg |
|------------|----------|-------------|
| video | Nyckel-/tillgångs-ID | `<_sandbox>.key` |
| video | Videolängd | `<_sandbox>.video_length` |
| video | Videonamn | `<_sandbox>.video_name` |
| video | Tillgångs-ID | `<_sandbox>.asset_id` |
| video | Första AIR-datum | `<_sandbox>.first_air_date` |
| video | Första digitala datum | `<_sandbox>.first_digital_date` |
| video | Innehållsklassificering | `<_sandbox>.content_rating` |
| video | Originator | `<_sandbox>.originator` |
| video | Nyckel/annons-ID | `<_sandbox>.key` |
| video | Annonslängd | `<_sandbox>.ad_length` |
| video | Annonsnamn | `<_sandbox>.ad_name` |
| video | CREATIVE ID | `<_sandbox>.creative_id` |
| videoadpod | Nyckel/annons-ID | `<_sandbox>.key` |
| videoadpod | Pod Position | `<_sandbox>.pod_position` |
| videoadpod | Pod Name | `<_sandbox>.pod_name` |
| videokort | Nyckel/kapitel | `<_sandbox>.key` |
| videokort | Kapitellängd | `<_sandbox>.chapter_length` |
| videokort | Kapitelavstånd | `<_sandbox>.chapter_offset` |
| videokort | Kapitelposition | `<_sandbox>.chapter_position` |
| videokort | Kapitelnamn | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Anpassade variabler för Media Analytics

I Adobe Analytics tilldelas anpassade variabler till olika händelser eller eVars beroende på de implementeringsregler som definieras i varje rapportserie. När dessa anpassade variabler importeras till Adobe Experience Platform (AEP) mappas de därför till olika XDM-sökvägar.

- Händelser lagras under sökvägen:

  `_experience.analytics.event<x>to<y>.event<number>.value`

- eVars lagras under sökvägen:

  `_experience.analytics.customDimensions.eVars.eVar<number>`

I båda fallen motsvarar `<number>` den specifika händelse eller det eVar-nummer som användes i den ursprungliga Adobe Analytics-rapportsvitskonfigurationen.

### Egna variabler

| Fältnamn | XDM-sökväg | Datatyp |
|-------------|-------------|-----------|
| Flagga för hämtning av media | `_experience.analytics.event<x>to<y>.event<number>.value` | Mått |
| SDK Version | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| VHL-version | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Strömformat | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Första AIR-datum | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Första digitala datum | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Federerade data | `_experience.analytics.customDimensions.eVars.eVar<number>` och `_experience.analytics.event<x>to<y>.event<number>.value` | Båda |
| Uppskattade strömmar | `_experience.analytics.event<x>to<y>.event<number>.value` | Mått |
| Antal annonser | `_experience.analytics.event<x>to<y>.event<number>.value` | Mått |
| Antal kapitel | `_experience.analytics.event<x>to<y>.event<number>.value` | Mått |
| CREATIVE ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Plats-ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| CREATIVE URL | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Placement-ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Bildrutor per sekund | `_experience.analytics.customDimensions.eVars.eVar<number>` och `_experience.analytics.event<x>to<y>.event<number>.value` | Båda |
| Fel-ID för Media SDK | `_experience.analytics.event<x>to<y>.event<number>.value` | Mått |
| Strömmar som påverkas | `_experience.analytics.event<x>to<y>.event<number>.value` | Mått |
| Fallande händelser | `_experience.analytics.event<x>to<y>.event<number>.value` | Mått |
| Total varaktighet för förvaring | `_experience.analytics.event<x>to<y>.event<number>.value` | Mått |

{style="table-layout:auto"}







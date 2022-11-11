---
title: Lär dig hur du migrerar från milstolpe till medieanalys
description: Lär dig hur du ändrar milstolpsvariabler till Media Analytics Metrics och Milestone-modulmetoder till Media Analytics-syntax.
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 11%

---

# Migrera från milstolpe till mediaanalys {#migrating-from-milestone-to-media-analytics}

## Översikt {#overview}

De centrala begreppen för videomätning är desamma för Milestone och Media Analytics, som tar videospelarhändelser och mappar dem till analysmetoder, samtidigt som de hämtar metadata och värden för spelaren och mappar dem till analysvariabler. Medieanalyslösningen växte ut ur milstolpen, så många av metoderna och mätvärdena är desamma, men konfigurationsstrategin och koden har ändrats avsevärt. Det bör vara möjligt att uppdatera händelsekoden för spelaren så att den pekar på de nya Media Analytics-metoderna. Se [SDK-översikt](/help/sdk-implement/setup/setup-overview.md) och [Spårningsöversikt](/help/sdk-implement/track-av-playback/track-core-overview.md) om du vill ha mer information om hur du implementerar Media Analytics.

I följande tabeller finns översättningar mellan milstolpe-lösningen och Media Analytics-lösningen.

## Migreringsguide {#migration-guide}

### Variabelreferens

| Mått för milstolpe | Variabeltyp | Media Analytics-mått |
| --- | --- | --- |
| Innehåll | eVar <br> Standardförfallodatum: Besök | Innehåll |
| Innehållstyp | eVar <br> Standardförfallodatum: Sidvy | Innehållstyp |
| Innehållstid | Händelse <br> Typ: Räknare | Innehållstid |
| Videostart | Händelse <br> Typ: Räknare | Videostart |
| Videon slutförs | Händelse <br> Typ: Räknare | Innehållet har slutförts |


### Mediemodvariabler

| Milstolpe | Syntax för milstolpe | Medieanalys | Syntax för medieanalys |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | Ej tillämpligt | Alla Media Analytics-data skickas endast med kontextdata. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | Ej tillämpligt | Kontextdata för Media Analytics fylls automatiskt i i reserverade variabler. Mappning till eVars, props och händelser som jag inte längre behöver i implementeringskoden. Kunder kan mappa kontextdata till variabler med bearbetningsregler. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | Ej tillämpligt | Krävs inte längre eftersom mappning sker via reserverade variabler och bearbetningsregler. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | Ej tillämpligt | Krävs inte längre eftersom mappning sker via reserverade variabler och bearbetningsregler. |

### Valfria variabler

| Milstolpe | Syntax för milstolpe | Medieanalys | Syntax för medieanalys |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | Ej tillämpligt | Vi tillhandahåller inte längre färdiga spelarmappningar. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | Ej tillämpligt | Vi tillhandahåller inte längre färdiga spelarmappningar. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | Ej tillämpligt | Innehållet Fullständigt stöder endast en 100 % förloppsindikator. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | Ej tillämpligt | Innehållet Fullständigt stöder endast en 100 % förloppsindikator. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK-nyckel: playerName;<br> API-nyckel: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | Ej tillämpligt | Media Analytics är inställt på 10 sekunder för innehåll och 1 sekund för annonser. Inga andra alternativ är tillgängliga. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | Ej tillämpligt | Media Analytics håller alltid reda på förloppsindikatorer med 10 %, 25 %, 50 %, 75 % och 95 %. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | Ej tillämpligt | Media Analytics håller alltid reda på förloppsindikatorer med 10 %, 25 %, 50 %, 75 % och 95 %. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |

### Annonsspårningsvariabler

| Milstolpe | Syntax för milstolpe | Medieanalys | Syntax för medieanalys |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | Ej tillämpligt | Media Analytics är inställt på 10 sekunder för innehåll och 1 sekund för annonser. Inga andra alternativ är tillgängliga. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | Ej tillämpligt | Förloppsmarkörer anges inte som standard för annonser. Använd beräknade mätvärden för att skapa annonsförloppsmarkörer. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | Ej tillämpligt | Media Analytics är inställt på 1 sekund för annonser. Inga andra alternativ är tillgängliga. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |

### Media Module-metoder

| Milstolpe | Syntax för milstolpe | Medieanalys | Syntax för medieanalys |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`: (obligatoriskt) Namnet på videon som du vill att den ska visas i videorapporter. | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`: (obligatoriskt) Videons längd i sekunder. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`: (obligatoriskt) Namnet på den mediespelare som användes för att visa videon, så som du vill att den ska visas i videorapporter. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name`: (obligatoriskt) Annonsens namn eller ID. | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`: (obligatoriskt) Annonsens längd. | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`: (obligatoriskt) Namnet på den mediespelare som användes för att visa annonsen. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: Namnet eller ID för det primära innehållet där annonsen är inbäddad. | Ej tillämpligt | Ärvs automatiskt. |
| parentPod | `parentPod`: Positionen i annonsens primära innehåll spelades upp. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: Positionen i rutan där annonsen spelas upp. | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: CPM eller krypterad CPM (prefix med ett &quot;~&quot;) som gäller för den här uppspelningen. | Ej tillämpligt | Inte tillgängligt som standard i Media Analytics. |
| Media.click | `s.Media.click(name, offset)` | Ej tillämpligt | Använd ett anpassat länkanalysanrop för att spåra klickningar. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause <br> eller <br> trackEvent | `trackPause()` <br> eller `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> eller <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Använd anpassade metadata eller standardmetadata för att ange ytterligare variabler. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | Ej tillämpligt | Frekvensen för spårningsanrop ställs in automatiskt. |

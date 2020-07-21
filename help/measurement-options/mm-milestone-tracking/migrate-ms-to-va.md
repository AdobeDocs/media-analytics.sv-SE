---
title: Migrera från milstolpe till Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: aa2a230daa96b823f9963345ac4578799e59d3f5
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 10%

---


# Migrera från milstolpe till Media Analytics {#migrating-from-milestone-to-media-analytics}

## Översikt {#overview}

De centrala begreppen för videomätning är desamma för Milestone och Media Analytics, som tar videospelarhändelser och mappar dem till analysmetoder, samtidigt som de hämtar metadata och värden för spelaren och mappar dem till analysvariabler. Media Analytics-lösningen växte ut ur milstolpen, så många av metoderna och mätvärdena är desamma, men konfigurationsstrategin och koden har ändrats avsevärt. Det bör vara möjligt att uppdatera spelarens händelsekod så att den pekar på de nya Media Analytics-metoderna. Mer information om hur du implementerar Media Analytics finns i Översikt [och](/help/sdk-implement/setup/setup-overview.md) Spårningsöversikt [för](/help/sdk-implement/track-av-playback/track-core-overview.md) SDK.

I följande tabeller finns översättningar mellan Milstolpe-lösningen och Media Analytics-lösningen.

## Migreringsguide {#migration-guide}

### Variabelreferens

| Mått för milstolpe | Variabeltyp | Media Analytics Metric |
| --- | --- | --- |
| Innehåll | Giltighetstid<br>för eVarDefault: Besök | Innehåll |
| Innehållstyp | eVar<br> standardutgångsdatum: Sidvy | Innehållstyp |
| Innehållstid | Händelsetyp<br> : Räknare | Innehållstid |
| Videostart | Händelsetyp<br> : Räknare | Videostart |
| Videon slutförs | Händelsetyp<br> : Räknare | Innehållet har slutförts |

### Mediemodvariabler

| Milstolpe | Syntax för milstolpe | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | Ej tillämpligt | Alla Analytics-data för Media skickas endast med kontextdata. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | Ej tillämpligt | Media Analytics-kontextdata fylls automatiskt i i reserverade variabler. Mappning till eVars, props och händelser som jag inte längre behöver i implementeringskoden. Kunder kan mappa kontextdata till variabler med bearbetningsregler. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | Ej tillämpligt | Krävs inte längre eftersom mappningen görs via reserverade variabler och bearbetningsregler. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | Ej tillämpligt | Krävs inte längre eftersom mappningen görs via reserverade variabler och bearbetningsregler. |

### Valfria variabler

| Milstolpe | Syntax för milstolpe | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | Ej tillämpligt | Vi tillhandahåller inte längre färdiga spelarmappningar. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | Ej tillämpligt | Vi tillhandahåller inte längre färdiga spelarmappningar. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | Ej tillämpligt | Innehållet Fullständigt stöder endast en 100 % förloppsindikator. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | Ej tillämpligt | Innehållet Fullständigt stöder endast en 100 % förloppsindikator. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK-nyckel: playerName;<br> API-nyckel: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | Ej tillämpligt | Media Analytics är inställt på 10 sekunder för innehåll och 1 sekund för annonser. Inga andra alternativ är tillgängliga. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | Ej tillämpligt | Media Analytics spårar alltid förloppsindikatorer vid 10 %, 25 %, 50 %, 75 %, 95 % |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | Ej tillämpligt | Media Analytics spårar alltid förloppsindikatorer vid 10 %, 25 %, 50 %, 75 %, 95 % |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |

### Annonsspårningsvariabler

| Milstolpe | Syntax för milstolpe | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | Ej tillämpligt | Media Analytics är inställt på 10 sekunder för innehåll och 1 sekund för annonser. Inga andra alternativ är tillgängliga. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | Ej tillämpligt | Förloppsmarkörer anges inte som standard för annonser. Använd beräknade mätvärden för att skapa annonsförloppsmarkörer. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | Ej tillämpligt | Media Analytics är inställt på 1 sekund för annonser. Inga andra alternativ är tillgängliga. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |

### Media Module-metoder

| Milstolpe | Syntax för milstolpe | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName - (obligatoriskt) <br> Namnet på videon som du vill att den ska visas i videorapporter. | `mediaName` | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength - (Required) <br> Videons längd i sekunder. | `mediaLength` | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName - (obligatoriskt) <br> Namnet på den mediespelare som användes för att visa videon, så som du vill att den ska visas i videorapporter. | `mediaPlayerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name - (Required) <br> Annonsens namn eller ID. | `name` | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length - (Required) <br> Annonsens längd. | `length` | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName - (Required) <br> Namnet på den mediespelare som användes för att visa annonsen. | `playerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName <br> Namnet eller ID för det primära innehåll där annonsen är inbäddad. | `parentName` | Ej tillämpligt | Automatiskt ärvd |
| parentPod <br> Positionen i annonsens primära innehåll spelades upp. | `parentPod` | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition <br> Den position i rutan där annonsen spelas upp. | `parentPodPosition` | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM <br> CPM eller krypterad CPM (prefix with a &quot;~&quot;) som gäller för den här uppspelningen. | `CPM` | Ej tillämpligt | Inte tillgängligt som standard i Media Analytics. |
| Media.click | `s.Media.click(` <br> `  name,` <br> `  offset)` | Ej tillämpligt | Använd ett anpassat länkanalysanrop för att spåra klickningar. |
| Media.close | `s.Media.close(` <br> `  mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | trackPause <br> eller <br> trackEvent | `trackPause()` <br> eller `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> eller <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Använd anpassade metadata eller standardmetadata för att ange ytterligare variabler. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | Ej tillämpligt | Frekvensen för spårningsanrop ställs in automatiskt. |


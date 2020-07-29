---
title: Migrera från milstolpe till Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: e25c4d0add969ad31393f2eeb33b1a12b7205586
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 12%

---


# Migrera från milstolpe till Media Analytics {#migrating-from-milestone-to-media-analytics}

## Översikt {#overview}

De centrala begreppen för videomätning är desamma för Milestone och Media Analytics, som tar videospelarhändelser och kopplar dem till analysmetoder, samtidigt som de samlar in spelarmetadata och -värden och mappar dem till analysvariabler. Media Analytics-lösningen växte upp ur Milstone, så många av metoderna och måtten är desamma, men konfigurationsstrategin och koden har ändrats avsevärt. Det bör vara möjligt att uppdatera spelarens händelsekod så att den pekar på de nya Media Analytics-metoderna. Se [SDK-översikt](/help/sdk-implement/setup/setup-overview.md) och [Spårningsöversikt](/help/sdk-implement/track-av-playback/track-core-overview.md) om du vill ha mer information om hur du implementerar Media Analytics.

I följande tabeller finns översättningar mellan Milestone-lösningen och Media Analytics-lösningen.

## Migreringsguide {#migration-guide}

### Variabelreferens

| Momsmetri för milsten | Variabeltyp | Media Analytics-mått |
| --- | --- | --- |
| Innehåll | eVar <br> Standardförfallodatum: Besök | Innehåll |
| Innehållstyp | eVar <br> Standardförfallodatum: Sidvy | Innehållstyp |
| Innehållstid spenderad | Händelse <br> Typ: Räknare | Innehållstid spenderad |
| Videoinitieringar | Händelse <br> Typ: Räknare | Videoinitieringar |
| Videon är klar | Händelse <br> Typ: Räknare | Innehållet har slutförts |

### Mediemodulvariabler

| Milstolpe | Milstolpsyntax | Medieanalys | Syntax för medieanalys |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | Ej tillämpligt | Alla Media Analytics-data skickas endast med kontextdata. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | Ej tillämpligt | Kontextdata för medieanalys fylls automatiskt i reserverade variabler. Mappning till eVars, props och händelser som jag inte längre behövde inom implementeringskoden. Kunder kan mappa kontextdata till variabler med bearbetningsregler. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | Ej tillämpligt | Det behövs inte längre eftersom kartläggningen sker via reserverade variabler och bearbetningsregler. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | Ej tillämpligt | Det behövs inte längre eftersom kartläggningen sker via reserverade variabler och bearbetningsregler. |

### Valfria variabler

| Milstolpe | Milstolpsyntax | Medieanalys | Syntax för medieanalys |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | Ej tillämpligt | Vi tillhandahåller inte längre förbyggda spelkartor. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | Ej tillämpligt | Vi tillhandahåller inte längre förbyggda spelkartor. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | Ej tillämpligt | Innehållet slutfört stöder endast en 100 %-förloppsmarkör. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | Ej tillämpligt | Innehållet slutfört stöder endast en 100 %-förloppsmarkör. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK-nyckel: playerName;<br> API-nyckel: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | Ej tillämpligt | Media Analytics är inställt på 10 sekunder för innehåll och 1 sekund för annonser. Inga andra alternativ är tillgängliga. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | Ej tillämpligt | Media Analytics spårar alltid framstegsmarkörer med 10 %, 25 %, 50 %, 75 %, 95 %. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | Ej tillämpligt | Media Analytics spårar alltid framstegsmarkörer med 10 %, 25 %, 50 %, 75 %, 95 %. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |

### Värdspårningsvariabler

| Milstolpe | Milstolpsyntax | Medieanalys | Syntax för medieanalys |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | Ej tillämpligt | Media Analytics är inställt på 10 sekunder för innehåll och 1 sekund för annonser. Inga andra alternativ är tillgängliga. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | Ej tillämpligt | Förloppsmarkörer tillhandahålls inte som standard för annonser. Använd beräknade mått för att skapa och förloppsmarkörer. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | Ej tillämpligt | Media Analytics är inställt på 1 sekund för annonser. Inga andra alternativ är tillgängliga. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | Ej tillämpligt | Automatiskt spår är inte längre tillgängligt. |

### Metoder för mediemodul

| Milstolpe | Milstolpsyntax | Medieanalys | Syntax för medieanalys |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`: (obligatoriskt) Namnet på videon som du vill att den ska visas i videorapporter. | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`: (obligatoriskt) Videons längd i sekunder. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`: (obligatoriskt) Namnet på den mediaspelare som används för att visa videon, som du vill att den ska visas i videorapporter. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| namn | `name`: (obligatoriskt) Namn eller ID för annonsen. | namn | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| längd | `length`: (krävs) Annonsens längd. | längd | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`: (obligatoriskt) Namnet på mediaspelaren som används för att visa annonsen. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: Namnet eller ID för det primära innehållet där annonsen bäddas in. | Ej tillämpligt | Ärv automatiskt. |
| parentPod | `parentPod`: Positionen i det primära innehållet som annonsen spelades upp. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: Placeringen i den punkt där annonsen spelas upp. | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: CPM eller krypterad CPM (förfixerad med ett &quot;~&quot;) som gäller för den här uppspelningen. | Ej tillämpligt | Inte tillgängligt som standard i Media Analytics. |
| Media.click | `s.Media.click(name, offset)` | Ej tillämpligt | Använd ett anpassat länkanalysanrop för att spåra klick. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | spårPaus <br> eller <br> traceEvent | `trackPause()` <br> eller `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> eller <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Använd anpassade metadata eller standardmetadata för att ange ytterligare variabler. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | Ej tillämpligt | Frekvensen för spårningssamtal ställs in automatiskt. |

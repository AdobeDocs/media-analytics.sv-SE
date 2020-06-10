---
title: Migrera från milstolpe till mediaanalys
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 20%

---


# Migrera från milstolpe till mediaanalys {#migrating-from-milestone-to-media-analytics}

## Översikt {#overview}

De centrala begreppen för videomätning är desamma för Milestone och Media Analytics, som tar videospelarhändelser och mappar dem till analysmetoder, samtidigt som de hämtar metadata och värden för spelaren och mappar dem till analysvariabler. Medieanalyslösningen växte ut ur milstolpen, så många av metoderna och mätvärdena är desamma, men konfigurationsstrategin och koden har ändrats avsevärt. Det bör vara möjligt att uppdatera händelsekoden för spelaren så att den pekar på de nya Media Analytics-metoderna. Mer information om hur du implementerar Media Analytics finns i Översikt [och](/help/sdk-implement/setup/setup-overview.md) Spårningsöversikt [för](/help/sdk-implement/track-av-playback/track-core-overview.md) SDK.

I följande tabeller finns översättningar mellan milstolpe-lösningen och Media Analytics-lösningen.

## Migreringsguide {#migration-guide}

### Variabelreferens

| Mått för milstolpe | Variabeltyp | Media Analytics-mått |
| --- | --- | --- |
| Innehåll | Giltighetstid<br/><br/>för eVarDefault: Besök | Innehåll |
| Innehållstyp | eVar<br/><br/> standardutgångsdatum: Sidvy | Innehållstyp |
| Innehållstid | Händelsetyp<br/><br/> : Räknare | Innehållstid |
| Videostart | Händelsetyp<br/><br/> : Räknare | Videostart |
| Videon slutförs | Händelsetyp<br/><br/> : Räknare | Innehållet har slutförts |

### Mediemodvariabler

<table>
<thead>
<tr>
<th>Milstolpe
</th>
<th>Syntax för milstolpe
</th>
<th>Medieanalys
</th>
<th>Syntax för medieanalys
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.trackUsingContextData = true;
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Alla Media Analytics-data skickas endast med kontextdata.
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = {
  "a.media.name":"eVar2,prop2",
  "a.media.segment":"eVar3",
  "a.contentType":"eVar1",
  "a.media.timePlayed":"event3",
  "a.media.view":"event1",
  "a.media.segmentView":"event2",
  "a.media.complete":"event7",
  "a.media.milestones": {
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Kontextdata för Media Analytics fylls i automatiskt i i reserverade variabler. Mappning till eVars, props och händelser behövs inte längre i implementeringskoden. Kunder kan mappa kontextdata till variabler med bearbetningsregler.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = 
  "events,
  prop2,
  eVar1,
  eVar2,
  eVar3";
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Krävs inte längre eftersom mappning sker via reserverade variabler och bearbetningsregler.
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = 
  "event1,
  event2,
  event3,
  event4,
  event5,
  event6,
  event7"
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Krävs inte längre eftersom mappning sker via reserverade variabler och bearbetningsregler.
</td>
</tr>
</tbody>
</table>

### Valfria variabler

<table>
<thead>
<tr>
<th>Milstolpe
</th>
<th>Syntax för milstolpe
</th>
<th>Medieanalys
</th>
<th>Syntax för medieanalys
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack = true;
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Vi tillhandahåller inte längre färdiga spelarmappningar.
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  autoTrackNetStreams = true
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Vi tillhandahåller inte längre färdiga spelarmappningar.
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  completeByCloseOffset = true
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Innehållet Fullständigt stöder endast en 100 % förloppsindikator.
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold = 1
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Innehållet Fullständigt stöder endast en 100 % förloppsindikator.
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "Namn på anpassad spelare"
</pre>
</td>
<td>
SDK-nyckel: playerName; 
API-nyckel: media.playerName
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.
  trackSeconds = 15
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Media Analytics är inställt på 10 sekunder för innehåll och 1 sekund för annonser. Inga andra alternativ är tillgängliga.
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.
  trackMilestone = "25,50,75";
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Media Analytics håller alltid reda på förloppsindikatorer med 10 %, 25 %, 50 %, 75 %, 95 %
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  trackOffsetMilestone = "20,40,60";
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Media Analytics håller alltid reda på förloppsindikatorer med 10 %, 25 %, 50 %, 75 %, 95 %
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestone = true;
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Automatiskt spår är inte längre tillgängligt
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestone = true;
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Automatiskt spår är inte längre tillgängligt
</td>
</tr>
</tbody>
</table>

### Annonsspårningsvariabler

<table>
<thead>
<tr>
<th>Milstolpe
</th>
<th>Syntax för milstolpe
</th>
<th>Medieanalys
</th>
<th>Syntax för medieanalys
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.
  adTrackSeconds = 15
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Media Analytics är inställt på 10 sekunder för innehåll och 1 sekund för annonser. Inga andra alternativ är tillgängliga.
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.
  adTrackMilestone = "25,50,75";
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Förloppsmarkörer anges inte som standard för annonser. Usecalculated metrics to build ad ad progress markers.
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestone = "20,40,60";
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Media Analytics är inställt på 1 sekund för annonser. Inga andra alternativ är tillgängliga.
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestone = true;
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Automatiskt spår är inte längre tillgängligt
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestone = true;
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Automatiskt spår är inte längre tillgängligt
</td>
</tr>
</tbody>
</table>

### Media Module-metoder

<table>
<thead>
<tr>
<th>Milstolpe
</th>
<th>Syntax för milstolpe
</th>
<th>Medieanalys
</th>
<th>Syntax för medieanalys
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open(
  mediaName,
  mediaLength,
  mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart(
  mediaObject, 
  contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName - (obligatoriskt) Namnet på videon som du vill att den ska visas i videorapporter.
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createMediaObject(
  name, 
  mediaId, 
  length, 
  streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength - (Required) Videons längd i sekunder.
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createMediaObject(
  name, 
  mediaId, 
  length, 
  streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName - (obligatoriskt) Namnet på den mediespelare som användes för att visa videon, så som du vill att den ska visas i videorapporter.
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(
  name,
  length,
  playerName,
  parentName,
  parentPod,
  parentPodPosition,
  CPM)
</pre>
</td>
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
mediaHeartbeat.trackEvent(
  MediaHeartbeat.
    Event.
    AdBreakStart, 
  adBreakObject);
...
trackEvent(
  MediaHeartbeat.
    Event.
    AdStart, 
  adObject, 
  adCustomMetadata);
</pre>
</td>
</tr>
<tr>
<td>
name - (Required) The name or ID of the ad.
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
length(Required) Annonsens längd.
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
playerName - (Required) Namnet på mediaplayer som används för att visa annonsen.
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
parentName - Namnet eller ID:t på det primära innehåll där annonsen är inbäddad.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Automatiskt ärvd
</td>
</tr>
<tr>
<td>
parentPod - Positionen i annonsens primära innehåll spelades upp.
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdBreakObject(
  name, 
  position, 
  startTime)
</pre>
</td>
</tr>
<tr>
<td>
parentPodPosition - positionen i rutan där annonsen spelas upp.
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
CPMTThe CPM or encrypted CPM (prefixed with a "~") that apply to this playback.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt som standard i Media Analytics
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click( namn, förskjutning)
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Använd ett anpassat länkanalysanrop för att spåra klickningar
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close( mediaName)
</pre>
</td>
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(
  name,
  offset)
</pre>
</td>
<td>
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play(
  name,
  offset,
  segmentNum,
  segment, 
  segmentLength)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop( mediaName, mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> eller 
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
eller
<pre>
trackEvent(
  MediaHeartbeat.
  Event.
  SeekStart)
</pre> eller
<pre>
trackEvent(
  MediaHeartbeat.
  Event.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>Använd anpassade metadata eller standardmetadata för att ange ytterligare variabler
</td>
<td>
<pre>
var customVideoMetadata = 
{
  isUserLoggedIn: 
    "false",
  tvStation: 
    "Sample TV station",
  programmer: 
    "Sample programmer"
};
...
var standardVideoMetadata 
  = {};
standardVideoMetadata
  [MediaHeartbeat.
   VideoMetadataKeys.
   EPISODE] = 
  "Sample Episode";
standardVideoMetadata
  [MediaHeartbeat.
   VideoMetadataKeys.
   SHOW] = "Sample Show";
...
mediaObject.setValue(
  MediaHeartbeat.
  MediaObjectKey.
  StandardVideoMetadata, 
  standardVideoMetadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track( mediaName)
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Frekvensen för spårningsanrop ställs in automatiskt.
</td>
</tr>
</tbody>
</table>


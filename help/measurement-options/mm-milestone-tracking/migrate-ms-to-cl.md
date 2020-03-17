---
title: Migrera från milstolpe till anpassad länk
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Migrera från milstolpe till anpassad länk{#migrating-from-milestone-to-custom-link}

## Översikt {#overview}

De centrala begreppen för videomätning är desamma för milstolpe och Custom Link tracking, som tar videospelarhändelser och mappar dem till analysmetoder, samtidigt som spelarens metadata och värden hämtas och mappas till analysvariabler. Metoden Custom Link bör ses som en nedbantning och en förenkling av både implementeringen och de data som samlas in. Med Custom Link-lösningen är inga variabler eller metoder fördefinierade för videomätning, utan en fullständig anpassad konfiguration krävs. Det bör vara möjligt att uppdatera spelarens händelsekod så att den pekar på anpassade länkspårningsanrop för grundläggande spelarhändelser som start och complete. Mer information finns i Implementeringshandboken [för](/help/measurement-options/cl-in-aa/cl-impl-guide.md) anpassad länk och [Manuell länkspårning med anpassad länkkod](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) .

I följande tabeller finns översättningar mellan milstolpe-lösningen och Custom Link-lösningen.

## Migreringsguide {#migration-guide}

### Videovariabelreferens

<table>
<thead>
<tr>
<th><strong>Mått för milstolpe</strong></th>
<th><strong>Variabeltyp</strong></th>
<th><strong>Egen länk</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Innehåll</td>
<td>
<p>eVar</p>
<p>Standardförfallodatum: Besök</p>
</td>
<td>Definiera din egen eVar</td>
</tr>
<tr>
<td>Innehållstyp</td>
<td>
<p>eVar</p>
<p>Standardförfallodatum: Sidvy</p>
</td>
<td>Definiera din egen eVar</td>
</tr>
<tr>
<td>Innehållstid</td>
<td>
<p>Händelse</p>
<p>Typ: Räknare</p>
</td>
<td>Definiera din egen händelse</td>
</tr>
<tr>
<td>Videostart</td>
<td>
<p>Händelse</p>
<p>Typ: Räknare</p>
</td>
<td>Definiera din egen händelse</td>
</tr>
<tr>
<td>Videon slutförs</td>
<td>
<p>Händelse</p>
<p>Typ: Räknare</p>
</td>
<td>Definiera din egen händelse</td>
</tr>
</tbody>
</table>

### Mediemodvariabler

<table>
<thead>
<tr>
<th>Milstolpe
</th>
<th>Syntax för milstolpe
</th>
<th>Egen länk
</th>
<th>Syntax för anpassad länk
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
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name'; 
s.contextData["video.name"] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  contextDataMapping = { "a.media.name":
    "eVar2,prop2", "a.media.segment":
    "eVar3", "a.contentType":
    "eVar1", "a.media.timePlayed":
    "event3", "a.media.view":
    "event1", "a.media.segmentView":
    "event2", "a.media.complete":
    "event7", "a.media.millestone":{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Mappning av kontextdata till eVars, props och händelser har nu slutförts via bearbetningsregler.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = "events, prop2, eVar1, eVar2, eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData.
       video.name, contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = "event1, event2, event3, event4, event5, event6, event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>Milstolpe
</th>
<th>Syntax för milstolpe
</th>
<th>Egen länk
</th>
<th>Syntax för anpassad länk
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
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name'; 
s.contextData["video.name"] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segmentView": "event2", "a.media.complete":"event7", "a.media.millestone":{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Mappning av kontextdata till eVars, props och händelser har nu slutförts via bearbetningsregler.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = "events, prop2, eVar1, eVar2, eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData.
       video.name, contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = "event1, event2, event3, event4, event5, event6, event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
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
<th>Egen länk
</th>
<th>Syntax för anpassad länk
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
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams = true
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset = true
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
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
<td>Inte tillgängligt
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
Ange eVar- eller kontextdatavariabeln i länkanrop
</td>
<td>
<pre>
s.contextData['video.player'] ="CustomPlayer Name";
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.trackMilstolpar
</td>
<td>
<pre>
s.Media.trackMilestone = "25,50,75";
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilstolpar
</td>
<td>
<pre>
s.Media.trackOffsetMilestone = "20,40,60";
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.segmentByMilestone
</td>
<td>
<pre>
s.Media.segmentByMilestone = true;
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilstolpar
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestone = true;
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
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
<th>Egen länk
</th>
<th>Syntax för anpassad länk
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
s.Media.adTrackSeconds = 15 
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.adTrackMilstolpar
</td>
<td>
<pre>
s.Media.adTrackMilestone = "25,50,75";
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilstolpar
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestone = "20,40,60";
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestone
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestone = true;
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilstolpar
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestone = true;
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
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
<th>Egen länk
</th>
<th>Syntax för anpassad länk
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open( mediaName, mediaLength, mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.video.name, contextData.video.view';
s.linkTrackEvents = 'event2';
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.eVar12 = "video";
s.eVar15 = mediaPlayerName;
s.events = 'event2';
s.contextData['video.name'] = mediaName;
s.contextData['video.view'] = 'true';
s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>mediaName:</b> (obligatoriskt) Namnet på videon som du vill att den ska visas i videorapporter.</td>
<td>Ange eVar- eller kontextdatavariabeln i länkanrop</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name'] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>mediaLength:</b> (obligatoriskt) Videons längd i sekunder.
</td>
<td>
Ange eVar- eller kontextdatavariabeln i länkanrop
</td>
<td>
<pre>
s.contextData['video.length'] ="90";
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>mediaPlayerName:</b> (obligatoriskt) Namnet på den mediespelare som används för att visa videon, så som du vill att den ska visas i videorapporter.
</td>
<td>
Ange eVar- eller kontextdatavariabeln i länkanrop
</td>
<td>
<pre>
s.contextData['video.player'] ="CustomPlayer Name";
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd( name, length, playerName, parentName, parentPod, parentPodPosition, CPM)
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt</td>
</tr>
<tr>
<td>name</td>
<td><b>namn:</b> (obligatoriskt) Annonsens namn eller ID.</td>
<td>Ej tillämpligt</td>
<td>Inte tillgängligt</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>längd:</b> (obligatoriskt) Annonsens längd.
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b>playerName:</b> (obligatoriskt) Namnet på mediespelaren som används för att visa annonsen.
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName:</b> Namnet eller ID för det primära innehåll där annonsen är inbäddad.
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod:</b> Positionen i det primära innehållet som annonsen spelades upp.
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition:</b> Positionen i rutan där thead spelas upp.
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM:</b> CPM eller krypterad CPM (prefix with a "~") som gäller för den här uppspelningen.
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name, offset)
</pre>
</td>
<td>
<pre>
s.tl()
</pre>
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
s.Media.close(mediaName)
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete( namn, offset)
</pre>
</td>
<td>
s.tl()
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.
       video.name, contextData.
       video.complete';
s.linkTrackEvents = 'event3';
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.eVar12 = "video";
s.eVar15 = mediaPlayerName;
s.events = 'event3';
s.contextData['video.name'] = mediaName;
s.contextData['video.complete'] = 'true';
s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play( namn, offset, segmentNum, segment, segmentLength)
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop( mediaName, mediaOffset)
</pre>
</td>
<td>Ej tillämpligt 
</td>
<td>Inte tillgängligt
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
Ange eVar- eller kontextdatavariabeln i länkanrop
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.
       video.name, contextData.
       video.view';
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>Ej tillämpligt
</td>
<td>Inte tillgängligt
</td>
</tr>
</tbody>
</table>


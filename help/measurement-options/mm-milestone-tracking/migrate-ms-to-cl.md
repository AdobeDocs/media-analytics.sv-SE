---
title: Lär dig hur du migrerar från milstolpe till anpassad länk
description: Lär dig hur du ändrar milstolpsvariabler till metoder i modulerna för anpassad länk och milstolpe till syntaxen för anpassad länk.
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 15%

---

# Migrera från milstolpe till anpassad länk{#migrating-from-milestone-to-custom-link}

## Översikt {#overview}

De centrala begreppen för videomätning är desamma för milstolpe och Custom Link tracking, som tar videospelarhändelser och mappar dem till analysmetoder, samtidigt som spelarens metadata och värden hämtas och mappas till analysvariabler. Metoden Custom Link bör ses som en nedbantning och en förenkling av både implementeringen och de data som samlas in. Med Custom Link-lösningen är inga variabler eller metoder fördefinierade för videomätning, utan en fullständig anpassad konfiguration krävs. Det bör vara möjligt att uppdatera spelarens händelsekod så att den pekar på anpassade länkspårningsanrop för grundläggande spelarhändelser som start och complete. Mer information finns i [Implementeringsguiden för anpassade länkar](/help/measurement-options/cl-in-aa/cl-impl-guide.md).

I följande tabeller finns översättningar mellan milstolpe-lösningen och Custom Link-lösningen.

## Migreringsguide {#migration-guide}

### Videovariabelreferens

| Mått för milstolpe | Variabeltyp | Anpassad länk |
| --- | --- | --- |
| Innehåll | eVar <br> Standardförfallodatum: Besök | Definiera din egen eVar. |
| Innehållstyp | eVar <br> Standardförfallodatum: Sidvy | Definiera din egen eVar. |
| Innehållstid | Händelsens <br>-typ: Räknare | Definiera din egen händelse. |
| Videostart | Händelsens <br>-typ: Räknare | Definiera din egen händelse. |
| Videon slutförs | Händelsens <br>-typ: Räknare | Definiera din egen händelse. |

### Mediemodvariabler

| Milstolpe | Syntax för milstolpe | Anpassad länk | Syntax för anpassad länk |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | Ej tillämpligt | Mappning av kontextdata till eVars, props och händelser slutförs nu via bearbetningsregler. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Valfria variabler

| Milstolpe | Syntax för milstolpe | Anpassad länk | Syntax för anpassad länk |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | Ej tillämpligt | Inte tillgängligt. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | Ej tillämpligt | Inte tillgängligt. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | Ej tillämpligt | Inte tillgängligt. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | Ej tillämpligt | Inte tillgängligt. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Ange eVar- eller kontextdatavariabel i länkanrop. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | Ej tillämpligt | Inte tillgängligt. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | Ej tillämpligt | Inte tillgängligt. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | Ej tillämpligt | Inte tillgängligt. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | Ej tillämpligt | Inte tillgängligt. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | Ej tillämpligt | Inte tillgängligt. |

### Annonsspårningsvariabler

| Milstolpe | Syntax för milstolpe | Anpassad länk | Syntax för anpassad länk |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | Ej tillämpligt | Inte tillgängligt. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | Ej tillämpligt | Inte tillgängligt. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | Ej tillämpligt | Inte tillgängligt. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | Ej tillämpligt | Inte tillgängligt. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | Ej tillämpligt | Inte tillgängligt. |

### Media Module-metoder

| Milstolpe | Syntax för milstolpe | Anpassad länk | Syntax för anpassad länk |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`: (obligatoriskt) Namnet på videon som du vill att den ska visas i videorapporter. | Ange eVar- eller kontextdatavariabel i länkanrop. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`: (obligatoriskt) Videons längd i sekunder. | Ange eVar- eller kontextdatavariabel i länkanrop. | `s.contextData['video.length']` <br> `  = ”90”;` |
| mediaPlayerName | `mediaPlayerName`: (obligatoriskt) Namnet på den mediespelare som användes för att visa videon, så som du vill att den ska visas i videorapporter. | Ange eVar- eller kontextdatavariabel i länkanrop. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | Ej tillämpligt | Inte tillgängligt. |
| name | `name`: (obligatoriskt) Annonsens namn eller ID. | Ej tillämpligt | Inte tillgängligt. |
| length | `length`: (obligatoriskt) Annonsens längd. | Ej tillämpligt | Inte tillgängligt. |
| playerName | `playerName`: (obligatoriskt) Namnet på den mediespelare som användes för att visa annonsen. | Ej tillämpligt | Inte tillgängligt. |
| parentName | `parentName`: Namnet eller ID för det primära innehållet där annonsen är inbäddad. | Ej tillämpligt | Inte tillgängligt. |
| parentPod | `parentPod`: Positionen i annonsens primära innehåll spelades upp. | Ej tillämpligt | Inte tillgängligt. |
| parentPodPosition | `parentPodPosition`: Positionen i rutan där annonsen spelas upp. | Ej tillämpligt | Inte tillgängligt. |
| CPM | `CPM`: CPM eller krypterad CPM (prefix med ett &quot;~&quot;) som gäller för den här uppspelningen. | Ej tillämpligt | Inte tillgängligt. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | Använd ett anpassat länkanalysanrop för att spåra klickningar. |
| Media.close | `s.Media.close(mediaName)` | Ej tillämpligt | Inte tillgängligt. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | Ej tillämpligt | Inte tillgängligt. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | Ej tillämpligt | Inte tillgängligt. |
| Media.monitor | `s.Media.monitor(s, media)` | Ange eVar- eller kontextdatavariabel i länkanrop. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | Ej tillämpligt | Inte tillgängligt. |

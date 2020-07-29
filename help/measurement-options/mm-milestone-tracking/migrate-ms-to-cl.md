---
title: Migrera från milstolpe till anpassad länk
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: e25c4d0add969ad31393f2eeb33b1a12b7205586
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 17%

---


# Migrera från milstolpe till anpassad länk{#migrating-from-milestone-to-custom-link}

## Översikt {#overview}

De centrala begreppen för videomätning är desamma för Milestone och Custom Link Tracking, som tar videospelarhändelser och kopplar dem till analysmetoder, samtidigt som spelarmetadata och -värden hämtas och mappas till analysvariabler. Metoden med anpassade länkar bör betraktas som en minskning och förenkling av både genomförandet och de uppgifter som samlas in. Med lösningen Anpassad länk är inga variabler eller metoder fördefinierade för videomätning, utan kräver en fullständig anpassad konfiguration. Det bör vara möjligt att uppdatera spelarens händelsekod för att peka på de anpassade länkspårningsanropen för grundläggande spelarhändelser som start och slutförande. Se [Implementeringsguide för anpassad länk](/help/measurement-options/cl-in-aa/cl-impl-guide.md) för mer information.

I följande tabeller finns översättningar mellan lösningen med milstolpe och lösningen med anpassad länk.

## Migreringsguide {#migration-guide}

### Videovariabelreferens

| Momsmetri för milsten | Variabeltyp | Anpassad länk |
| --- | --- | --- |
| Innehåll | eVar <br> Standardförfallodatum: Besök | Definiera din egen eVar. |
| Innehållstyp | eVar <br> Standardförfallodatum: Sidvy | Definiera din egen eVar. |
| Innehållstid spenderad | Händelse <br> Typ: Räknare | Definiera din egen händelse. |
| Videoinitieringar | Händelse <br> Typ: Räknare | Definiera din egen händelse. |
| Videon är klar | Händelse <br> Typ: Räknare | Definiera din egen händelse. |

### Mediemodulvariabler

| Milstolpe | Milstolpsyntax | Anpassad länk | Anpassad länksyntax |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | Ej tillämpligt | Mappning av kontextdata till eVars, props och händelser slutförs nu genom bearbetningsregler. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Valfria variabler

| Milstolpe | Milstolpsyntax | Anpassad länk | Anpassad länksyntax |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | Ej tillämpligt | Inte tillgängligt. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | Ej tillämpligt | Inte tillgängligt. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | Ej tillämpligt | Inte tillgängligt. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | Ej tillämpligt | Inte tillgängligt. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Ange eVar- eller kontextdatavariabeln i länkanropet. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | Ej tillämpligt | Inte tillgängligt. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | Ej tillämpligt | Inte tillgängligt. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | Ej tillämpligt | Inte tillgängligt. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | Ej tillämpligt | Inte tillgängligt. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | Ej tillämpligt | Inte tillgängligt. |

### Värdspårningsvariabler

| Milstolpe | Milstolpsyntax | Anpassad länk | Anpassad länksyntax |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | Ej tillämpligt | Inte tillgängligt. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | Ej tillämpligt | Inte tillgängligt. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | Ej tillämpligt | Inte tillgängligt. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | Ej tillämpligt | Inte tillgängligt. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | Ej tillämpligt | Inte tillgängligt. |

### Metoder för mediemodul

| Milstolpe | Milstolpsyntax | Anpassad länk | Anpassad länksyntax |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`: (obligatoriskt) Namnet på videon som du vill att den ska visas i videorapporter. | Ange eVar- eller kontextdatavariabeln i länkanropet. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`: (obligatoriskt) Videons längd i sekunder. | Ange eVar- eller kontextdatavariabeln i länkanropet. | `s.contextData['video.length']` <br> `  = ”90”;` |
| mediaPlayerName | `mediaPlayerName`: (obligatoriskt) Namnet på den mediaspelare som används för att visa videon, som du vill att den ska visas i videorapporter. | Ange eVar- eller kontextdatavariabeln i länkanropet. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | Ej tillämpligt | Inte tillgängligt. |
| name | `name`: (obligatoriskt) Namn eller ID för annonsen. | Ej tillämpligt | Inte tillgängligt. |
| length | `length`: (krävs) Annonsens längd. | Ej tillämpligt | Inte tillgängligt. |
| playerName | `playerName`: (obligatoriskt) Namnet på mediaspelaren som används för att visa annonsen. | Ej tillämpligt | Inte tillgängligt. |
| parentName | `parentName`: Namnet eller ID för det primära innehållet där annonsen bäddas in. | Ej tillämpligt | Inte tillgängligt. |
| parentPod | `parentPod`: Positionen i det primära innehållet som annonsen spelades upp. | Ej tillämpligt | Inte tillgängligt. |
| parentPodPosition | `parentPodPosition`: Placeringen i den punkt där annonsen spelas upp. | Ej tillämpligt | Inte tillgängligt. |
| CPM | `CPM`: CPM eller krypterad CPM (förfixerad med ett &quot;~&quot;) som gäller för den här uppspelningen. | Ej tillämpligt | Inte tillgängligt. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | Använd ett anpassat länkanalysanrop för att spåra klick. |
| Media.close | `s.Media.close(mediaName)` | Ej tillämpligt | Inte tillgängligt. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | Ej tillämpligt | Inte tillgängligt. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | Ej tillämpligt | Inte tillgängligt. |
| Media.monitor | `s.Media.monitor(s, media)` | Ange eVar- eller kontextdatavariabeln i länkanropet. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | Ej tillämpligt | Inte tillgängligt. |

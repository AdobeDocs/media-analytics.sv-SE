---
title: Huvudinnehåll för live
description: Visa ett exempel på hur du spårar direktsänt innehåll med Media SDK.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
exl-id: f6a00ffd-da6a-4d62-92df-15d119cfc426
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Live-huvudinnehåll{#live-main-content}

## Scenario {#scenario}

I det här scenariot finns det en liveresurs utan annonser som spelas upp i 40 sekunder efter att liveströmmen anslutits.

| Utlösare | Heartbeat-metod | Nätverksanrop | Anteckningar   |
|---|---|---|---|
| Användaren klickar på **[!UICONTROL Play]** | `trackSessionStart` | Börja med Analytics-innehåll, starta pulsslagsinnehåll | Det kan vara en användare som klickar på **[!UICONTROL Play]** eller en automatisk uppspelningshändelse. |
| Den första bildrutan i mediet spelas upp. | `trackPlay` | Spela upp pulsslagsinnehåll | Den här metoden utlöser timern. Hjärtslag skickas var 10:e sekund så länge uppspelningen fortsätter. |
| Innehållet spelas upp. |  | Hjärtslag för innehåll |  |
| Sessionen är över. | `trackSessionEnd` |  | `SessionEnd` betyder slutet på en visningssession. Detta API måste anropas även om användaren inte använder mediet för att slutföra det. |

## Parametrar {#parameters}

Många av de värden du ser på Adobe Analytics Content Start Call visas även på Heartbeat Content Start Call. Du kommer också att se många andra parametrar som Adobe använder för att fylla i olika medierapporter i Adobe Analytics. Vi kommer inte att täcka alla här, bara de viktiga.

### Starta pulsslagsinnehåll

| Parameter | Värde | Anteckningar |
|---|---|---|
| `s:sc:rsid` | &lt;your Adobe=&quot;&quot; Report=&quot;&quot; Suite=&quot;&quot; ID=&quot;&quot;> |  |
| `s:sc:tracking_serve` | &lt;your Analytics=&quot;&quot; Tracking=&quot;&quot; Server=&quot;&quot; URL=&quot;&quot;> |  |
| `s:user:mid` | `s:user:mid` | Ska matcha mittvärdet på Adobe Analytics Content Start Call |
| `s:event:type` | &quot;start&quot; |  |
| `s:asset:type` | &quot;main&quot; |  |
| `s:asset:mediao_id` | &lt;your Media=&quot;&quot; Name=&quot;&quot;> |  |
| `s:stream:type` | live |  |
| `s:meta:*` | valfri | Anpassade metadata för mediet |

## Hjärtslag för innehåll {#content-heartbeats}

Under medieuppspelningen finns det en tidtagare som skickar en eller flera hjärtslag (eller punkter) var 10:e sekund för huvudinnehållet och varje sekund för annonser. Dessa hjärtslag innehåller information om uppspelning, annonser, buffring och ett antal andra saker. Det exakta innehållet i varje pulsslag ligger utanför det här dokumentets omfång. Det viktigaste att validera är att pulsslag utlöses konsekvent medan uppspelningen fortsätter.

I innehållets pulsslag kan du leta efter några specifika saker:

| Parameter | Värde | Anteckningar |
|---|---|---|
| `s:event:type` | &quot;play&quot; |  |
| `l:event:playhead` | &lt;playhead position=&quot;&quot;> t.ex. 50, 60, 70 | Detta bör återspegla spelhuvudets aktuella position. |

## Hearsbeat-innehåll slutfört {#heartbeat-content-complete}

Det kommer inte att ske något fullständigt anrop i det här scenariot, eftersom liveströmmen aldrig har slutförts.

## Värdeinställningar för spelhuvud

För LIVE-strömmar måste du ställa in spelhuvudet på en förskjutning från när programmeringen påbörjas, så att analytikerna i sin rapportering kan avgöra vid vilken tidpunkt användare ansluter sig och lämnar LIVE-strömmen i en 24-timmarsvy.

### Vid start

För LIVE-media måste du ange `l:event:playhead` till aktuell förskjutning i sekunder när en användare börjar spela upp strömmen. Detta är i motsats till VOD, där du ställer in spelhuvudet på &quot;0&quot;.

Exempel: en LIVE-direktuppspelningshändelse startar vid midnatt och pågår i 24 timmar (`a.media.length=86400`; `l:asset:length=86400`). Anta sedan att en användare börjar spela upp den LIVE-strömmen kl. 12:00. I det här scenariot bör du ange `l:event:playhead` till 43200 (12 timmar in i strömmen).

### Vid paus

Samma&quot;live playhead&quot;-logik som används i början av uppspelningen måste användas när en användare pausar uppspelningen. När användaren återgår till att spela upp LIVE-strömmen måste du ange `l:event:playhead`-värdet till den nya förskjutna spelhuvudspositionen, _inte_ till den punkt där användaren pausade LIVE-strömmen.

## Exempelkod {#sample-code}

![](assets/live-content-playback.png)

### Android

Här är den förväntade API-anropsordningen:

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
```

### iOS

Här är den förväntade API-anropsordningen:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

Här är den förväntade API-anropsordningen:

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

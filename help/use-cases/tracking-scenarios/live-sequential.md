---
title: Live Main Content with Sequential Tracking
description: Visa ett exempel på hur du spårar direktsänt innehåll med sekventiell spårning med Media SDK.
uuid: b03477b6-9be8-4b67-a5a0-4cef3cf262ab
exl-id: 277a72b8-453b-41e5-b640-65c43587baf8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---

# Live-huvudinnehåll med sekventiell spårning{#live-main-content-with-sequential-tracking}

## Scenario {#scenario}

I det här scenariot finns det en liveresurs utan annonser som spelas upp i 40 sekunder efter att liveströmmen anslutits.

Detta är samma scenario som [VOD-uppspelning utan annonser](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) scenario, men en del av innehållet stegas igenom och en sökning utförs från en punkt i huvudinnehållet till en annan.

| Utlösare | Heartbeat-metod |  Nätverksanrop  |  Anteckningar   |
| --- | --- | --- | --- |
| Användaren klickar [!UICONTROL Play] | trackSessionStart | Börja med Analytics-innehåll, starta pulsslagsinnehåll | Mätbiblioteket är ovetande om att det finns en förrollsannons, så dessa nätverksanrop är identiska med [VOD-uppspelning utan annonser](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| Den första bildrutan i innehållet spelas upp. | trackPlay | Spela upp pulsslagsinnehåll | När kapitelinnehåll spelas upp före huvudinnehållet startar Heartslag när kapitlet börjar. |
| Innehåll spelas upp |  | Hjärtslag för innehåll | Detta nätverksanrop är exakt detsamma som [VOD-uppspelning utan annonser](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| Session1 över (Episod1 avslutad) | trackComplete/trackSessionEnd | Hearsbeat-innehåll slutfört | Komplett innebär att session1 för det första avsnittet nåddes och sågs fullständigt. Innan du startar sessionen för nästa avsnitt måste den här sessionen avslutas. |
| Episod2 har startats (session2 har startats) | trackSessionStart | Start av pulsslaginnehåll för analysinnehåll | Detta beror på att användaren tittade på det första avsnittet och fortsatte att titta på ett annat avsnitt |
| Mediets första bildruta | trackPlay | Spela upp pulsslagsinnehåll | Den här metoden utlöser timern och från och med nu skickas hjärtslag var 10:e sekund så länge uppspelningen fortsätter. |
| Innehållsuppspelning |  | Hjärtslag för innehåll |  |
| Sessionen är över (avsnitt 2 har avslutats) | trackComplete/trackSessionEnd | Hearsbeat-innehåll slutfört | Komplett innebär att session 2 för det andra avsnittet nåddes och sågs fullständigt. Innan du startar sessionen för nästa avsnitt måste den här sessionen avslutas. |

## Parametrar {#parameters}

### Starta pulsslagsinnehåll

| Parameter | Värde | Anteckningar |
|---|---|---|
| `s:sc:rsid` | &lt;Your Adobe Report Suite ID> |  |
| `s:sc:tracking_serve` | &lt;Your Analytics Tracking Server URL> |  |
| `s:user:mid` | `s:user:mid` | Ska matcha mittvärdet på Adobe Analytics Content Start Call |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Your Media Name> |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` | *valfri* | Anpassade metadata för mediet |

## Spela upp pulsslagsinnehåll {#heartbeat-content-play}

Detta ska se ut nästan exakt som när du anropar Heartbeat Content Start, men med den största skillnaden i &quot;s&quot;:event:type&quot;-parameter. Alla parametrar bör fortfarande finnas här.

| Parameter | Värde | Anteckningar |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Hjärtslag för innehåll {#content-heartbeats}

Under medieuppspelningen finns det en tidtagare som skickar en eller flera hjärtslag var 10:e sekund för huvudinnehållet och varje sekund för annonser. Dessa hjärtslag innehåller information om uppspelning, annonser, buffring och ett antal andra saker. Det exakta innehållet i varje pulsslag ligger utanför det här dokumentets omfång. Det viktigaste att validera är att pulsslag utlöses konsekvent medan uppspelningen fortsätter.

I innehållets pulsslag kan du leta efter några specifika saker:

| Parameter | Värde | Anteckningar |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;playhead position=&quot;&quot;> t.ex. 50, 60, 70 | Detta bör återspegla spelhuvudets aktuella position. |

## Hearsbeat-innehåll slutfört {#heartbeat-content-complete}

När uppspelningen för ett visst avsnitt har slutförts (spelhuvudet korsar avsnittsgränsen) skickas ett anrop till funktionen Slutför pulsslagsinnehåll. Detta ser ut som andra Heartbeat-samtal, men kommer att innehålla några specifika saker:

| Parameter | Värde | Anteckningar |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Exempelkod {#sample-code}

![](assets/ios-live-noads-multiplesessions.png)

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
//    i.e., when there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing 1st episode/session.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2 /episode 2 of the same live stream.  
// There is no need to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 
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

// 5. Call trackSessionStart() when the playhead reaches a point that denotes the 
//    start of session 2 
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue similarly tracking further sessions in the live stream if required 
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
//    frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing the first 
//    episode/session. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 4. Call trackSessionEnd to end session 1 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Start tracking session 2 / episode 2 of the same live stream, No need to  
// reinstantiate mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 5. Call trackSessionStart when the playhead reaches a point that denotes  
//    start of session 2 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 6. Call trackPlay to start tracking session 2 playback 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 7. Call trackComplete when the playback reaches the end of session 2,  
//    i.e., when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 
 
// 8. Call trackSessionEnd to end the session 2 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```

### JavaScript

Här är den förväntade API-anropsordningen:

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of a session,  
//    i.e., whn playback completes and finishes playing the 1st episode/session. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2/episode 2 of the same live stream. There is no need  
// to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
var mediaInfo2 = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

var mediaMetadata2 = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes  
//    the start of session 2 
this._mediaHeartbeat.trackSessionStart(mediaInfo2, mediaMetadata2); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```

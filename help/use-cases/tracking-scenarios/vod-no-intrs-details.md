---
title: VOD Playback with No Ads
description: Se ett exempel på hur du spårar uppspelning i VOD som inte innehåller några annonser.
uuid: ee2a1b79-2c2f-42e1-8e81-b62bbdd0d8cb
exl-id: 9e2240f0-da8d-4dcc-9d44-0f121c60d924
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---

# VOD utan annonser{#vod-playback-with-no-ads}

## Scenario {#scenario}

Det här scenariot har en VOD-resurs utan annonser, som spelas upp en gång från början till slut.

| Utlösare | Heartbeat-metod | Nätverksanrop | Anteckningar   |
|---|---|---|---|
| Användaren klickar på **[!UICONTROL Play]** | `trackSessionStart` | Börja med Analytics-innehåll, starta pulsslagsinnehåll | Detta kan antingen vara en användare som klickar på Spela upp eller en automatisk uppspelningshändelse. |
| Mediets första bildruta | `trackPlay` | Spela upp pulsslagsinnehåll | Den här metoden utlöser timern och från och med nu skickas hjärtslag var 10:e sekund under hela uppspelningen. |
| Innehåll spelas upp |  | Hjärtslag för innehåll |  |
| Innehållet är färdigt | `trackComplete` | Passa upp innehållet fullständigt | *Fullständigt* innebär att slutet på spelhuvudet nåddes. |

## Parametrar {#parameters}

Många av de värden som du ser på startanrop för pulsslagsinnehåll visas också i Adobe Analytics `Content Start`-anrop. Det finns många parametrar som Adobe använder för att fylla i de olika medierapporter, men bara de viktigaste parametrarna visas i följande tabell:

### Start för pulsslagsinnehåll

| Parameter | Värde | Anteckningar   |
|---|---|---|
| `s:sc:rsid` | &lt;Ditt Adobe Report Suite-ID> |  |
| `s:sc:tracking_server` | &lt;URL för analysspårningsserver> |  |
| `s:user:mid` | måste anges | Ska matcha mittvärdet för anropet `Adobe Analytics Content Start`. |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Ditt medienamn> |  |
| `s:meta:*` | valfri | Anpassade metadata som är inställda på mediet. |

## Spela upp pulsslagsinnehåll {#heartbeat-content-play}

De här parametrarna ska se nästan identiska ut som anropet `Heartbeat Content Start`, men den största skillnaden är parametern `s:event:type`. Alla andra parametrar ska fortfarande finnas.

| Parameter | Värde | Anteckningar   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Innehållshjärtslag {#content-heartbeats}

Under medieuppspelning skickar en tidtagare minst ett pulsslag var 10:e sekund. Dessa hjärtslag innehåller information om uppspelning, annonser, buffring och så vidare. Det exakta innehållet i varje pulsslag ligger utanför det här dokumentets räckvidd, men det kritiska problemet är att pulsslag utlöses konsekvent medan uppspelningen fortsätter.

I innehållets pulsslag ska du leta efter följande parametrar:

| Parametrar | Värde | Anteckningar   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;playhead position> t.ex. 50,60,70 | Den här parametern återspeglar spelhuvudets aktuella position. |

## Passa upp innehållet fullständigt {#heartbeat-content-complete}

När uppspelningen har slutförts, vilket innebär att slutet av spelhuvudet nås, skickas ett `Heartbeat Content Complete`-anrop. Det här anropet ser ut som andra Heartbeat-anrop, men innehåller några specifika parametrar:

| Parametrar | Värde | Anteckningar   |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Exempelkod {#sample-code}

I det här scenariot är innehållet 40 sekunder långt. Den spelas upp tills slutet utan några avbrott.

![](assets/main-content-regular-playback.png)

### Android

```java
// Set up  mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay  
//    is used, i.e., there's an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts,  
//    i.e., the first frame of media is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when the playback session ends prior to the  
//    media completing to the finish. This method must be called when   
//    playback ends if the user does not watch the media to completion. When trackSessionEnd is used, trackComplete should not be called. 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// 4. Call trackComplete() when the playback reaches the end and   
//    completes, i.e., when the media finishes because it is played to completion. When trackComplete is used, trackSessionEnd does not need to be called.
_mediaHeartbeat.trackComplete(); 

........ 
........ 
```

### iOS

```
when the user clicks Play 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 

NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there's an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 

// 2. Call trackPlay when the playback actually starts, i.e., when the  
//    first frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end, i.e.,  
//    when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 

// 4. Call trackSessionEnd when the playback session is over. This method  
//    must be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME, Configuration.MEDIA_ID,  
Configuration.MEDIA_LENGTH,MediaHeartbeat.StreamType.VOD); 
var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 

}; 

// 1. Call trackSessionStart() when the user clicks play, or when autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the main content starts, i.e.,  
//    the first frame of the media content is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end,  
    i.e., the media completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not  
//    watch the media to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........
```

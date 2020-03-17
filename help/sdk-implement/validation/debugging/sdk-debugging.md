---
title: SDK-felsökning
description: I det här avsnittet beskrivs spårning/loggning som är tillgänglig i Media SDK.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# SDK-felsökning{#sdk-debugging}

Du kan aktivera och inaktivera loggning. Media SDK har en omfattande funktion för spårning/loggning i hela mediespårningsstacken. Du kan aktivera eller inaktivera loggning genom att ange `debugLogging` flaggan för Config-objektet.

## Exempelkod för felsökningsloggning

### Android

```java
// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
config.debugLogging = true; 

// Use this space for setting other config values 
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config); 
```

### iOS

```
// Media Heartbeat Initialization 
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
config.debugLogging = YES; 

// Use this space for setting other config values 
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
```

### JavaScript

```js
// Media Heartbeat initialization 
var mediaConfig = new MediaHeartbeatConfig(); 
mediaConfig.debugLogging = true; 
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
```

### OTT (kromecast, Roku)

ADBMomobile-biblioteket innehåller felsökningsloggning via `setDebugLogging` metoden. Felsökningsloggning bör anges till `false` för alla produktionsprogram.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Kromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Använda Adobe Bloodhound för att testa Chromecast-program

Under programutvecklingen kan du med Bloodhound visa serveranrop lokalt och eventuellt vidarebefordra data till Adobes samlingsservrar. Mer information om Bloodhound finns i följande handböcker:

* [Bloodhound 3.x for Mac](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/)
* [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

>[!IMPORTANT]
>
>Från och med den 30 april 2017 har Adobe Bloodhound solnedgångar. Från och med 1 maj 2017 kommer inga ytterligare förbättringar att göras och ingen ytterligare support för tekniker eller Adobe Expert Care kommer att ges.

## Loggmeddelanden

Loggmeddelanden har följande format:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **tidsstämpel:** Detta är den aktuella processortiden (tidszonsindelad för GMT)
* **nivå:** Det finns fyra definierade meddelandenivåer:
   * INFO - Vanligtvis indata från programmet (validera spelarens namn, video-ID etc.)
   * DEBUG - Felsökningsloggar som används av utvecklare för att felsöka mer komplexa problem
   * VARNING - Anger potentiella integrerings-/konfigurationsfel eller Heartbeats SDK-fel
   * FEL - Anger viktiga integreringsfel eller Heartbeats SDK-fel
* **tagg:** Namnet på den underkomponent som utfärdade loggmeddelandet (vanligtvis klassnamnet)
* **meddelande:** Det faktiska spårningsmeddelandet

Du kan använda loggutdata från Media SDK-biblioteket för att verifiera implementeringen. En bra strategi är att söka igenom loggarna efter strängen `#track`. Då markeras alla `track*()` anrop som görs av programmet.

Detta är till exempel vad loggarna som filtrerats efter `#track` kan se ut som:

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad() 
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart() 
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay() 
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart() 
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart() 
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete() 
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart() 
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause() 
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete() 
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```


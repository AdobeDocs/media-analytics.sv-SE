---
title: Uppdatera flera spelarlägen samtidigt
description: I det här avsnittet beskrivs funktionen Spårning av flera spelartillstånd.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: fdbb777547181422b81ff6f7874bec3d317d02e9
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---

# Spårning av flera spelarlägen

Ibland börjar och slutar två spelarlägen samtidigt eller slutet av ett läge också i början av ett annat läge, vilket visas i följande bild:

![Flera spelarlägen](assets/multiple-player-states.svg)

Den aktuella implementeringen tillåter båda scenarierna:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Detta kräver dock att du utfärdar flera `stateStart` och `stateEnd` händelser för att signalera flera samtidiga statusförändringar. Ett nytt `statesUpdate` händelsetypen har implementerats, vilket avslutar en lista med lägen och startar en lista med nya lägen.

Använda nya `statesUpdate` blir ovanstående lista över händelser:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Antalet anrop om tillståndsuppdateringar har reducerats från sex till tre för samma beteende. Den sista händelsen kunde också ha varit en enkel `stateEnd(fullScreen)`.

## API-implementering för Media Collection {#mpst-api}

Du kan använda API:t för Media Collection för att implementera flera spårningar av spelartillstånd.

### Exempel

Nedan visas ett exempel på en implementering av API:t för Media Collection för att spåra flera spelarlägen.

```
// statesUpdate (ex: mute and pictureInPicture are switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: mute and pictureInPicture are switched off, fullScreen is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ],
    "statesStart": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: fullScreen is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

## Media SDK-implementering

Det finns ingen Media SDK-implementering.

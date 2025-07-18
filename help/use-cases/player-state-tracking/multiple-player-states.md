---
title: Uppdatera flera spelarlägen samtidigt
description: I det här avsnittet beskrivs funktionen Spårning av flera spelartillstånd.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 7a512a81-a6d1-4d0c-a4fe-91e9b11419db
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Spårning av flera spelarlägen

Ibland börjar och slutar två spelarlägen samtidigt eller slutet av ett läge också i början av ett annat läge, vilket visas i följande bild:

![Flera spelarlägen](assets/multiple-player-states.png)

Den aktuella implementeringen tillåter båda scenarierna:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Detta kräver dock att du utfärdar flera `stateStart`- och `stateEnd`-händelser för att signalera flera samtidiga statusändringar. I
för att optimera det här vanliga beteendet har en ny `statesUpdate`-händelsetyp implementerats som avslutar en lista över lägen
och startar en lista med nya lägen.

Med den nya `statesUpdate`-händelsen blir listan över händelser ovan:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Antalet anrop om tillståndsuppdateringar har reducerats från sex till tre för samma beteende. Den sista händelsen
kan också ha varit en enkel `stateEnd(fullScreen)`.

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

## Implementering av SDK Media

Det finns ingen Media SDK-implementering.

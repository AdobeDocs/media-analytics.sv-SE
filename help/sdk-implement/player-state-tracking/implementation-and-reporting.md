---
title: Implementering och rapportering
description: I det här avsnittet beskrivs hur du implementerar funktionen för spårning av spelartillstånd, inklusive .
translation-type: tm+mt
source-git-commit: b0bfe74d1f6083e700dbf98f504a17518bd19ecb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Implementering och rapportering

Under en uppspelningssession måste varje lägesförekomst (från början till slut) spåras individuellt. Media SDK och Media Collection API innehåller nya spårningsmetoder för den här funktionen.

Media SDK innehåller två nya metoder för anpassad statusspårning:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


Media Collection API innehåller två nya händelser som har &quot;media.stateName&quot; som obligatorisk parameter:

`stateStart` och `stateEnd`

## Media SDK-implementering

Spelarstatus startar

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

Spelarstatus upphör

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## API-implementering för Media Collection

Spelarstatus startar

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

Spelarstatus upphör

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## Lägesmått

De mått som anges för varje enskilt tillstånd beräknas och överförs till Adobe Analytics som kontextdataparametrar och lagras för rapportändamål. Tre mätvärden är tillgängliga för varje läge:

* `a.media.states.(media.state.name).set = true` — Ange som true om läget ställdes in minst en gång per varje specifik uppspelning av en ström.
* `a.media.states.(media.state.name).count = 4` — Identifierar antalet förekomster av ett läge under varje enskild uppspelning av en ström
* `a.media.states.(media.state.name).time = 240` — Identifierar den totala lägeslängden i sekunder för varje enskild uppspelning av en ström

## Rapportering

Alla lägesvärden kan användas för alla rapportvisualiseringar eller -komponenter (segment, beräknade värden).
TBD - kontrollera källa/wiki för uppdaterad information - för skärmbild från AW

## Importera värden från spelaren till Adobe Experience Platform

Data som lagras i Analytics kan användas i alla syften och spelarstatusvärdena kan importeras till Adobe Experience Platform med hjälp av XDM och användas med kundreseanalys. Standardlägesegenskaperna har specifika egenskaper medan de anpassade lägena är egenskaper som är tillgängliga via anpassade händelser. Mer information finns i egenskapslistan för XDM-identiteter på ?LINK TO METRIC LIST?.

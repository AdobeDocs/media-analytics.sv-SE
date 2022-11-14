---
title: Implementering och rapportering
description: Läs om hur du implementerar funktionen för spårning av spelartillstånd, inklusive .
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---

# Implementering och rapportering

Under en uppspelningssession måste varje lägesförekomst (från början till slut) spåras individuellt. Media SDK och Media Collection API innehåller nya spårningsmetoder för den här funktionen.

Media SDK innehåller två nya metoder för anpassad statusspårning:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


API:t för Media Collection innehåller två nya händelser med `media.stateName` som den obligatoriska parametern:

`stateStart` och `stateEnd`

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

De mått som anges för varje enskilt tillstånd beräknas och skickas till Adobe Analytics som kontextdataparametrar och lagras för rapportering. Tre mätvärden är tillgängliga för varje läge:

* `a.media.states.[state.name].set = true` — Ange som true om läget ställdes in minst en gång per varje specifik uppspelning av en ström.
* `a.media.states.[state.name].count = 4` — Identifierar antalet förekomster av ett läge under varje enskild uppspelning av en ström
* `a.media.states.[state.name].time = 240` — Identifierar den totala lägeslängden i sekunder för varje enskild uppspelning av en ström

## Rapportering

Alla värden för spelartillstånd kan användas för alla rapportvisualiseringar som är tillgängliga i Analysis Workspace eller en komponent (segment, beräknade värden) när en rapportserie har aktiverats för spårning av spelartillstånd. De nya måtten kan aktiveras från Admin Console för varje enskild rapport med hjälp av inställningarna för medierapportering (Redigera inställningar > Mediehantering > Medierapportering).

![](assets/report-setup.png)

I arbetsytan Analytics (Analyser) finns alla nya egenskaper på mätpanelen. Du kan till exempel söka efter `full screen` för att visa helskärmsdata på mätpanelen.

![](assets/full-screen-report.png)

## Importera mätvärden från spelaren till Adobe Experience Platform

Data som lagras i Analytics kan användas i alla syften och spelarlägesstatistik kan importeras till Adobe Experience Platform med hjälp av XDM och användas med Customer Journey Analytics. Standardlägesegenskaperna har specifika egenskaper medan de anpassade lägena är egenskaper som är tillgängliga med anpassade händelser. Mer information om standardlägesegenskaperna finns i *Egenskapslista för XDM-identiteter* i [Parametrar för spelartillstånd](/help/implementation/variables/player-state-parameters.md) sida.

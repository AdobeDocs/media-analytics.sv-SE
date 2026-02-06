---
title: Lär dig mer om tidslinjer för mediespårning - sessionen användaren avbryter
description: Lär dig mer om spelhuvudets tidslinje och motsvarande � när en videosession avbryts. Läs mer om de olika åtgärderna och förfrågningarna.
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
exl-id: 0c6a89f4-7949-4623-8ed9-ce1d1547bdfa
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 5%

---

# Tidslinje 2 - sessionen användaren avbryter {#timeline--2-user-abandons-session}

## VOD, Pre-roll-reklam, midroll-ads-annonser, användare överger innehåll tidigt

I följande diagram visas spelhuvudets tidslinje och motsvarande tidslinje för en användares åtgärder. Nedan presenteras närmare uppgifter om varje åtgärd och de tillhörande ansökningarna.

![API-innehåll](assets/va_api_content_2.png)

![API-åtgärder](assets/va_api_actions_2.png)

## Åtgärdsinformation

### Åtgärd 1 - Starta session {#Action-1}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Knappen Spela upp automatiskt eller Spela upp nedtryckt | 0 | 0 | `/api/v1/sessions` |

Det här anropet signalerar _användarens avsikt att spela upp_ en video. Det returnerar ett sessions-ID ( `{sid}`) till klienten som används för att identifiera alla efterföljande spårningsanrop i sessionen. Spelarläget är inte&quot;uppspelning&quot; än, utan är i stället&quot;start&quot;.  Obligatoriska sessionsparametrar måste inkluderas i kartan `params` i begärandetexten.  I bakgrunden genererar det här samtalet ett Adobe Analytics-initieringssamtal. Mer information om sessioner finns i dokumentationen för Media Collection API.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "sessionStart",
    "params": {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Åtgärd 2 - Ping-timerstart {#Action-2}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen börjar pinga händelsetimer | 0 | 0 | |

Starta appens ping-timer. Den första ping-händelsen ska sedan utlösas 1 sekund om det finns annonser före rullning, annars 10 sekunder.

### Åtgärd 3 - annonsradbrytning - start {#Action-3}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra start av annonsbrytning före rullning | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Annonser före rullning måste spåras. Annonserna kan bara spåras inom en annonsbrytning.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### Åtgärd 4 - annonsstart {#Action-4}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra start av förrullningsannons nr 1 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

En 12-sekunders annons börjar.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### Åtgärd 5 - annonsmaterial {#Action-5}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 1 | 0 | `/api/v1/sessions/{sid}/events` |

Rita serverdelen var 1 sekund. (Efterföljande reklamskyltar visas inte av utrymmesskäl.)

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Åtgärd 6 - annonsen är klar {#Action-6}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra förrullad annons nr 1 slutförd | 12 | 0 | `/api/v1/sessions/{sid}/events` |

Den första pre-roll-annonsen är över.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Åtgärd 7 - Ad break complete {#Action-7}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra pre-roll ad break complete | 12 | 0 | `/api/v1/sessions/{sid}/events` |

Annonsbrytningen är över. Under reklampausen har spelaren förblivit&quot;uppspelad&quot;.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### Åtgärd 8 - Spela upp innehåll {#Action-8}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra uppspelningshändelse | 12 | 0 | `/api/v1/sessions/{sid}/events` |

Flytta spelaren till uppspelningsläget. Börja spåra uppspelningen av innehållet.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "play",
    "qoeData": {
        "bitrate": 10000
    }
}
```

### Åtgärd 9 - Ping {#Action-9}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 20 | 8 | `/api/v1/sessions/{sid}/events` |

Ringa backend var 10:e sekund.

```json
{
    "playerTime": {
        "playhead": 8,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Åtgärd 10 - Ping {#Action-10}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 30 | 18 | `/api/v1/sessions/{sid}/events` |

Ringa backend var 10:e sekund.

```json
{
    "playerTime": {
        "playhead": 18,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Åtgärd 11 - Fel {#Action-11}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Ett fel inträffar. Felinformation skickas. | 32 | 20 | `/api/v1/sessions/{sid}/events` |

```json
{
    "playerTime": {
        "playhead": 20,
        "ts": "<timestamp>"
    },
    "eventType": "error"
}
```

### Åtgärd 12 - Spela upp innehåll {#Action-12}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Programmet återställs från fel, användaren trycker på Spela upp | 37 | 20 | `/api/v1/sessions/{sid}/events` |

```json
{
    "playerTime": {
        "playhead": 18,
        "ts": "<timestamp>"
    },
    "eventType":"play",
    "qoeData": {
        "bitrate": 10000
    }
}
```

### Åtgärd 13 - Ping {#Action-13}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 40 | 28 | `/api/v1/sessions/{sid}/events` |

Ringa backend var 10:e sekund.

```json
{
    "playerTime": {
        "playhead": 28,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Åtgärd 14 - Annonsuppspelning - start {#Action-14}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra start av annonsbrytning mitt i rullen | 45 | 33 | `/api/v1/sessions/{sid}/events` |

Adress mellan rullar med 8 sekunders varaktighet: skicka `adBreakStart`.

```json
{
    "playerTime": {
        "playhead": 33,
        "ts": "<timestamp>"
    },
    "eventType":"adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### Åtgärd 15 - annonsstart {#Action-15}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra start av annonsering nr 1 i mellanrullning | 45 | 33 | `/api/v1/sessions/{sid}/events` |

Spåra annonsen i mellanrullen.

```json
{
    "playerTime": { "playhead": 33, "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Åtgärd 16 - Stäng app {#Action-16}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Användaren stänger appen. Appen avgör att användaren har övergett visningen och inte återgår till den här sessionen. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

Skicka `sessionEnd` till VA-serverdelen för att ange att sessionen ska stängas omedelbart, utan någon ytterligare bearbetning.

```json
{
    "playerTime": {
        "playhead": 33,
        "ts": "<timestamp>"
    },
    "eventType": "sessionEnd"
}
```

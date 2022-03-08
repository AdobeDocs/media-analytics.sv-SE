---
title: Lär dig mer om tidslinjer för Media Traking � View till slutet av innehållet
description: Gå djupare in på spelhuvudets tidslinje och motsvarande � åtgärder. Läs mer om de olika åtgärderna och deras medföljande förfrågningar.
uuid: 0ff591d3-fa99-4123-9e09-c4e71ea1060b
exl-id: 16b15e03-5581-471f-ab0c-077189dd32d6
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 88bf699cb5b0872cefa4d6a6609c74f8fa35189a
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 5%

---

# Tidslinje 1 – Visa till innehållets slut{#timeline-view-to-end-of-content}

## VOD, pre-roll ads, pausa, buffra, visa innehållet i slutet

I följande diagram visas spelhuvudets tidslinje och motsvarande tidslinje för en användares åtgärder. Nedan presenteras närmare uppgifter om varje åtgärd och de tillhörande ansökningarna.


![](assets/va_api_content.png)


![](assets/va_api_actions.png)


## Åtgärdsinformation

### Åtgärd 1 - Starta session {#Action-1}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Automatiskt uppspelad eller uppspelningsknappen nedtryckt börjar videoinläsningen. | 0 | 0 | `/api/v1/sessions` |

**Implementeringsinformation**

Dessa samtalssignaler _användarens avsikt att spela_ en video. <br/><br/>Det returnerar ett sessions-ID ( `{sid}`) till klienten som används för att identifiera alla efterföljande spårningsanrop i sessionen. Spelarläget är inte&quot;uppspelning&quot; än, utan är i stället&quot;start&quot;. <br/><br/>[Parametrar för obligatoriska sessioner ](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) måste inkluderas i `params` karta i begärandetexten. <br/><br/>I bakgrunden genererar det här samtalet ett Adobe Analytics-initieringssamtal.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0, ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR_TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
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
| Appen börjar pinga händelsetimer | 0 | 0 | `/api/v1/sessions/{sid}/events` |  |

**Implementeringsinformation**

Starta appens ping-timer. Den första ping-händelsen ska sedan utlösas 1 sekund om det finns annonser före rullning, annars 10 sekunder.

### Åtgärd 3 - annonsradbrytning - start {#Action-3}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra start av annonsbrytning före rullning | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Annonserna kan bara spåras inom en annonsbrytning.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
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

**Implementeringsinformation**

Börja spåra den första pre-roll-annonsen, som är 15 sekunder lång. Inkludera anpassade metadata med detta `adStart` .

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: &lt;timestamp&gt;
    },
    eventType:adStart,
    params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement"
    },
    customMetadata: {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

**OBS! Mellan AdBreakStart- och AdStart-händelser ska det inte finnas några ytterligare uppspelningshändelser.**

### Åtgärd 5 - annonsmaterial {#Action-5}

#### Action 5.1 - Ad ping 1 {#Action-5-1}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Pinga serverdelen var 1 sekund medan du är inne i en annons.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

#### Action 5.2 - Ad ping 2 {#Action-5-2}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 2 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Pinga serverdelen var 1 sekund medan du är inne i en annons.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

#### Action 5.3 - Ad ping 3 {#Action-5-3}


| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 3 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Pinga serverdelen var 1 sekund medan du är inne i en annons.

>[!NOTE]
>
>Efterföljande annonser i tidslinjen kommer inte att visa serien med ensekunders ping
>i fortsättningens intresse...

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Åtgärd 6 - annonsen är klar {#Action-6}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra förrullad annons nr 1 slutförd | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Spåra slutet av den första pre-roll-annonsen.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Åtgärd 7 - annonsstart {#Action-7}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra start av förrullningsannons nr 2 | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Spåra början av den andra pre-roll-annonsen, som är 7 sekunder lång.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Åtgärd 8 - Annonsmaterial {#Action-8}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 20 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Rita serverdelen var 1 sekund.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Åtgärd 9 - Ad complete {#Action-9}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra förrullningsannons nr 2 slutförd | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Spåra slutet av den andra pre-roll-annonsen.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Åtgärd 10 - Ad break complete {#Action-10}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra pre-roll ad break complete | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Annonsbrytningen är över. Under reklampausen har lekläget fortsatt att&quot;leka&quot;.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Åtgärd 11 - Spela upp innehåll {#Action-11}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra uppspelningshändelse | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Efter `adBreakComplete` -händelsen, placerar spelaren i uppspelningsläge med `play` -händelse.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### Åtgärd 12 - Ping {#Action-12}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Ringa backend var 10:e sekund.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Åtgärd 13 - Buffertstart {#Action-13}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Buffertstarthändelse inträffade | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Spåra spelarens förflyttning till buffringsläge.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    }, eventType:bufferStart
}
```

### Åtgärd 14 - Buffertslut {#Action-14}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Buffringen är avslutad, programmet spårar återanvändning av innehåll | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Buffringen slutar efter 3 sekunder, så ställ in spelaren i uppspelningsläge igen. Du måste skicka ytterligare en spårets uppspelningshändelse som slutar buffras.  **The `play` ring efter `bufferStart` infogar ett &quot;bufferEnd&quot;-anrop i bakänden,** så det finns inget behov av `bufferEnd` -händelse.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### Åtgärd 15 - Ping {#Action-15}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Ringa backend var 10:e sekund.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    }, eventType:ping
}
```

### Åtgärd 16 - annonsradbrytning - start {#Action-16}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra start av annonsbrytning mitt i rullen | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Adress mellan rullar med 8 sekunders varaktighet: skicka `adBreakStart` .

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart,
    params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 21
    }
}
```

### Åtgärd 17 - annonsstart {#Action-17}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra start av annonsering nr 3 i mellanrullning | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Spåra annonsen i mellanrullen.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Action 18 - Ad ping {#Action-18}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 50 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Ringa backend var 10:e sekund.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    }, eventType:ping
}
```

### Åtgärd 19 - Ad complete {#Action-19}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra annonsering nr 1 i mellanrullen slutförd | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Mittrollannonsen är färdig.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Åtgärd 20 - Ad break complete {#Action-20}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Spåra annonsbrytning mitt i rullen | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Annonsbrytningen är klar.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Åtgärd 21 - Ping {#Action-21}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Ringa backend var 10:e sekund.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Åtgärd 22 - Pausa {#Action-22}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Användaren klickade på paus | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Användarens åtgärd flyttar uppspelningsläget till &quot;pausad&quot;.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### Åtgärd 23 - Ping {#Action-23}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Ringa backend var 10:e sekund. Spelaren är fortfarande i buffertläge. användaren sitter fast vid 20 sekunders innehåll. Rensar...

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:ping
}
```

### Action 24 - Play {#Action-24}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Användaren tryckte på Spela upp för att återuppta huvudinnehållet | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Flytta uppspelningsläget till&quot;uppspelning&quot;.  **The `play` ring efter `pauseStart` infogar ett &quot;resume&quot;-anrop till back end,** så det finns inget behov av `resume` -händelse.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:play
}
```

### Åtgärd 25 - Ping {#Action-25}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Appen skickar ping-händelse | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Ringa backend var 10:e sekund.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    }, eventType:ping
}
```

### Åtgärd 26 - Sessionen slutförd {#Action-26}

| Åtgärd | Tidslinje för åtgärd (sekunder) | Spelhuvudsposition (sekunder) | Klientbegäran |
| --- | :---: | :---: | --- |
| Användaren har tittat klart på innehållet. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**Implementeringsinformation**

Skicka `sessionComplete` till serverdelen för att ange att användaren har tittat klart på hela innehållet.

**Exempelbegärandebrödtext**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    }, eventType:sessionComplete
}
```

>[!NOTE]
>
>**Hittar du inga händelser? -** Det finns inget uttryckligt stöd i Media Collection API för `seekStart` eller `seekComplete` händelser. Detta beror på att vissa spelare genererar ett mycket stort antal sådana händelser när slutanvändaren rensar, och att flera hundra användare enkelt kan tappa bort nätverksbandbredden för en backend-tjänst. Adobe kringgår explicit stöd för seek-händelser genom att beräkna pulsslagets varaktighet baserat på enhetens tidsstämpel i stället för spelhuvudets position.

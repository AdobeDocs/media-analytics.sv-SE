---
title: API för direktuppspelning av medietjänster - Slutpunkt för sessionsbegäran
description: Vilka är Media Collection API-sessionerna som begär slutpunktsparametrar och svar?
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# Sessionsbegäran{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI-parametrar

Ingen

## Begärandetext

Begärandetexten måste vara JSON och ha samma struktur som exempelbegärandetexten:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime` (obligatoriskt)
   * `playhead` - Om innehållet är live måste spelhuvudet vara den aktuella sekunden på dagen, 0 &lt;= spelhuvud &lt; 86400. Om innehållet spelas in måste spelhuvudet vara den aktuella sekunden av innehållet, 0 &lt;= spelhuvud &lt; innehållslängd. Värdet kan vara ett flyttal.
   * `ts` - Tidsstämpel; måste vara i millisekunder; UTC (Coordinated Universal Time).
* `eventType` (obligatoriskt)

  **Giltigt värde:** `sessionStart`
* `params` (obligatoriskt)
* `customMetadata` (valfritt)
* `qoeData` (valfritt)

## Svar

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

`Location:` header - `/api/v1/`-delen innehåller API-versionen. Delen efter `[…]sessions/` är sessions-ID.

## Svarskoder

| HTTP-svarskod | Beskrivning |
|---|---|
| 201 | Session skapad |
| 400 | Felaktig begäran |
| 500 | Serverfel |

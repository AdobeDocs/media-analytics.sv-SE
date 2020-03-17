---
title: Sessionsbegäran
description: null
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

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

* `playerTime` (Obligatoriskt)
   * `playhead` - Måste vara i sekunder, men det kan vara ett flytande objekt.
   * `ts` - Tidsstämpel. måste vara i millisekunder.
* `eventType` (Obligatoriskt)

   **Giltigt värde:**`sessionStart`
* `params` (Obligatoriskt)
* `customMetadata` (Valfritt)
* `qoeData` (Valfritt)

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

`Location:` header - `/api/v1/` Delen innehåller API-versionen. Delen efter `[…]sessions/` är sessions-ID.

## Svarskoder

| HTTP-svarskod | Beskrivning |
|---|---|
| 201 | Session skapad |
| 400 | Felaktig begäran |
| 500 | Serverfel |


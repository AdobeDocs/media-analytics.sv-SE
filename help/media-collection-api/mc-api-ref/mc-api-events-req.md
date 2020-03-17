---
title: Händelsebegäran
description: null
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Händelsebegäran{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URI-parameter

`sid`: Sessions-ID som returnerats från en [sessionsbegäran.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Begärandetext

Begärandetexten måste vara JSON och ha samma struktur som exempelbegärandetexten:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (Obligatoriskt)
   * `playhead` - Måste vara i sekunder, men det kan vara ett flytande objekt.
   * `ts` - Tidsstämpel. måste vara i millisekunder.
* `eventType` (Obligatoriskt)
* `params` (Valfritt)
* `customMetadata` (Valfritt) skicka endast med `adStart` och `chapterStart` händelsetyper)
* `qoeData` (Valfritt)

En lista över giltiga händelsetyper för den här versionen finns i [Händelsetyper och beskrivningar.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Annonsuppföljning -**Du kan bara spåra annonser inuti en`adBreak`*.
>
>I avsaknad av `adBreakStart` - och `adBreakComplete` &quot;bokstöd&quot; runt annonser, kommer `adStart` och `adComplete` händelser helt enkelt att ignoreras och motsvarande annonslängd kommer att spåras som innehållets längd. Detta kan ha en betydande inverkan på de aggregerade data som kommer att bli tillgängliga i Adobe Analytics.

## Svar

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## HTTP-svarskoder

| HTTP-svarskod | Beskrivning | Klientåtgärdsobjekt |
|---|---|---|
| **204** | **Inget innehåll.** Anropet <br/><br/>till pulsslag lyckades. | Ej tillämpligt |
| **400** | **Felaktig begäran.** Begäran <br/><br/>hade ett felaktigt format. | Kontrollera [JSON-valideringsscheman](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) för begärandetypen. |
| **404** | **Hittades inte.** Det <br/><br/>gick inte att hitta sessions-ID för mediesessionen i back end-tjänsten. | Klientprogrammet bör använda API:t för [sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) för att skapa en annan mediesession och rapportera spårning för den. |
| **410** | **Borta.** Mediesessionen <br/><br/>hittades i back-end-tjänsten, men klienten kan inte längre rapportera aktivitet på den. | Klientprogrammet bör använda API:t för [sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) för att skapa en annan mediesession och rapportera spårning för den. |
| **500** | **Serverfel** | Ej tillämpligt |


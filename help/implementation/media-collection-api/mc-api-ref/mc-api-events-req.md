---
title: API för direktuppspelad mediainsamling � händelsebegärandeslutpunkt
description: "Vad begär Media Collection API-händelser slutpunktsparametrar och svar?"
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 4%

---

# Händelsebegäran{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## URI-parameter

`sid`: Sessions-ID som returneras från en [Sessionsbegäran](mc-api-sessions-req.md).

## Begärandetext

Begärandetexten måste vara JSON och ha samma struktur som exempelbegärandetexten:

```json
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

En lista över giltiga händelsetyper för den här versionen finns på [Händelsetyper och beskrivningar.](mc-api-event-types.md)

>[!IMPORTANT]
>
>***Annonsuppföljning -**Du kan bara spåra annonser inuti en`adBreak`*.
>
>I avsaknad av `adBreakStart` och `adBreakComplete` &quot;bokstöd&quot; runt annonser, `adStart` och `adComplete` Händelser ignoreras helt enkelt och motsvarande annonslängd spåras som innehållets längd. Detta kan ha en betydande inverkan på de aggregerade data som kommer att bli tillgängliga i Adobe Analytics.

## Svar

```text
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
| **204** | **Inget innehåll.** <br/><br/>Anropet till pulsslag lyckades. | Ej tillämpligt |
| **400** | **Felaktig begäran.** <br/><br/>Begäran hade ett felaktigt format. | Kontrollera [JSON-valideringsscheman](mc-api-json-validation.md) för begärandetypen. |
| **404** | **Hittades inte.** <br/><br/>Sessions-ID:t för mediesessionen hittades inte i back end-tjänsten. | Klientprogrammet bör använda [Sessionsbegäran](mc-api-sessions-req.md) API för att skapa en annan mediesession och rapportera spårning för den. |
| **410** | **Borta.** <br/><br/>Mediesessionen hittades i back-end-tjänsten, men klienten kan inte längre rapportera aktivitet på den. | Klientprogrammet bör använda [Sessionsbegäran](mc-api-sessions-req.md) API för att skapa en annan mediesession och rapportera spårning för den. |
| **500** | **Serverfel** | Ej tillämpligt |

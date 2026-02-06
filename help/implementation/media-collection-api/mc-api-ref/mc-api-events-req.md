---
title: API för direktuppspelad mediainsamling � händelsebegärandeslutpunkt
description: Vilka är Media Collection API-händelserna som begär slutpunktsparametrar och svar?
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 1%

---

# Händelsebegäran{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## URI-parameter

`sid`: Sessions-ID som returnerats från en [sessionsbegäran](mc-api-sessions-req.md).

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

* `playerTime` (obligatoriskt)
   * `playhead` - Måste vara i sekunder, men det kan vara ett flyttal.
   * `ts` - Tidsstämpel; måste vara i millisekunder.
* `eventType` (obligatoriskt)
* `params` (valfritt)
* `customMetadata` (Valfritt; skicka endast med händelsetyperna `adStart` och `chapterStart`)
* `qoeData` (valfritt)

En lista över giltiga händelsetyper för den här versionen finns i [Händelsetyper och beskrivningar.](mc-api-event-types.md)

>[!IMPORTANT]
>
>***Annonsuppföljning -**&#x200B;Du kan bara spåra annonser inuti en`adBreak`*.
>
>Om `adBreakStart` och `adBreakComplete` &quot;bokstöd&quot; saknas runt annonser ignoreras `adStart`- och `adComplete`-händelser och motsvarande annonslängd spåras som innehållslängd. Detta kan ha en betydande inverkan på de aggregerade data som kommer att bli tillgängliga i Adobe Analytics.

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
| **400** | **Ogiltig begäran.** <br/><br/>Begäran hade ett felaktigt format. | Kontrollera [JSON-valideringsscheman](mc-api-json-validation.md) för begärandetypen. |
| **404** | **Hittades inte.** <br/><br/>Sessions-ID:t för mediesessionen hittades inte i back-end-tjänsten. | Klientprogrammet bör använda API:t för [sessionsbegäran](mc-api-sessions-req.md) för att skapa en annan mediesession och rapportera spårning för den. |
| **410** | **Borta.** <br/><br/>Mediesessionen hittades i back-end-tjänsten, men klienten kan inte längre rapportera aktivitet på den. | Klientprogrammet bör använda API:t för [sessionsbegäran](mc-api-sessions-req.md) för att skapa en annan mediesession och rapportera spårning för den. |
| **500** | **Serverfel** | Ej tillämpligt |

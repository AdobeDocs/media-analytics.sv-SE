---
seo-title: Översikt
title: Översikt
description: null
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
translation-type: tm+mt
source-git-commit: cebf5697e3746721d29bfaa5356d5a2748fea435

---


# Översikt{#overview}

Media Collection API är Adobes RESTful-alternativ till Media SDK på klientsidan. Med Media Collection API kan spelaren spåra ljud- och videohändelser med RESTful HTTP-anrop.

Media Collection API är i princip ett kort som fungerar som en serverversion av Media SDK. Detta innebär att vissa aspekter av Media SDK-dokumentationen också är relevanta för Media Collection API. Båda lösningarna använder till exempel samma [ljud- och videoparametrar](/help/metrics-and-metadata/audio-video-parameters.md), och de insamlade ljud- och videospårningsdata leder till samma [rapportering och analys.](/help/media-reports/media-reports-enable.md)

## Dataflöden för medieuppföljning {#media-tracking-data-flows}

En mediespelare som implementerar API:t för Media Collection gör RESTful API-spårningsanrop direkt till bakomliggande mediaspårningsserver, medan en spelare som implementerar Media SDK gör spårningsanrop till SDK API:er inuti spelarappen. En effekt av att anropa via webben är att spelaren som implementerar API:t för Media Collection måste hantera en del av bearbetningen som Media SDK hanterar automatiskt. (Information om implementering av [Media Collection.](mc-api-impl/mc-api-quick-start.md))

Spårningsdata som hämtas med Media Collection API skickas och bearbetas först annorlunda än spårningsdata som hämtas i en Media SDK-spelare, men samma bearbetningsmotor på baksidan används för båda lösningarna.

![](assets/col_api_overview_simple.png)

## API-översikt {#api-overview}

**URI:** Hämta den här från din Adobe-representant.

**HTTP-metod:** POST, med JSON-begärandetext.

### API-anrop {#mc-api-calls}

* **`sessions`-**Upprättar en session med servern och returnerar ett sessions-ID som används vid efterföljande`events`anrop. Din app anropar detta en gång i början av en spårningssession.

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-**Skickar mediespårningsdata.

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### Begärandetext {#mc-api-request-body}

```
{
    "playerTime": {
        "playhead": {playhead position in seconds},
        "ts": {timestamp in milliseconds}
    },
    "eventType": {event-type},
    "params": {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    },
    "qoeData" : {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    },
    "customMetadata": {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    }
}
```

* `playerTime` - Obligatoriskt för alla förfrågningar.
* `eventType` - Obligatoriskt för alla förfrågningar.
* `params` - Obligatorisk för vissa `eventTypes`: kontrollera [JSON-valideringsschemat](mc-api-ref/mc-api-json-validation.md) för att avgöra vilka eventTypes som är obligatoriska och vilka som är valfria.

* `qoeData` - Valfritt för alla förfrågningar.
* `customMetadata` - Valfritt för alla förfrågningar, men bara för att skickas med `sessionStart`-, `adStart`och `chapterStart` händelsetyper.

För var `eventType`och en finns ett öppet [JSON-valideringsschema](mc-api-ref/mc-api-json-validation.md) som du bör använda för att verifiera parametertyper och om en parameter är valfri eller nödvändig för en viss händelse.

### Händelsetyper {#mc-api-event-types}

* `sessionStart`
* `play`
* `ping`
* `pauseStart`
* `bufferStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakStart`
* `adBreakComplete`
* `chapterStart`
* `chapterSkip`
* `chapterComplete`
* `sessionEnd`
* `sessionComplete`

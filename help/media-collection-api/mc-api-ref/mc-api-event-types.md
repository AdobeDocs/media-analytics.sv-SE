---
title: Händelsetyper och beskrivningar
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Händelsetyper och beskrivningar{#event-types-and-descriptions}

## sessionStart

Skickat med `sessions` samtalet. När svaret returneras extraherar du sessions-ID från platshuvudet och använder det för efterföljande händelseanrop till samlingsservern.

## play

Skickas när spelaren ändrar läge till&quot;uppspelning&quot; från ett annat läge (d.v.s. återanropet aktiveras av spelaren). `on('Playing')` Andra lägen från vilka spelaren går till&quot;uppspelning&quot; är&quot;buffring&quot;, användaren återupptog från&quot;pausad&quot;, spelaren återställdes från ett fel, automatisk uppspelning osv.

## ping

* **Huvudinnehåll -** Måste skickas var 10:e sekund under uppspelning av huvudinnehåll, oavsett andra API-händelser som har skickats. Den första ping-händelsen ska utlösas 10 sekunder efter att uppspelningen av huvudinnehållet har startat.
* **Annonsinnehåll -** Måste skickas var 1 sekund under annonsspårning.

Ping-händelser ska *inte* innehålla `params` kartan i begärandetexten.

## bitrateChange

Skickas när skiljeförfarandet ändras.

## bufferStart

Skickas när buffringen startar. Det finns ingen `bufferResume` händelsetyp. En `bufferResume` bild visas när du skickar en `play` händelse efter `bufferStart`.

## pauseStart

Skickas när användaren trycker på Paus. Det finns ingen `resume` händelsetyp. En bild `resume` härleds när du skickar en `play` händelse efter en `pauseStart`.

## adBreakStart

Signalerar början av en annonsbrytning

## adStart

Signalerar början av en annons

## adComplete

Signalerar slutförandet av en annonsbrytning

## adSkip

Signalerar en annons

## adBreakComplete

Signalerar slutförandet av en annonsbrytning

## chapterStart

Signalerar början av ett kapitelsegment

## kapitelSkip

Signalerar ett kapitelhopp

## chapterComplete

Signalerar slutförandet av ett kapitel

## fel

Signalerar att ett fel har inträffat.

## sessionEnd

Detta används för att meddela Media Analytics-backend-objektet att omedelbart stänga sessionen när användaren har avbrutit sin visning av innehållet och det är osannolikt att de kommer att returnera det.

Om du inte skickar en `sessionEnd`session tar en övergiven session normalt slut (efter att inga händelser har tagits emot under 10 minuter eller när ingen spelhuvudrörelse inträffar under 30 minuter) och sessionen tas bort av serverdelen.

## sessionComplete

Skickas när slutet av huvudinnehållet nås

>[!IMPORTANT]
>
>Du bör läsa [JSON-valideringsscheman](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) för varje händelsetyp för att kontrollera att händelsens parametertyper och krav är korrekta.


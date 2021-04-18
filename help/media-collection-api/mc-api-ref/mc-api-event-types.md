---
title: Händelsetyper och beskrivningar
description: Händelsetyper och beskrivningar
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Händelsetyper och beskrivningar{#event-types-and-descriptions}

## sessionStart

Skickat med `sessions`-anropet. När svaret returneras extraherar du sessions-ID från platshuvudet och använder det för efterföljande händelseanrop till samlingsservern.

## play

Skickas när spelaren ändrar läge till&quot;uppspelning&quot; från ett annat läge (d.v.s. `on('Playing')`-återanropet aktiveras av spelaren). Andra lägen från vilka spelaren går till&quot;uppspelning&quot; är&quot;buffring&quot;, användaren återupptog från&quot;pausad&quot;, spelaren återställdes från ett fel, automatisk uppspelning osv.

## ping

* **Huvudinnehåll -** Måste skickas var 10:e sekund under uppspelning av huvudinnehåll, oavsett andra API-händelser som har skickats. Den första ping-händelsen ska utlösas 10 sekunder efter att uppspelningen av huvudinnehållet har startat.
* **Annonsinnehåll -** Måste skickas var 1 sekund under annonsspårning.

Ping-händelser ska *inte* innehålla `params`-kartan i begärandetexten.

## bitrateChange

Skickas när skiljeförfarandet ändras.

## bufferStart

Skickas när buffringen startar. Det finns ingen `bufferResume`-händelsetyp. En `bufferResume`-händelse härleds när du skickar en `play`-händelse efter `bufferStart`.

## pauseStart

Skickas när användaren trycker på Paus. Det finns ingen `resume`-händelsetyp. En `resume`-händelse härleds när du skickar en `play`-händelse efter en `pauseStart`.

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

Om du inte skickar en `sessionEnd` kommer en övergiven session att gå in i timeout (när inga händelser tas emot under 10 minuter eller när ingen spelhuvudrörelse sker under 30 minuter) och sessionen tas bort av serverdelen.

## sessionComplete

Skickas när slutet av huvudinnehållet nås

>[!IMPORTANT]
>
>Du bör läsa [JSON-valideringsscheman](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) för varje händelsetyp för att verifiera korrekta händelseparametertyper och -krav.

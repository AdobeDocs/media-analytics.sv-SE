---
title: Typer och beskrivningar av direktuppspelande mediahändelser
description: "Vad är händelsetyperna och beskrivningarna för Media Collection? "
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Händelsetyper och beskrivningar{#event-types-and-descriptions}

## sessionStart

Skickat med `sessions` ring. När svaret returneras extraherar du sessions-ID från platshuvudet och använder det för efterföljande händelseanrop till samlingsservern.

## play

Skickas när spelaren ändrar läge till &quot;spela upp&quot; från ett annat läge (dvs. `on('Playing')` återanrop aktiveras av spelaren). Andra lägen från vilka spelaren går till&quot;uppspelning&quot; är&quot;buffring&quot;, användaren återupptog från&quot;pausad&quot;, spelaren återställdes från ett fel, automatisk uppspelning osv.

## ping

* **Huvudinnehåll -** Måste skickas var 10:e sekund under uppspelning av huvudinnehåll, oavsett andra API-händelser som har skickats. Den första ping-händelsen ska utlösas 10 sekunder efter att uppspelningen av huvudinnehållet har startat.
* **Annonsinnehåll -** Måste skickas var 1 sekund under annonsspårning.

Ping-händelser bör *not* innehåller `params` karta i begärandetexten.

## bitrateChange

Skickas när skiljeförfarandet ändras.

## bufferStart

Skickas när buffringen startar. Det finns inga `bufferResume` händelsetyp. A `bufferResume` härleds när du skickar en `play` händelse efter `bufferStart`.

## pauseStart

Skickas när användaren trycker på Paus. Det finns inga `resume` händelsetyp. A `resume` härleds när du skickar en `play` händelse efter `pauseStart`.

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

Om du inte skickar en `sessionEnd`, går en övergiven session normalt ut (efter att inga händelser har tagits emot under 10 minuter eller när ingen spelhuvudrörelse inträffar under 30 minuter) och sessionen tas bort av serverdelen.

## sessionComplete

Skickas när slutet av huvudinnehållet nås

>[!IMPORTANT]
>
>Du bör läsa [JSON-valideringsscheman](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) för varje händelsetyp, verifiera korrekta händelseparametertyper och krav.

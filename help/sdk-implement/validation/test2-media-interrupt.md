---
title: Test 2 Medieavbrott
description: Lär dig mer om testet av mediefel som används vid validering.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Test 2: Avbrott av media{#test-media-interruption}

Det här testfallet validerar beteendet för mobilavbrott.

## Provningsförfarande

Du måste slutföra och registrera dessa uppgifter i följande ordning:

1. **Starta mediespelaren**

   När mediespelaren startas skickas följande samtal i följande ordning:

   1. Adobe Analytics (AppMeasurement) - start
   1. Starta Media Analytics (hjärtslag)
   1. Begärt Adobe Analytics Start-anrop om Media Analytics (hjärtslag)

   De två första anropen ovan innehåller ytterligare metadata och variabler. Information om anropsparametrar och metadata finns i [Testa samtalsinformation.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Det tredje anropet ovan talar om för Media Analytics-servern att Media SDK har begärt att Adobe Analytics Start-anropet (`pev2=ms_s`) ska skickas till Adobe Analytics-servern.

1. **Spela upp huvudinnehåll i minst 5 minuter utan avbrott**

   **Innehållsuppspelning**

   Under uppspelning av innehåll skickar Media SDK uppspelningsanrop (hjärtslag) till Media Analytics-servern var tionde sekund.

   Information om anropsparametrar och metadata finns i [Testa samtalsinformation.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Se även instruktionerna [Spåra annonser](/help/sdk-implement/track-ads/track-ads-overview.md) för din plattform för ytterligare information om dessa annonsanrop.

1. **Flytta programmet eller webbläsaren till bakgrunden**

   När appen körs i bakgrunden bör endast `main:pause` anrop skickas till Media Analytics-servern, med början från VHL version 1.6.6 och senare.

1. **Flytta tillbaka appen eller webbläsaren till förgrunden**

   Vid återgång från bakgrunden bör uppspelningen av innehållet återupptas.

1. **Spela upp mediematerial i minst 5 minuter utan avbrott**

   Information om anropsparametrar och metadata finns i [Information om testsamtal.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Stäng mediespelaren**

   Inga ytterligare spårningsanrop ska utlösas när mediespelaren stängs.

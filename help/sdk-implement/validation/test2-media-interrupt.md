---
title: Test 2 Medieavbrott
description: I det här avsnittet beskrivs det test för mediefel som används vid validering.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: cebf5697e3746721d29bfaa5356d5a2748fea435

---


# Test 2: Avbrott av media{#test-media-interruption}

Det här testfallet validerar beteendet för mobilavbrott.

## Provningsförfarande

Du måste slutföra och registrera dessa uppgifter i följande ordning:

1. **Starta mediespelaren**

   När mediespelaren startas skickas följande samtal i följande ordning:

   1. Adobe Analytics (AppMeasurement) - start
   1. Starta Media Analytics (hjärtslag)
   1. Start-anrop för Adobe Analytics (hjärtslag)
   De två första anropen ovan innehåller ytterligare metadata och variabler. Information om samtalsparametrar och metadata finns i [Testa samtalsinformation.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Det tredje anropet ovan talar om för Media Analytics-servern att Media SDK har begärt att Adobe Analytics Start Call (`pev2=ms_s`) ska skickas till Adobe Analytics-servern.

1. **Spela upp huvudinnehåll i minst 5 minuter utan avbrott**

   **Innehållsuppspelning**

   Under uppspelning av innehåll skickar Media SDK uppspelningsanrop (hjärtslag) till Media Analytics-servern var tionde sekund.

   Information om samtalsparametrar och metadata finns i [Testa samtalsinformation.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Mer information om dessa annonsanrop finns även i [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) -instruktionerna för plattformen.

1. **Flytta programmet eller webbläsaren till bakgrunden**

   Medan appen körs i bakgrunden bör endast `main:pause` anrop skickas till Media Analytics-servern, med början från VHL-version 1.6.6 och senare.

1. **Flytta tillbaka appen eller webbläsaren till förgrunden**

   Vid återgång från bakgrunden bör uppspelningen av innehållet återupptas.

1. **Spela upp mediematerial i minst 5 minuter utan avbrott**

   Information om anropsparametrar och metadata finns i [Information om provsamtal.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Stäng mediespelaren**

   Inga ytterligare spårningsanrop ska utlösas när mediespelaren stängs.

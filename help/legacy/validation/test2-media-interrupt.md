---
title: Test 2 - mediefel
description: Lär dig mer om testet av mediefel som används vid validering.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Test 2: Medieavbrott{#test-media-interruption}

Det här testfallet validerar beteendet för mobilavbrott.

## Provningsförfarande

Du måste slutföra och registrera dessa uppgifter i följande ordning:

1. **Starta mediespelaren**

   När mediespelaren startas skickas följande samtal i följande ordning:

   1. Adobe Analytics (AppMeasurement) - start
   1. Starta Media Analytics (hjärtslag)
   1. Begärt Adobe Analytics Start-anrop om Media Analytics (hjärtslag)

   De två första anropen ovan innehåller ytterligare metadata och variabler. Information om samtalsparametrar och metadata finns i [Testa samtalsinformation.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   Det tredje anropet ovan talar om för Media Analytics-servern att Media SDK har begärt att Adobe Analytics Start-anropet (`pev2=ms_s`) ska skickas till Adobe Analytics-servern.

1. **Spela upp huvudinnehåll i minst 5 minuter utan avbrott**

   **Innehållsuppspelning**

   Under uppspelning av innehåll skickar Media SDK uppspelningsanrop (hjärtslag) till Media Analytics-servern var tionde sekund.

   Information om samtalsparametrar och metadata finns i [Testa samtalsinformation.](/help/legacy/validation/test-call-details.md#play-main-content)

   Se även instruktionerna [Spåra annonser](/help/use-cases/track-ads/track-ads-overview.md) för din plattform för ytterligare information om dessa annonsanrop.

1. **Flytta programmet eller webbläsaren till bakgrunden**

   När appen körs i bakgrunden bör bara `main:pause` anrop skickas till Media Analytics-servern, med början från VHL-version 1.6.6 och senare.

1. **Flytta tillbaka appen eller webbläsaren till förgrunden**

   Vid återgång från bakgrunden bör uppspelningen av innehållet återupptas.

1. **Spela upp mediet med huvudinnehåll i minst 5 minuter utan avbrott**

   Information om anropsparametrar och metadata finns i [Information om testsamtal.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Stäng mediespelaren**

   Inga ytterligare spårningsanrop ska utlösas när mediespelaren stängs.

---
title: Spåra fel med JavaScript 3.x
description: I det här avsnittet beskrivs hur du implementerar felspårning med Media SDK i webbläsarprogram (JS).
translation-type: tm+mt
source-git-commit: 5f274452b9ff5770908f7e2e450935be572a22ea
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Spåra fel med JavaScript 3.x{#track-errors-on-javascript}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning för implementering i alla 3.x SDK:er. Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandböckerna här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Implementera felspårning

1. Spåra mediespelarfel:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>Spårning av mediespelarfel stoppar inte mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att ringa `trackSessionEnd` efter att du har anropat `trackError`.

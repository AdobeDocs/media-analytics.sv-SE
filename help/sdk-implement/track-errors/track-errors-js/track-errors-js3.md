---
title: Lär dig spåra fel med JavaScript 3.x
description: Lär dig hur du implementerar felspårning med Media SDK i webbläsarappar (JS).
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Spåra fel med JavaScript 3.x{#track-errors-on-javascript}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandböckerna här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Implementera felspårning

1. Spåra mediespelarfel:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>Spårning av mediespelarfel stoppar inte mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att anropa `trackSessionEnd` efter att du har anropat `trackError`.

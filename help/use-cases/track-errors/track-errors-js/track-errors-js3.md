---
title: Lär dig spåra fel med JavaScript 3.x
description: Lär dig hur du implementerar felspårning med Media SDK i webbläsarappar (JS).
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Spåra fel med JavaScript 3.x{#track-errors-on-javascript}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Implementera felspårning

1. Spåra mediespelarfel:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>Spårning av mediespelarfel kommer inte att stoppa mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter ska du kontrollera att mediespårningssessionen stängs genom att anropa `trackSessionEnd` efter att `trackError` har anropats.

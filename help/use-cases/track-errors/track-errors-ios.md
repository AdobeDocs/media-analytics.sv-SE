---
title: Lär dig spåra fel på iOS
description: Lär dig hur du implementerar felspårning med Media SDK på iOS.
uuid: 18ea93d3-5948-4375-bcdb-72309268e38d
exl-id: c4ce7092-a102-41da-80a6-a4359f925708
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Spåra fel i iOS{#track-errors-on-ios}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Implementera felspårning

1. Spåra mediespelarfel:

   ```
   - (void)onPlayerError:(NSNotification *)notification {
       [_mediaHeartbeat trackError:@"mediaoErrorId"];
   }
   ```

>[!NOTE]
>
>Spårning av mediespelarfel kommer inte att stoppa mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter ska du kontrollera att mediespårningssessionen stängs genom att anropa `trackSessionEnd` efter att `trackError` har anropats.

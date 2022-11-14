---
title: Lär dig spåra fel på Roku
description: Lär dig hur du implementerar felspårning med Media SDK på Roku.
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Spåra fel på Roku{#track-errors-on-roku}

Följande instruktioner ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
> Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Implementera felspårning

1. Spåra mediespelarfel:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(),
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>Spårning av mediespelarfel stoppar inte mediespårningssessionen. Om mediaspelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att anropa `trackSessionEnd` efter anrop `trackError`.

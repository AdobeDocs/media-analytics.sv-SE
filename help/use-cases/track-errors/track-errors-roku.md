---
title: Lär dig spåra fel på Roku
description: Lär dig hur du implementerar felspårning med Media SDK på Roku.
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Spåra fel på Roku{#track-errors-on-roku}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
> Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK.](/help/getting-started/download-sdks.md)

## Implementera felspårning

1. Spåra mediespelarfel:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(),
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>Spårning av mediespelarfel kommer inte att stoppa mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter ska du kontrollera att mediespårningssessionen stängs genom att anropa `trackSessionEnd` efter att `trackError` har anropats.

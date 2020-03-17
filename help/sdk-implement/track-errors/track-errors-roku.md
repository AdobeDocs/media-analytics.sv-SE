---
title: Spåra fel på Roku
description: I det här avsnittet beskrivs hur du implementerar felspårning med Media SDK på Roku.
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra fel på Roku{#track-errors-on-roku}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Implementera felspårning

1. Spåra mediespelarfel:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(), 
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>Spårning av mediespelarfel stoppar inte mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att ringa `trackSessionEnd` efter att du har anropat `trackError`.


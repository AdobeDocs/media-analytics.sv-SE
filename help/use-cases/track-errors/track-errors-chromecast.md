---
title: Lär dig spåra fel i Chromecast
description: Lär dig hur du implementerar felspårning med Media SDK på Chromecast.
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
exl-id: 513772c2-582d-4b4b-92ed-0c32b99d7fdc
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Spåra fel i Chromecast{#track-errors-on-chromecast}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK.](/help/getting-started/download-sdks.md)

## Implementera felspårning

1. Spåra mediespelarfel: [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Spårning av mediespelarfel kommer inte att stoppa mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter ska du kontrollera att mediespårningssessionen stängs genom att anropa `trackSessionEnd` efter att `trackError` har anropats.

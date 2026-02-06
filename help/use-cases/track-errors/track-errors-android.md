---
title: Lär dig spåra fel på Android
description: Läs om hur du implementerar felspårning med Media SDK på Android.
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
exl-id: 6c4f693d-45c0-4a9c-bda1-c8721afe31f5
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Spåra fel i Android{#track-errors-on-android}

Följande instruktioner ger vägledning vid implementering med 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK.](/help/getting-started/download-sdks.md)

1. Spåra mediespelarfel:

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID");
   }
   ```

>[!NOTE]
>
>Spårning av mediespelarfel kommer inte att stoppa mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter ska du kontrollera att mediespårningssessionen stängs genom att anropa `trackSessionEnd` efter att `trackError` har anropats.

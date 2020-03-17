---
title: Spåra fel på Android
description: I det här avsnittet beskrivs hur du implementerar felspårning med Media SDK på Android.
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra fel på Android{#track-errors-on-android}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

1. Spåra mediespelarfel:

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>Spårning av mediespelarfel stoppar inte mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att ringa `trackSessionEnd` efter att du har anropat `trackError`.


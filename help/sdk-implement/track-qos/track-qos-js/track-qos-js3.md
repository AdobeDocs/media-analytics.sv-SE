---
title: Spåra upplevelsekvalitet med JavaScript 3.x
description: I det här avsnittet beskrivs hur du implementerar upplevelsekvalitet (QoE, QoS) med Media SDK i webbläsarprogram med JavaScript 3x.
translation-type: tm+mt
source-git-commit: fa161e2d41629fdfe77100d87d6a44728e23d77f
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Spåra upplevelsekvalitet med JavaScript 3.x{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning för implementering i alla 3.x SDK:er. Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandböckerna här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Implementerings-QOE

1. Identifiera när bithastigheten ändras under medieuppspelning och skapa `qoeObject` instansen med hjälp av QoE-informationen.

   QoEObject-variabler:

   >[!TIP]
   >
   >Dessa variabler är bara obligatoriska om du tänker spåra QoS.

   | Variabel | Typ | Beskrivning |
   | --- | --- | --- |
   | `bitrate` | tal | Aktuell bithastighet |
   | `startupTime` | tal | Starttid |
   | `fps` | tal | FPS-värde |
   | `droppedFrames` | tal | Antal uteslutna bildrutor |

   Skapa QoE-objekt:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
   ```

1. När uppspelningen växlar bithastigheter anropar du `BitrateChange` händelsen i Media Heartbeat-instansen:

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >Uppdatera QoE-objektet och anropa bithastighetsändringshändelsen för varje bithastighetsändring. Detta ger de mest exakta QoE-data.

1. Se till att anropa `updateQoEObject()` metoden för att tillhandahålla den senaste QoE-informationen till SDK:n.
1. När mediespelaren stöter på ett fel och felhändelsen är tillgänglig för spelarens API använder du `trackError()` för att hämta felinformationen. (Se [Översikt](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Spårning av mediespelarfel stoppar inte mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att ringa `trackSessionEnd()` efter att du har anropat `trackError()`.

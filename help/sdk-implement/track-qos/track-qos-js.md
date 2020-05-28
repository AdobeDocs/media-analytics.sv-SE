---
title: Spåra upplevelsekvaliteten med JavaScript 2.x
description: I det här avsnittet beskrivs hur du implementerar upplevelsekvalitet (QoE, QoS) med Media SDK i webbläsarprogram med JavaScript 2.x.
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
translation-type: tm+mt
source-git-commit: b165c9d133637fd0f1c529a98a936f8f31b72465
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---


# Spåra upplevelsekvaliteten med JavaScript 2.x{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Implementera QOS

1. Identifiera när bithastigheten ändras under medieuppspelning och skapa `MediaObject` instansen med QoS-informationen.

   QoSObject-variabler:

   >[!TIP]
   >
   >Dessa variabler är bara obligatoriska om du tänker spåra QoS.

   | Variabel | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `bitrate` | Aktuell bithastighet | Ja |
   | `startupTime` | Starttid | Ja |
   | `fps` | FPS-värde | Ja |
   | `droppedFrames` | Antal uteslutna bildrutor | Ja |

   Skapa QoS-objekt:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>);
   ```

1. När uppspelningen växlar bithastigheter anropar du `BitrateChange` händelsen i Media Heartbeat-instansen:

   ```js
   _onBitrateChange = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject);
   };
   ```

   >[!IMPORTANT]
   >
   >Uppdatera QoS-objektet och anropa bithastighetsändringshändelsen för varje bithastighetsändring. Detta ger de mest exakta QoS-data.

1. Se till att den `getQoSObject()` metoden returnerar den senaste QoS-informationen.
1. När mediespelaren stöter på ett fel och felhändelsen är tillgänglig för spelarens API använder du `trackError()` för att hämta felinformationen. (Se [Översikt](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Spårning av mediespelarfel stoppar inte mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att ringa `trackSessionEnd()` efter att du har anropat `trackError()`.

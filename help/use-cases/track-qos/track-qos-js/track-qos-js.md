---
title: Lär dig att spåra Experience Quality med JavaScript 2.x
description: "Lär dig hur du implementerar kvalitetskontroll av upplevelser (QoE, QoS) med Media SDK i webbläsarappar med JavaScript 2.x."
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
exl-id: 5924eba4-15a9-405b-9a05-8a7308ddec47
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---

# Spåra upplevelsekvaliteten med JavaScript 2.x{#track-quality-of-experience-on-javascript}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Ladda ned SDK:er.](/help/getting-started/download-sdks.md)

## Implementera QOS

1. Identifiera när bithastigheten ändras under medieuppspelning och skapa `MediaObject` -instans med QoS-informationen.

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

1. När uppspelningen växlar bithastigheter anropar du `BitrateChange` i Media Heartbeat-instansen:

   ```js
   _onBitrateChange = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject);
   };
   ```

   >[!IMPORTANT]
   >
   >Uppdatera QoS-objektet och anropa bithastighetsändringshändelsen för varje bithastighetsändring. Detta ger de mest exakta QoS-data.

1. Se till att `getQoSObject()` returnerar den senaste QoS-informationen.
1. När mediespelaren påträffar ett fel och felhändelsen är tillgänglig för spelarens API använder du `trackError()` om du vill hämta felinformation. (Se [Ökning](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Spårning av mediespelarfel kommer inte att stoppa mediespårningssessionen. Om mediaspelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att anropa `trackSessionEnd()` efter anrop `trackError()`.

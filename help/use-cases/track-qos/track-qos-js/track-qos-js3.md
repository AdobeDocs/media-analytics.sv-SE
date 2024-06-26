---
title: Lär dig att spåra Experience Quality med JavaScript 3.x
description: "Lär dig hur du implementerar kvalitetskontroll av upplevelser (QoE, QoS) med Media SDK i webbläsarappar med JavaScript 3x."
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 1%

---

# Spåra upplevelsekvaliteten med JavaScript 3.x{#track-quality-of-experience-on-javascript}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandböckerna här: [Ladda ned SDK:er.](/help/getting-started/download-sdks.md)

## Implementera QOE

1. Identifiera när bithastigheten ändras under medieuppspelning och skapa `qoeObject` -instans med QoE-informationen.

   QoObject-variabler:

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

1. När uppspelningen växlar bithastigheter anropar du `BitrateChange` i Media Heartbeat-instansen:

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

1. Se till att ringa `updateQoEObject()` metod för att tillhandahålla den mest uppdaterade QoE-informationen till SDK.
1. När mediespelaren påträffar ett fel och felhändelsen är tillgänglig för spelarens API använder du `trackError()` om du vill hämta felinformation. (Se [Ökning](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Spårning av mediespelarfel kommer inte att stoppa mediespårningssessionen. Om mediaspelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att anropa `trackSessionEnd()` efter anrop `trackError()`.

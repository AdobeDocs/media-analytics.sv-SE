---
title: Lär dig hur du spårar upplevelsekvalitet på iOS
description: "Lär dig att implementera kvalitetskontroll av upplevelser (QoE, QoS) med Media SDK på iOS."
uuid: cae2c142-ed39-4234-a711-765dcabc5415
exl-id: 7f01e6eb-95bd-4e3d-93d0-8a2e68323313
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 3%

---

# Spåra upplevelsekvalitet på iOS{#track-quality-of-experience-on-ios}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Implementera QOS

1. Identifiera när bithastigheten ändras under medieuppspelning och skapa instansen `MediaObject` med QoS-informationen.

   QoSObject-variabler:

   | Variabel | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `bitrate` | Aktuell bithastighet | Ja |
   | `startupTime` | Starttid | Ja |
   | `fps` | FPS-värde | Ja |
   | `droppedFrames` | Antal uteslutna bildrutor | Ja |

   >[!TIP]
   >
   >Dessa variabler är bara obligatoriska om du tänker spåra QoS.

   Skapa QoS-objekt:

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE]
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. Kontrollera att metoden `getQoSObject` returnerar den senaste QoS-informationen.
1. När uppspelningen växlar bithastigheter anropar du händelsen `BitrateChange` i instansen Mediepulsslag:

   ```
   - (void)onBitrateChange:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil];
   }
   ```

   >[!IMPORTANT]
   >
   >Uppdatera QoS-objektet och anropa bithastighetsändringshändelsen för varje bithastighetsändring. Detta ger de mest exakta QoS-data.

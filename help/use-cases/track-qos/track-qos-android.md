---
title: Lär dig hur du spårar upplevelsekvalitet på Android
description: Lär dig hur du implementerar kvalitetskontroll av upplevelser (QoE, QoS) med Media SDK i Android.
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
exl-id: cee8b119-bca2-4a5c-8111-2b49f7eede66
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 3%

---

# Spåra upplevelsekvalitet på Android{#track-quality-of-experience-on-android}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK.](/help/getting-started/download-sdks.md)

## Implementera QoS

1. Identifiera när bithastigheten ändras under medieuppspelning och skapa instansen `MediaObject` med QoS-informationen.

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

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. Kontrollera att metoden `getQoSObject()` returnerar den senaste QoS-informationen.
1. När uppspelningen växlar bithastigheter anropar du händelsen `BitrateChange` i instansen Mediepulsslag:

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null);
   }
   ```

   >[!IMPORTANT]
   >
   >Uppdatera QoS-objektet och anropa bithastighetsändringshändelsen för varje bithastighetsändring. Detta ger de mest exakta QoS-data.

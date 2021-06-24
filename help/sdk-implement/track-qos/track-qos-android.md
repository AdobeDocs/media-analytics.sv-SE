---
title: Lär dig hur du spårar Experience Quality på Android
description: '"Lär dig hur du implementerar kvalitetskontroll av upplevelser (QoE, QoS) med Media SDK på Android."'
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
exl-id: cee8b119-bca2-4a5c-8111-2b49f7eede66
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 3%

---

# Spåra upplevelsekvalitet på Android{#track-quality-of-experience-on-android}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Implementera QoS

1. Identifiera när bithastigheten ändras under medieuppspelning och skapa `MediaObject`-instansen med QoS-informationen.

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

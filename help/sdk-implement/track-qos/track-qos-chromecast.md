---
title: Lär dig hur du spårar upplevelsekvalitet på Chromecast
description: '"Lär dig hur du implementerar kvalitetskontroll av upplevelser (QoE, QoS) med Media SDK på Chromecast."'
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---

# Spåra upplevelsekvalitet på Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Översikt {#overview}

Kvalitetsspårning innefattar QoS (Quality of Service) och felspårning, båda är valfria element och **krävs inte** för implementeringar av huvudmediespårning. Du kan använda mediespelarens API för att identifiera variabler som är relaterade till QoS och felspårning.

## Spelarhändelser {#player-events}

### Alla bithastighetsändringshändelser

* Skapa/uppdatera QoS-objektinstansen för uppspelningen `qosObject`
* Ring `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Vid spelarfel

Ring `trackError(“media error id”);`

## Implementera {#implement}

1. Identifiera när bithastigheten ändras under medieuppspelning och skapa `MediaObject`-instansen med QoS-informationen.

   **QoSObject-variabler:**

   >[!TIP]
   >
   >Dessa variabler är bara obligatoriska om du tänker spåra QoS.

   | Variabel | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `bitrate` | Aktuell bithastighet | Ja |
   | `startupTime` | Starttid | Ja |
   | `fps` | FPS-värde | Ja |
   | `droppedFrames` | Antal uteslutna bildrutor | Ja |

   **skapa QoS-objekt:** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. När uppspelningen växlar bithastigheter anropar du händelsen `BitrateChange` i instansen Mediepulsslag: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >Uppdatera QoS-objektet och anropa bithastighetsändringshändelsen för varje bithastighetsändring. Detta ger de mest exakta QoS-data.

1. Kontrollera att metoden `getQoSObject()` returnerar den senaste QoS-informationen.
1. När mediespelaren stöter på ett fel och felhändelsen är tillgänglig för spelarens API använder du `trackError()` för att hämta felinformationen. (Se [Översikt](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Spårning av mediespelarfel stoppar inte mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att anropa `trackSessionEnd()` efter att du har anropat `trackError()`.

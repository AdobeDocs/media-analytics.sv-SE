---
title: Lär dig hur du spårar upplevelsekvalitet på Chromecast
description: "Lär dig hur du implementerar kvalitetskontroll av upplevelser (QoE, QoS) med Media SDK på Chromecast."
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 2%

---

# Spåra upplevelsekvalitet på Chromecast{#track-quality-of-experience-on-chromecast}

Följande instruktioner ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Översikt {#overview}

Kvalitetsspårning innefattar QoS (Quality of Service) och felspårning, båda är valfria element och är **not** krävs för implementering av mediespårning. Du kan använda mediespelarens API för att identifiera variabler som är relaterade till QoS och felspårning.

## Spelarhändelser {#player-events}

### Alla bithastighetsändringshändelser

* Skapa/uppdatera QoS-objektinstansen för uppspelningen, `qosObject`
* Utlysning `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Vid spelarfel

Utlysning `trackError("media error id");`

## Implementera {#implement}

1. Identifiera när bithastigheten ändras under medieuppspelning och skapa `MediaObject` -instans med QoS-informationen.

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

   **Skapa QoS-objekt:** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10);
   ```

1. När uppspelningen växlar bithastigheter anropar du `BitrateChange` i Media Heartbeat-instansen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
   ```

   >[!IMPORTANT]
   >
   >Uppdatera QoS-objektet och anropa bithastighetsändringshändelsen för varje bithastighetsändring. Detta ger de mest exakta QoS-data.

1. Se till att `getQoSObject()` returnerar den senaste QoS-informationen.
1. När mediespelaren påträffar ett fel och felhändelsen är tillgänglig för spelarens API använder du `trackError()` om du vill hämta felinformation. (Se [Översikt](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Spårning av mediespelarfel stoppar inte mediespårningssessionen. Om mediaspelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att anropa `trackSessionEnd()` efter anrop `trackError()`.

---
title: Spåra upplevelsekvalitet på Chromecast
description: I det här avsnittet beskrivs hur du implementerar kvalitetsuppföljning av upplevelser (QoE, QoS) med Media SDK on Chromecast.
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra upplevelsekvalitet på Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Översikt {#overview}

Kvaliteten på upplevelsespårningen innefattar QoS (Quality of Service) och felspårning, båda är valfria element och behövs **inte** för implementering av huvudmediespårning. Du kan använda mediespelarens API för att identifiera variabler som är relaterade till QoS och felspårning.

## Spelarhändelser {#player-events}

### Alla bithastighetsändringshändelser

* Skapa/uppdatera QoS-objektinstansen för uppspelningen, `qosObject`
* Utlysning `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Vid spelarfel

Utlysning `trackError(“media error id”);`

## Implementera {#implement}

1. Identifiera när bithastigheten ändras under medieuppspelning och skapa `MediaObject` instansen med QoS-informationen.

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

1. När uppspelningen växlar bithastigheter anropar du `BitrateChange` händelsen i Media Heartbeat-instansen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >Uppdatera QoS-objektet och anropa bithastighetsändringshändelsen för varje bithastighetsändring. Detta ger de mest exakta QoS-data.

1. Se till att den `getQoSObject()` metoden returnerar den senaste QoS-informationen.
1. När mediespelaren stöter på ett fel och felhändelsen är tillgänglig för spelarens API använder du `trackError()` för att hämta felinformationen. (Se [Översikt](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Spårning av mediespelarfel stoppar inte mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter kontrollerar du att mediespårningssessionen stängs genom att ringa `trackSessionEnd()` efter att du har anropat `trackError()`.


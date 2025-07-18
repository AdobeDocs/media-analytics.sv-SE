---
title: Lär dig hur du spårar Experience-kvalitet på Roku
description: Lär dig hur du implementerar kvalitetskontroll av upplevelser (QoE, QoS) med Media SDK på Roku.
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a
exl-id: cd84c26d-ad91-4179-9532-83408030ff3e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 4%

---

# Spåra upplevelsekvaliteten på Roku{#track-quality-of-experience-on-roku}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK.](/help/getting-started/download-sdks.md)

## Implementera QOS

1. Identifiera när bithastigheten ändras under medieuppspelning och använd `mediaUpdateQoS`-API:t för att uppdatera QoS-informationen på Media SDK.

   QoSObject-variabler:

   >[!TIP]
   >
   >Dessa variabler är bara obligatoriska om du spårar QoS.

   | Variabel | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `bitrate` | Aktuell bithastighet | Ja |
   | `startupTime` | Starttid | Ja |
   | `fps` | FPS-värde | Ja |
   | `droppedFrames` | Antal uteslutna bildrutor | Ja |

   Exempel:

   ```
   bitrate = 200000
   fps = 0
   droppedFrames = 1
   startupTime = 2
   qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)
   
   ADBMobile().mediaUpdateQoS(qosinfo)
   ```

   <!--
    QoS object creation:

    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. När uppspelningen växlar bithastigheter anropar du `trackEvent(BitrateChange)` för att meddela Media SDK att bithastigheten har ändrats.

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >Du måste anropa `updateQoSObject` med det uppdaterade bithastighetsvärdet.

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```

    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. När mediespelaren stöter på ett fel och felhändelsen är tillgänglig för spelarens API använder du `trackError()` för att hämta felinformationen. (Se [Översikt](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Spårning av mediespelarfel kommer inte att stoppa mediespårningssessionen. Om mediespelarfelet förhindrar att uppspelningen fortsätter ska du kontrollera att mediespårningssessionen stängs genom att anropa `trackSessionEnd()` efter att `trackError()` har anropats.

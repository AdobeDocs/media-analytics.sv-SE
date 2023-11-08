---
title: Lär dig hur du spårar uppspelning på Roku
description: Lär dig implementera huvudspårning med Media SDK på Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c308dba2d7cf07b89bf124bd6e5f972c253c9f18
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# Spåra kärnuppspelning på Roku{#track-core-playback-on-roku}

I den här dokumentationen beskrivs spårning i version 2.x av SDK.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er](/help/getting-started/download-sdks.md)

1. **Inledande spårningsinställning**

   Identifiera när användaren aktiverar uppspelningsavsikten (användaren klickar på play och/eller autoplay är aktiverat) och skapar en `MediaObject` -instans.

   **`MediaObject`referens:**

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Videonamn | Ja |
   | `mediaid` | Unik identifierare för video | Ja |
   | `length` | Videolängd | Ja |
   | `streamType` | Strömtyp (se _StreamType-konstanter_ nedan) | Ja |
   | `mediaType` | Medietyp (se _MediaType-konstanter_ nedan) | Ja |

   **`StreamType`konstanter:**

   | Konstantnamn | Beskrivning   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Strömtyp för Video on Demand. |
   | `MEDIA_STREAM_TYPE_LIVE` | Strömtyp för LIVE-innehåll. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Strömtyp för LINEAR-innehåll. |
   | `MEDIA_STREAM_TYPE_AOD` | Strömtyp för ljud på begäran |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Strömtyp för ljudbok |
   | `MEDIA_STREAM_TYPE_PODCAST` | Strömtyp för Podcast |

   **`MediaType`konstanter:**

   | Konstantnamn | Beskrivning |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Medietyp för ljudströmmar. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Medietyp för videoströmmar. |

   **Skapa ett medieinformationsobjekt för video med VOD-innehåll:**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

   eller

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **Skapa ett medieinformationsobjekt för video med AOD-innehåll:**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>",
    "<MEDIA_ID>",
    600,
    ADBMobile().MEDIA_STREAM_TYPE_AOD,
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   eller

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **Bifoga metadata**

   Du kan också bifoga standard- och/eller anpassade metadataobjekt till spårningssessionen via kontextdatavariabler.

   * **Standardmetadata**

[Implementera standardmetadata i Roku](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

     >[!NOTE]
     >
     >Det är valfritt att bifoga standardmetadataobjektet för video till mediaobjektet.

   * **Anpassade metadata**

     Skapa ett variabelobjekt för de anpassade variablerna och fyll i med data för videon. Exempel:

     ```
     mediaContextData = {}
     mediaContextData["cmk1"] = "cmv1"
     mediaContextData["cmk2"] = "cmv2"
     ```

1. **Spåra avsikten att starta uppspelning**

   Om du vill börja spåra en mediesession ringer du `trackSessionStart` på Media Heartbeat-instansen:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >
   >Det andra värdet är det anpassade namnet på videometadataobjektet som du skapade i steg 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` spårar användarens avsikt att spela upp, inte början av uppspelningen. Detta API används för att läsa in videodata/metadata och för att beräkna QoS-måttet för tiden till start (tidsintervallet mellan `trackSessionStart` och `trackPlay`).

   >[!NOTE]
   >
   >Om du inte använder anpassade videometadata skickar du ett tomt objekt för `data` argument i `trackSessionStart`, vilket visas i kommenteringsraden i iOS-exemplet ovan.

1. **Spåra faktiskt uppspelningsstart**

   Identifiera händelsen från videospelaren i början av videouppspelningen, där videons första bildruta återges på skärmen, och anropa `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Uppdatera spelhuvudets värde**

   Meddela SDK när mediespelhuvudet ändras genom att anropa `mediaUpdatePlayhead` API. <br /> För video-on-demand (VOD) anges värdet i sekunder från mediaobjektets början. <br /> Om spelaren inte anger information om innehållets varaktighet för direktuppspelning kan värdet anges som antalet sekunder sedan midnatt UTC den dagen.

   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Tänk på följande när du anropar `mediaUpdatePlayhead` API:
   >* När du använder förloppsmarkörer krävs innehållets längd och spelhuvudet måste uppdateras som antal sekunder från början av medieobjektet, med början från 0.
   >* När du använder medie-SDK:er måste du anropa `mediaUpdatePlayhead` API minst en gång per sekund.


1. **Spåra uppspelningen**

   Identifiera händelsen från videospelaren för att slutföra videouppspelningen, där användaren har tittat på innehållet tills slutet, och anropa `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Spåra slutet av sessionen**

   Identifiera händelsen från videospelaren för borttagning/stängning av videouppspelningen, där användaren stänger videon och/eller videon är slutförd och har tagits bort, och anropa `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` markerar slutet av en videospårningssession. Om sessionen har bevakats till slutet, där användaren har tittat på innehållet till slutet, måste du se till att `trackComplete` anropas före `trackSessionEnd`. Övriga `track*` API-anrop ignoreras efter `trackSessionEnd`, förutom `trackSessionStart` för en ny videospårningssession.

1. **Spåra alla möjliga pausscenarier**

   Identifiera händelsen från videospelaren för paus och anrop av videon `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Pausa scenarier**

   Identifiera alla scenarier där videouppspelaren pausar och se till att `trackPause` anropas korrekt. Följande scenarier kräver alla ditt appsamtal `trackPause()`:

   * Användaren träffar uttryckligen paus i appen.
   * Spelaren försätts i pausläget.
   * (*Mobilappar*) - Användaren placerar programmet i bakgrunden, men du vill att sessionen ska vara öppen.
   * (*Mobilappar*) - Alla typer av systemavbrott inträffar som gör att ett program backjordas. Användaren får t.ex. ett samtal eller ett popup-fönster från ett annat program inträffar, men du vill att sessionen ska vara aktiv så att användaren kan återuppta videon från avbrottet.

1. Identifiera händelsen från spelaren för videouppspelning och/eller videouppspelning från paus och samtal `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Detta kan vara samma händelsekälla som användes i steg 4. Se till att varje `trackPause()` API-anrop har parats med följande `trackPlay()` API-anrop när videouppspelningen återupptas.

* Spårningsscenarier: [VOD-uppspelning utan annonser](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Exempelspelare som ingår i Roku SDK för ett fullständigt spårningsexempel.

---
title: Lär dig hur du spårar uppspelning på Roku
description: Lär dig implementera huvudspårning med Media SDK på Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# Spåra kärnuppspelning på Roku{#track-core-playback-on-roku}

Denna dokumentation beskriver spårning i version 2.x av SDK.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er](/help/getting-started/download-sdks.md)

1. **Inledande spårningsinställning**

   Identifiera när användaren aktiverar uppspelningsavsikten (användaren klickar på play och/eller autoplay är aktiverat) och skapar en `MediaObject`-instans.

   **`MediaObject`-referens:**

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

[Implementera standardmetadata på Roku](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

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

1. **Spåra avsikten att starta uppspelningen**

   Om du vill börja spåra en mediesession anropar du `trackSessionStart` på instansen för pulsslag i media:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >
   >Det andra värdet är det anpassade namnet på videometadataobjektet som du skapade i steg 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` spårar användarens avsikt att spela upp, inte början av uppspelningen. Det här API:t används för att läsa in videodata/metadata och för att uppskatta QoS-måttet för tid till start (tidslängden mellan `trackSessionStart` och `trackPlay`).

   >[!NOTE]
   >
   >Om du inte använder anpassade videometadata skickar du bara ett tomt objekt för argumentet `data` i `trackSessionStart`, vilket visas i den kommenterade utdataraden i iOS-exemplet ovan.

1. **Spåra faktiskt uppspelningsstart**

   Identifiera händelsen från videospelaren i början av videouppspelningen, där den första bildrutan i videon återges på skärmen, och anropa `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Uppdatera spelhuvudet**

   Meddela SDK om mediespelhuvudet ändras genom att anropa `mediaUpdatePlayhead`-API:t. <br /> För video-on-demand (VOD) anges värdet i sekunder från mediaobjektets början. <br /> Om spelaren inte anger information om innehållets varaktighet för direktuppspelning kan värdet anges som antalet sekunder sedan midnatt UTC den dagen.

   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Tänk på följande när du anropar API:t `mediaUpdatePlayhead`:
   >* När du använder förloppsmarkörer krävs innehållets längd och spelhuvudet måste uppdateras som antal sekunder från början av medieobjektet, med början från 0.
   >* När du använder medie-SDK:er måste du anropa `mediaUpdatePlayhead`-API:t minst en gång per sekund.


1. **Spåra uppspelningen**

   Identifiera händelsen från videospelaren för att slutföra videouppspelningen, där användaren har tittat på innehållet tills slutet och anropa `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Spåra slutet av sessionen**

   Identifiera händelsen från videospelaren för borttagning/stängning av videouppspelningen, där användaren stänger videon och/eller videon är slutförd och har tagits bort, och anropa `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` markerar slutet på en videospårningssession. Om sessionen har bevakats till att slutföras, där användaren har tittat på innehållet till slutet, kontrollerar du att `trackComplete` anropas före `trackSessionEnd`. Alla andra `track*` API-anrop ignoreras efter `trackSessionEnd`, förutom `trackSessionStart` för en ny videospårningssession.

1. **Spåra alla möjliga pausscenarier**

   Identifiera händelsen från videospelaren för att pausa videon och anropa `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Pausa scenarier**

   Identifiera alla scenarier i vilka videospelaren pausar och se till att `trackPause` anropas korrekt. Följande scenarier kräver att din app anropar `trackPause()`:

   * Användaren träffar uttryckligen paus i appen.
   * Spelaren försätts i pausläget.
   * (*Mobilappar*) - Användaren placerar programmet i bakgrunden, men du vill att sessionen ska vara öppen i appen.
   * (*Mobilappar*) - Alla typer av systemavbrott inträffar som gör att ett program backjordas. Användaren får t.ex. ett samtal eller ett popup-fönster från ett annat program inträffar, men du vill att sessionen ska vara aktiv så att användaren kan återuppta videon från avbrottet.

1. Identifiera händelsen från spelaren för videouppspelning och/eller videouppspelning från paus och anrop `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Detta kan vara samma händelsekälla som användes i steg 4. Kontrollera att varje `trackPause()` API-anrop är parat med ett följande `trackPlay()` API-anrop när videouppspelningen återupptas.

* Spåra scenarier: [VOD-uppspelning utan annonser](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Exempelspelare ingår i Roku SDK för ett komplett spårningsexempel.

---
title: Spåra kärnuppspelning i JavaScript
description: I det här avsnittet beskrivs hur du implementerar huvudspårning med Media SDK i webbläsarappar (JS).
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra kärnuppspelning i JavaScript{#track-core-playback-on-javascript}

>[!IMPORTANT]
>I den här dokumentationen beskrivs spårning i version 2.x av SDK. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er](/help/sdk-implement/download-sdks.md)

1. **Inledande spårningsinställning**

   Identifiera när användaren aktiverar uppspelningsavsikten (användaren klickar på play och/eller autoplay är aktiverat) och skapar en `MediaObject` instans.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Medienamn | Ja |
   | `mediaid` | Unik medieidentifierare | Ja |
   | `length` | Medielängd | Ja |
   | `streamType` | Strömtyp (se _StreamType-konstanter_ nedan) | Ja |
   | `mediaType` | Medietyp (se _MediaType-konstanter_ nedan) | Ja |

   **`StreamType`konstanter:**

   | Konstantnamn | Beskrivning |
   |---|---|
   | `VOD` | Strömtyp för Video on Demand. |
   | `LIVE` | Strömtyp för LIVE-innehåll. |
   | `LINEAR` | Strömtyp för LINEAR-innehåll. |
   | `AOD` | Strömtyp för ljud på begäran. |
   | `AUDIOBOOK` | Strömtyp för ljudbok. |
   | `PODCAST` | Strömtyp för Podcast. |

   **`MediaType`konstanter:**

   | Konstantnamn | Beskrivning |
   |---|---|
   | `Audio` | Medietyp för ljudströmmar. |
   | `Video` | Medietyp för videoströmmar. |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>, 
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **Bifoga metadata**

   Du kan också bifoga standard- och/eller anpassade metadataobjekt till spårningssessionen via kontextdatavariabler.

   * **Standardmetadata**

      [Implementera standardmetadata i JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Det är valfritt att bifoga standardmetadataobjektet till medieobjektet.

      * API-referens för metadata för media - [standardmetadatanycklar - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Se alla tillgängliga metadata här: Parametrar för [ljud och video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Anpassade metadata**

      Skapa ett variabelobjekt för de anpassade variablerna och fyll i med data för mediet. Exempel:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **Spåra avsikten att starta uppspelningen**

   Om du vill börja spåra en mediesession anropar du `trackSessionStart` instansen Mediepulsslag:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >Det andra värdet är det anpassade objektnamnet för metadata för media som du skapade i steg 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` spårar användarens avsikt att spela upp, inte början av uppspelningen. Detta API används för att läsa in data/metadata och för att beräkna QoS-måttet för tid till start (tidsintervallet mellan `trackSessionStart` och `trackPlay`).

   >[!NOTE]
   >
   >Om du inte använder anpassade metadata skickar du bara ett tomt objekt för argumentet i `data` `trackSessionStart`, vilket visas i den kommenterade utdataraden i iOS-exemplet ovan.

1. **Spåra faktiskt uppspelningsstart**

   Identifiera händelsen från mediespelaren i början av uppspelningen, där den första bildrutan i mediet återges på skärmen, och anropa `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Spåra slutförd uppspelning**

   Identifiera händelsen från mediespelaren för att slutföra uppspelningen, där användaren har tittat på innehållet tills slutet, och ring `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Spåra slutet av sessionen**

   Identifiera händelsen från mediespelaren för borttagning/stängning av uppspelningen, där användaren stänger mediet och/eller mediet har slutförts och har tagits bort, och ring `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markerar slutet av en spårningssession. Om sessionen slutfördes utan fel, där användaren tittade på innehållet tills slutet, måste du se till att `trackComplete` anropas före `trackSessionEnd`. Alla andra `track*` API-anrop ignoreras efter `trackSessionEnd`, förutom `trackSessionStart` för en ny spårningssession.

1. **Spåra alla möjliga pausscenarier**

   Identifiera händelsen från mediespelaren för att pausa och ringa `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Pausa scenarier**

   Identifiera alla scenarier där mediespelaren pausar och se till att `trackPause` anropas korrekt. Följande scenarier kräver alla ditt appsamtal `trackPause()`:

   * Användaren träffar uttryckligen paus i appen.
   * Spelaren försätts i pausläget.
   * (*Mobilappar*) - Användaren placerar programmet i bakgrunden, men du vill att sessionen ska vara öppen i appen.
   * (*Mobilappar*) - Alla typer av systemavbrott inträffar som gör att ett program backjordas. Användaren får t.ex. ett samtal eller ett popup-fönster från ett annat program inträffar, men du vill att sessionen ska vara aktiv så att användaren kan återuppta mediet från den punkt då det avbröts.

1. Identifiera händelsen från spelaren för uppspelning och/eller återupptagning från paus och samtal `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Detta kan vara samma händelsekälla som användes i steg 4. Se till att varje API-anrop `trackPause()` paras med ett följande API- `trackPlay()` anrop när uppspelningen återupptas.

* Spårningsscenarier: VOD- [uppspelning utan annonser](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Exempelspelare som ingår i JavaScript SDK för ett fullständigt spårningsexempel.


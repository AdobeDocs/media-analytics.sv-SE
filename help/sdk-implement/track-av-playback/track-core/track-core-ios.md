---
title: Spåra kärnuppspelning på iOS
description: I det här avsnittet beskrivs hur du implementerar huvudspårning med Media SDK på iOS.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra kärnuppspelning på iOS{#track-core-playback-on-ios}

>[!IMPORTANT]
>I den här dokumentationen beskrivs spårning i version 2.x av SDK. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er](/help/sdk-implement/download-sdks.md)

1. **Inledande spårningsinställning**

   Identifiera när användaren aktiverar uppspelningsavsikten (användaren klickar på play och/eller autoplay är aktiverat) och skapar en `MediaObject` instans.

   [createMediaObjectWithName API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Variabelnamn | Beskrivning | Obligatoriskt |
   |---|---|---|
   | `name` | Videonamn | Ja |
   | `mediaid` | Unik identifierare för video | Ja |
   | `length` | Videolängd | Ja |
   | `streamType` | Strömtyp (se _StreamType-konstanter_ nedan) | Ja |
   | `mediaType` | Medietyp (se _MediaType-konstanter_ nedan) | Ja |

   **`StreamType`konstanter:**

   | Konstantnamn | Beskrivning |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Strömtyp för Video on Demand |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Strömtyp för Live-innehåll |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Strömtyp för linjärt innehåll |
   | `ADBMediaHeartbeatStreamTypeAOD` | Strömtyp för ljud på begäran |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Strömtyp för ljudbok |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Strömtyp för Podcast |

   **`MediaType`konstanter:**

   | Konstantnamn | Beskrivning |
   |---|---|
   | `ADBMediaTypeAudio` | Medietyp för ljudströmmar. |
   | `ADBMediaTypeVideo` | Medietyp för videoströmmar. |

   Det allmänna formatet för att skapa `MediaObject`:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                                          mediaId:<MEDIA_ID> 
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE> 
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Bifoga metadata för video**

   Du kan också bifoga standard- och/eller anpassade videometadataobjekt till videospårningssessionen via kontextdatavariabler.

   * **Standardmetadata för video**

      * [Implementera standardmetadata på iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Metadataknappar för video**
         [iOS-metadatanycklar](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Se den omfattande listan med videometadata här: Parametrar för [ljud och video](/help/metrics-and-metadata/audio-video-parameters.md)
      >[!NOTE]
      >
      >Det är valfritt att bifoga standardmetadataobjektet för video till mediaobjektet.

   * **Anpassade metadata**

      Skapa ett variabelobjekt för de anpassade variablerna och fyll i med data för videon. Exempel:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Spåra avsikten att starta uppspelningen**

   Om du vill börja spåra en mediesession anropar du instansen Mediepulsslag `trackSessionStart` .

   >[!TIP]
   >
   >Det andra värdet är det anpassade namnet på videometadataobjektet som du skapade i steg 2.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` spårar användarens avsikt att spela upp, inte början av uppspelningen. Detta API används för att läsa in videodata/metadata och för att beräkna QoS-måttet för tid till start (tidsintervallet mellan `trackSessionStart` och `trackPlay`).

   >[!NOTE]
   >
   >Om du inte använder anpassade videometadata skickar du bara ett tomt objekt för argumentet i `data` `trackSessionStart`, vilket visas i den kommenterade utdataraden i iOS-exemplet ovan.

1. **Spåra faktiskt uppspelningsstart**

   Identifiera händelsen från videospelaren i början av videouppspelningen, där den första bildrutan i videon återges på skärmen, och anropa `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **Spåra slutförd uppspelning**

   Identifiera händelsen från videospelaren när videouppspelningen är klar, där användaren har tittat på innehållet tills slutet och ring `trackComplete`:

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **Spåra slutet av sessionen**

   Identifiera händelsen från videospelaren för borttagning/stängning av videouppspelningen, där användaren stänger videon och/eller videon är klar och har tagits bort, och anropa `trackSessionEnd`:

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markerar slutet av en videospårningssession. Om sessionen slutfördes utan fel, där användaren tittade på innehållet tills slutet, måste du se till att `trackComplete` anropas före `trackSessionEnd`. Alla andra `track*` API-anrop ignoreras efter `trackSessionEnd`, förutom `trackSessionStart` för en ny videospårningssession.

1. **Spåra alla möjliga pausscenarier**

   Identifiera händelsen från videospelaren för paus och anrop av videon `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **Pausa scenarier**

   Identifiera alla scenarier där videouppspelaren pausas och se till att det `trackPause` anropas korrekt. Följande scenarier kräver alla ditt appsamtal `trackPause()`:

   * Användaren träffar uttryckligen paus i appen.
   * Spelaren försätts i pausläget.
   * (*Mobilappar*) - Användaren placerar programmet i bakgrunden, men du vill att sessionen ska vara öppen i appen.
   * (*Mobilappar*) - Alla typer av systemavbrott inträffar som gör att ett program backjordas. Användaren får t.ex. ett samtal eller ett popup-fönster från ett annat program inträffar, men du vill att sessionen ska vara aktiv så att användaren kan återuppta videon från avbrottet.

1. Identifiera händelsen från spelaren för videouppspelning och/eller videouppspelning från paus och samtal `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >Detta kan vara samma händelsekälla som användes i steg 4. Se till att varje API-anrop `trackPause()` paras med ett följande API- `trackPlay()` anrop när videouppspelningen återupptas.

Mer information om hur du spårar uppspelning finns i följande:

* Spårningsscenarier: VOD- [uppspelning utan annonser](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Exempelspelare som ingår i iOS SDK för ett fullständigt spårningsexempel.

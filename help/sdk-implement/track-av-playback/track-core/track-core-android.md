---
title: Spåra kärnuppspelning på Android
description: I det här avsnittet beskrivs hur du implementerar huvudspårning med Media SDK på Android.
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra kärnuppspelning på Android{#track-core-playback-on-android}

>[!IMPORTANT]
>I den här dokumentationen beskrivs spårning i version 2.x av SDK. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken för Android här: [Hämta SDK:er](/help/sdk-implement/download-sdks.md)

1. **Inledande spårningsinställning**

   Identifiera när användaren aktiverar uppspelningsavsikten (användaren klickar på play och/eller autoplay är aktiverat) och skapar en `MediaObject` instans.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Medienamn | Ja |
   | `mediaId` | Unik medieidentifierare | Ja |
   | `length` | Medielängd | Ja |
   | `streamType` | Strömtyp (se _StreamType-konstanter_ nedan) | Ja |
   | `mediaType` | Medietyp (se _MediaType-konstanter_ nedan) | Ja |

   **`StreamType`konstanter:**

   | Konstantnamn | Beskrivning |
   |---|---|
   | `VOD` | Strömtyp för Video on Demand. |
   | `LIVE` | Direktuppspelningstyp för Live-innehåll. |
   | `LINEAR` | Strömtyp för linjärt innehåll. |
   | `AOD` | Strömtyp för ljud på begäran |
   | `AUDIOBOOK` | Strömtyp för ljudbok |
   | `PODCAST` | Strömtyp för Podcast |

   **`MediaType`konstanter:**

   | Konstantnamn | Beskrivning |
   |---|---|
   | `Audio` | Medietyp för ljudströmmar. |
   | `Video` | Medietyp för videoströmmar. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Bifoga metadata**

   Du kan också bifoga standard- och/eller anpassade metadataobjekt till spårningssessionen via kontextdatavariabler.

   * **Standardmetadata**

      [Implementera standardmetadata på Android](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >Det är valfritt att bifoga standardmetadataobjektet till medieobjektet.

      * API-referens för metadata för media - [standardmetadatanycklar - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Här finns en omfattande uppsättning videometadata: Parametrar för [ljud och video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Anpassade metadata**

      Skapa en ordlista för de anpassade variablerna och fyll i med data för mediet. Exempel:

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **Spåra avsikten att starta uppspelningen**

   Om du vill börja spåra en mediesession anropar du instansen Mediepulsslag `trackSessionStart` . Exempel:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >Det andra värdet är det anpassade objektnamnet för metadata för media som du skapade i steg 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` spårar användarens avsikt att spela upp, inte början av uppspelningen. Detta API används för att läsa in mediedata/metadata och för att beräkna QoS-måttet för tid till start (tidsintervallet mellan `trackSessionStart` och `trackPlay`).

   >[!NOTE]
   >
   >Om du inte använder anpassade mediametadata skickar du bara ett tomt objekt för det andra argumentet i `trackSessionStart`.

1. **Spåra faktiskt uppspelningsstart**

   Identifiera händelsen från mediespelaren i början av mediespelningen, där den första bildrutan i mediet återges på skärmen, och anropa `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **Spåra slutförd uppspelning**

   Identifiera händelsen från mediespelaren för att slutföra medieuppspelningen, där användaren har tittat på innehållet tills slutet, och ring `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **Spåra slutet av sessionen**

   Identifiera händelsen från mediespelaren för borttagning/stängning av mediespelningen, där användaren stänger mediet och/eller mediet är klart och har tagits bort, och ring `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markerar slutet på en mediaspårningssession. Om sessionen slutfördes utan fel, där användaren tittade på innehållet tills slutet, måste du se till att `trackComplete` anropas före `trackSessionEnd`. Alla andra `track*` API-anrop ignoreras efter `trackSessionEnd`, förutom `trackSessionStart` för en ny mediespårningssession.

1. **Spåra alla möjliga pausscenarier**

   Identifiera händelsen från mediespelaren för att pausa och ringa `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **Pausa scenarier**

   Identifiera alla scenarier där videouppspelaren pausas och se till att det `trackPause` anropas korrekt. Följande scenarier kräver alla ditt appsamtal `trackPause()`:

   * Användaren träffar uttryckligen paus i appen.
   * Spelaren försätts i pausläget.
   * (*Mobilappar*) - Användaren placerar programmet i bakgrunden, men du vill att sessionen ska vara öppen i appen.
   * (*Mobilappar*) - Alla typer av systemavbrott inträffar som gör att ett program backjordas. Användaren får t.ex. ett samtal eller ett popup-fönster från ett annat program inträffar, men du vill att sessionen ska vara aktiv så att användaren kan återuppta mediet från den punkt då det avbröts.

1. Identifiera händelsen från spelaren för uppspelning av media och/eller återupptagning av media från paus och samtal `trackPlay`.

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >Detta kan vara samma händelsekälla som användes i steg 4. Kontrollera att varje `trackPause()` API-anrop har parats med ett följande API- `trackPlay()` anrop när medieuppspelningen återupptas.

Mer information om hur du spårar uppspelning finns i följande:

* Spårningsscenarier: VOD- [uppspelning utan annonser](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Exempelspelare som ingår i Android SDK för ett fullständigt spårningsexempel.


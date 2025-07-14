---
title: Lär dig spåra uppspelning med JavaScript v3.x
description: Lär dig hur du implementerar huvudspårning med Media SDK i en webbläsare med JavaScript 3.x-appar.
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# Spåra kärnuppspelning med JavaScript 3.x{#track-core-playback-on-javascript}

Denna dokumentation behandlar spårning i version 3.x av SDK.

>[!IMPORTANT]
>
>Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er](/help/getting-started/download-sdks.md)

1. **Inledande spårningsinställning**

   Identifiera när användaren aktiverar uppspelningsavsikten (användaren klickar på play och/eller autoplay är aktiverat) och skapar en `MediaObject`-instans.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Variabelnamn | Typ | Beskrivning |
   | --- | --- | --- |
   | `name` | string | En sträng som inte är tom motsvarar medienamnet. |
   | `id` | string | En sträng som inte är tom och som betecknar en unik medieidentifierare. |
   | `length` | tal | Positivt tal som anger mediets längd i sekunder. Använd 0 om längden är okänd. |
   | `streamType` | string |   |
   | `mediaType` | | Typ av media (ljud eller video). |

   **`StreamType`konstanter:**

   | Konstantnamn | Beskrivning   |
   |---|---|
   | `VOD` | Strömtyp för Video on Demand. |
   | `AOD` | Strömtyp för ljud på begäran. |

   **`MediaType`konstanter:**

   | Konstantnamn | Beskrivning |
   |---|---|
   | `Audio` | Medietyp för ljudströmmar. |
   | `Video` | Medietyp för videoströmmar. |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **Bifoga metadata**

   Du kan också bifoga standardmetadata och/eller anpassade metadata till spårningssessionen via kontextdatavariabler.

   * **Standardmetadata**

     >[!NOTE]
     >
     >Det är valfritt att bifoga standardmetadata.

      * API-referens för metadata för media - [Standardmetadatanycklar - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

        Se den omfattande uppsättningen tillgängliga metadata här: [Ljud- och videoparametrar](/help/implementation/variables/audio-video-parameters.md)

   * **Anpassade metadata**

     Skapa ett variabelobjekt för de anpassade variablerna och fyll i med data för mediet. Exempel:

     ```js
     /* Set context data */
      var contextData = {};
     
      //Standard metadata
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
     
      //Custom metadata
      contextData["isUserLoggedIn"] = "false";
      contextData["tvStation"] = "Sample TV Station";
     ```

1. **Spåra avsikten att starta uppspelningen**

   Om du vill börja spåra en mediesession anropar du `trackSessionStart` på instansen för pulsslag i media:

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` spårar användarens avsikt att spela upp, inte början av uppspelningen. Det här API:t används för att läsa in data/metadata och för att uppskatta QoS-måttet för tid till start (tidsintervallet mellan `trackSessionStart` och `trackPlay`).

   >[!NOTE]
   >
   >Om du inte använder contextData skickar du ett tomt objekt för argumentet `data` i `trackSessionStart`.

1. **Spåra faktiskt uppspelningsstart**

   Identifiera händelsen från mediespelaren för början av uppspelningen, där den första bildrutan i mediet återges på skärmen, och anropa `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **Uppdatera spelhuvudet**

   Meddela SDK om mediespelhuvudet ändras genom att anropa `mediaUpdatePlayhead`-API:t. <br /> För video-on-demand (VOD) anges värdet i sekunder från mediaobjektets början. <br /> Om spelaren inte anger information om innehållets varaktighet för direktuppspelning kan värdet anges som antalet sekunder sedan midnatt UTC den dagen.

   ```
   tracker.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Tänk på följande när du anropar API:t `tracker.updatePlayhead`:
   >* När du använder förloppsmarkörer krävs innehållets längd och spelhuvudet måste uppdateras som antal sekunder från början av medieobjektet, med början från 0.
   >* När du använder medie-SDK:er måste du anropa `tracker.updatePlayhead`-API:t minst en gång per sekund.

1. **Spåra uppspelningen**

   Identifiera händelsen från mediespelaren för att slutföra uppspelningen, där användaren har tittat på innehållet tills slutet och anropa `trackComplete`:

   ```js
   tracker.trackComplete();
   ```

1. **Spåra slutet av sessionen**

   Identifiera händelsen från mediespelaren för borttagning/stängning av uppspelningen, där användaren stänger mediet och/eller mediet har slutförts och har tagits bort, och anropa `trackSessionEnd`:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markerar slutet på en spårningssession. Om sessionen har bevakats till att slutföras, där användaren har tittat på innehållet till slutet, kontrollerar du att `trackComplete` anropas före `trackSessionEnd`. Alla andra `track*` API-anrop ignoreras efter `trackSessionEnd`, förutom `trackSessionStart` för en ny spårningssession.

1. **Spåra alla möjliga pausscenarier**

   Identifiera händelsen från mediespelaren för att pausa och ringa `trackPause`:

   ```js
   tracker.trackPause();
   ```

   **Pausa scenarier**

   Identifiera alla scenarier där mediespelaren pausar och se till att `trackPause` anropas korrekt. Följande scenarier kräver att din app anropar `trackPause()`:

   * Användaren träffar uttryckligen paus i appen.
   * Spelaren försätts i pausläget.
   * (*Mobilappar*) - Användaren placerar programmet i bakgrunden, men du vill att sessionen ska vara öppen i appen.
   * (*Mobilappar*) - Alla typer av systemavbrott inträffar som gör att ett program backjordas. Användaren får t.ex. ett samtal eller ett popup-fönster från ett annat program inträffar, men du vill att sessionen ska vara aktiv så att användaren kan återuppta mediet från den punkt då det avbröts.

1. Identifiera händelsen från spelaren för uppspelning och/eller återupptagning från paus och anrop `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Detta kan vara samma händelsekälla som användes i steg 4. Se till att varje `trackPause()` API-anrop paras med ett följande `trackPlay()` API-anrop när uppspelningen återupptas.

* Spåra scenarier: [VOD-uppspelning utan annonser](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Exempelspelare ingår i JavaScript SDK för ett komplett spårningsexempel.

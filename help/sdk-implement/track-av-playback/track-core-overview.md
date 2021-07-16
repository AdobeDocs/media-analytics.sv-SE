---
title: Uppspelning av spårningsinnehåll förklaras
description: '"Läs om hur du spårar uppspelning, inklusive spårning av mediainläsning, mediestart, mediapaus och slutförda media. "'
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# Spårningsöversikt{#tracking-overview}

I den här dokumentationen beskrivs spårning i version 2.x av SDK.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Spelarhändelser

Spårning av huvuduppspelning inkluderar spårning av mediainläsning, mediestart, mediapaus och slutförda media. Även om det inte är obligatoriskt är spårning av buffring och sökning också viktiga komponenter som används för att spåra uppspelning av innehåll. Identifiera de spelarhändelser som motsvarar Media SDK-spårningsanrop i mediespelarens API, och koda händelsehanterarna för att anropa spårnings-API:er och för att fylla i obligatoriska och valfria variabler.

### Vid mediainläsning

* Skapa medieobjektet
* Fyll i metadata
* Ring `trackSessionStart`; Till exempel: `trackSessionStart(mediaObject, contextData)`

### Vid mediestart

* Ring `trackPlay`

### Vid paus/fortsätt

* Ring `trackPause`
* Ring `trackPlay`   _när uppspelningen återupptas_

### On media complete

* Ring `trackComplete`

### Vid medieavbrott

* Ring `trackSessionEnd`

### När snabbspolning startar

* Ring `trackEvent(SeekStart)`

### När snabbspolning slutar

* Ring `trackEvent(SeekComplete)`

### När buffring börjar

* Ring `trackEvent(BufferStart);`

### När buffring slutar

* Ring `trackEvent(BufferComplete);`

>[!TIP]
>
>Spelhuvudets position anges som en del av konfigurerings- och konfigurationskoden. Mer information om `getCurrentPlayheadTime` finns i [Översikt: Allmänna riktlinjer för implementering.](/help/sdk-implement/setup/setup-overview.md#general-implementation-guidelines)

## Implementera {#implement}

1. **Inledande spårningsinställning -** Identifiera när användaren aktiverar uppspelningen (användaren klickar på play och/eller autoplay är aktiverat) och skapa en  `MediaObject` instans med mediainformationen för innehållsnamn, innehålls-ID, innehållslängd och strömtyp.

   **`MediaObject`referens:**

   | Variabelnamn | Beskrivning | Obligatoriskt |
   |---|---|---|
   | `name` | Innehållsnamn | Ja |
   | `mediaid` | Unik identifierare för innehåll | Ja |
   | `length` | Innehållslängd | Ja |
   | `streamType` | Strömtyp | Ja |
   | `mediaType` | Medietyp (ljud- eller videoinnehåll) | Ja |

   **`StreamType`konstanter:**

   | Konstantnamn | Beskrivning |
   |---|---|
   | `VOD` | Strömtyp för Video on Demand. |
   | `LIVE` | Direktuppspelningstyp för Live-innehåll. |
   | `LINEAR` | Strömtyp för linjärt innehåll. |
   | `AOD` | Strömtyp för ljud on demand |
   | `AUDIOBOOK` | Strömtyp för ljudbok |
   | `PODCAST` | Strömtyp för Podcast |

   **`MediaType`konstanter:**

   | Konstantnamn | Beskrivning |
   |---|---|
   | `Audio` | Medietyp för ljudströmmar. |
   | `Video` | Medietyp för videoströmmar. |

   Det allmänna formatet för att skapa `MediaObject` är `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Bifoga metadata -** Du kan även bifoga standard- och/eller anpassade metadataobjekt till spårningssessionen via kontextdatavariabler.

   * **Standardmetadata -**

      >[!NOTE]
      >
      >Det är valfritt att bifoga standardmetadataobjektet till medieobjektet.

      Instansiera ett metadataobjekt av standardtyp, fyll i önskade variabler och ange metadataobjektet i objektet Mediepulsslag.

      Se den omfattande listan med metadata här: [Parametrar för ljud och video.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **Anpassade metadata -** Skapa ett variabelobjekt för de anpassade variablerna och fyll i med data för det här innehållet.

1. **Spåra avsikten att starta uppspelningen -** Om du vill börja spåra en session anropar du instansen  `trackSessionStart` av pulsslag i media.

   >[!IMPORTANT]
   >
   >`trackSessionStart` spårar användarens avsikt att spela upp, inte början av uppspelningen. Detta API används för att läsa in data/metadata och för att beräkna QoS-måttet för tid till start (tidslängden mellan `trackSessionStart` och `trackPlay`).

   >[!NOTE]
   >
   >Om du inte använder anpassade metadata skickar du ett tomt objekt för argumentet `data` i `trackSessionStart`.

1. **Spåra faktiskt uppspelningsstart -** Identifiera händelsen från mediespelaren för uppspelningens början, där den första bildrutan av innehållet återges på skärmen, och anropa  `trackPlay`.

1. **Spåra hela uppspelningen -** Identifiera händelsen från mediespelaren för att slutföra uppspelningen, där användaren har tittat på innehållet tills slutet och ringa  `trackComplete`.

1. **Spåra slutet av sessionen -** Identifiera händelsen från mediespelaren för borttagning/stängning av uppspelningen, där användaren stänger innehållet och/eller innehållet är slutfört och har tagits bort, och anropa  `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markerar slutet av en spårningssession. Om sessionen kunde bevakas tills det var klart, där användaren tittade på innehållet till slutet, kontrollerar du att `trackComplete` anropas före `trackSessionEnd`. Alla andra `track*` API-anrop ignoreras efter `trackSessionEnd`, förutom `trackSessionStart` för en ny spårningssession.

1. **Spåra alla möjliga pausscenarier -** Identifiera händelsen från mediespelaren för att pausa och ringa  `trackPause`.

   **Pausa scenarier -** Identifiera alla scenarier där spelaren pausar och se till att det  `trackPause` anropas korrekt. Följande scenarier kräver alla att ditt program anropar `trackPause()`:

   * Användaren träffar uttryckligen paus i appen.
   * Spelaren försätts i pausläget.
   * (*Mobilappar*) - Användaren placerar programmet i bakgrunden, men du vill att sessionen ska vara öppen i appen.
   * (*Mobilappar*) - Alla typer av systemavbrott inträffar som gör att ett program backoreras. Användaren får t.ex. ett samtal eller ett popup-fönster från ett annat program inträffar, men du vill att sessionen ska vara aktiv så att användaren kan återuppta innehållet från den punkt då det avbröts.

1. Identifiera händelsen från spelaren för uppspelning och/eller återupptagning från paus och ring `trackPlay`.

   >[!TIP]
   >
   >Detta kan vara samma händelsekälla som användes i steg 4. Kontrollera att varje `trackPause()` API-anrop är parat med följande `trackPlay()` API-anrop när uppspelningen återupptas.

1. Lyssna efter uppspelningssökningshändelser från mediespelaren. Spåra sökningen med händelsen `SeekStart` när du söker efter händelsemeddelanden.
1. Spåra slutet av sökningen med händelsen `SeekComplete` när du söker efter ett fullständigt meddelande från mediespelaren.
1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och spåra buffring med händelsen `BufferStart` vid meddelande om start av buffert.
1. Spåra slutet av buffringen med händelsen `BufferComplete` när ett meddelande om att bufferten har slutförts från mediespelaren.

Se exempel på varje steg i följande plattformsspecifika ämnen och titta på de exempelspelare som ingår i dina SDK:er.

Ett enkelt exempel på uppspelningsspårning finns i denna användning av JavaScript 2.x SDK i en HTML5-spelare:

```js
/* Call on media start */
if (e.type == "play") {

    // Check for start of media
    if (!sessionStarted) {
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>,
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/
        var mediaInfo = MediaHeartbeat.createMediaObject(
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration,
          MediaHeartbeat.StreamType.VOD);

        /* Set custom context data */
        var customVideoMetadata = {
            isUserLoggedIn: "false",
            tvStation: "Sample TV station",
            programmer: "Sample programmer"
        };

        /* Set standard video metadata */     
        var standardVideoMetadata = {};
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     

        // Start Session
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    

        // Track play
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     

    } else {
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    }
};

/* Call on video complete */
if (e.type == "ended") {
    console.log("video ended");
    this.mediaHeartbeat.trackComplete();
    this.mediaHeartbeat.trackSessionEnd();
    sessionStarted = false;     
};

/* Call on pause */
if (e.type == "pause") {
    this.mediaHeartbeat.trackPause();
};

/* Call on scrub start */
if (e.type == "seeking") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};

/* Call on scrub stop */
if (e.type == "seeked") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};

/* Call on buffer start */
if (e.type == “buffering”) {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};

/* Call on buffer complete */
if (e.type == “buffered”) {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

## Validera {#validate}

Information om hur du validerar implementeringen finns i [Validering.](/help/sdk-implement/validation/validation-overview.md)

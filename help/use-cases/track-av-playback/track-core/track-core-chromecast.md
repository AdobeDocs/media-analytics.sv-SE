---
title: Lär dig hur du spårar uppspelning i Chromecast
description: Lär dig implementera huvudspårning med Media SDK på Chromecast.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
exl-id: 9812d06d-9efd-460c-a626-6a15f61a4c35
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c308dba2d7cf07b89bf124bd6e5f972c253c9f18
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# Spåra kärnuppspelning på Chromecast{#track-core-playback-on-chromecast}

I den här dokumentationen beskrivs spårning i version 2.x av SDK.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er](/help/getting-started/download-sdks.md)

1. **Inledande spårningsinställning**

   Identifiera när användaren aktiverar uppspelningsavsikten (användaren klickar på play och/eller autoplay är aktiverat) och skapar en `MediaObject` -instans.

   **`MediaObject`API-referens:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>);
   ```

   **`StreamType`konstanter:**

   [ADBMomobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`konstanter:**

   [ADBMomobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Bifoga metadata för video**

   Du kan också bifoga standard- och/eller anpassade videometadataobjekt till videospårningssessionen via kontextdatavariabler.

   * **Standardmetadata för video**

     [Implementera standardmetadata i Chromecast](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

     >[!NOTE]
     >
     >Det är valfritt att bifoga standardmetadataobjektet för video till mediaobjektet.

   * **Anpassade metadata**

     Skapa ett variabelobjekt för de anpassade variablerna och fyll i med data för videon. Exempel:

     ```js
     /* Set custom context data */
     var customVideoMetadata = {
         isUserLoggedIn: "false",
         tvStation: "Sample TV station",
         programmer: "Sample programmer"
     };
     ```

1. **Spåra avsikten att starta uppspelning**

   Om du vill börja spåra en mediesession ringer du [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) på `media` -objekt.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` spårar användarens avsikt att spela upp, inte början av uppspelningen. Detta API används för att läsa in videodata/metadata och för att beräkna QoS-måttet för tiden till start (tidsintervallet mellan `trackSessionStart` och `trackPlay`).

   >[!NOTE]
   >
   >Det andra värdet är det anpassade namnet på videometadataobjektet som du skapade i steg 2. Om du inte använder anpassade videometadata skickar du ett tomt objekt för `data` argument i `trackSessionStart`, vilket visas i kommenteringsraden i iOS-exemplet ovan.

1. **Spåra faktiskt uppspelningsstart**

   Identifiera händelsen från videospelaren i början av videouppspelningen, där videons första bildruta återges på skärmen, och anropa [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Uppdatera spelhuvudets värde**

   Uppdatera `mediaUpdatePlayhead`&#39; positionsvärde flera gånger när spelhuvudet ändras. <br /> För video-on-demand (VOD) anges värdet i sekunder från mediaobjektets början. <br /> Om spelaren inte anger information om innehållets varaktighet för direktuppspelning kan värdet anges som antalet sekunder sedan midnatt UTC den dagen.

   ```
   ADBMobile().media.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Tänk på följande när du anropar `media.updatePlayhead` API:
   >* När du använder förloppsmarkörer krävs innehållets längd och spelhuvudet måste uppdateras som antal sekunder från början av medieobjektet, med början från 0.
   >* När du använder medie-SDK:er måste du anropa `media.updatePlayhead` API minst en gång per sekund.

1. **Spåra uppspelningen**

   Identifiera händelsen från videospelaren för att slutföra videouppspelningen, där användaren har tittat på innehållet tills slutet, och anropa [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Spåra slutet av sessionen**

   Identifiera händelsen från videospelaren för borttagning/stängning av videouppspelningen, där användaren stänger videon och/eller videon är slutförd och har tagits bort, och anropa [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` markerar slutet av en videospårningssession. Om sessionen har bevakats till slutet, där användaren har tittat på innehållet till slutet, måste du se till att `trackComplete` anropas före `trackSessionEnd`. Övriga `track*` API-anrop ignoreras efter `trackSessionEnd`, förutom `trackSessionStart` för en ny videospårningssession.

1. **Spåra alla möjliga pausscenarier**

   Identifiera händelsen från videospelaren för paus och anrop av videon [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Pausa scenarier**

   Identifiera alla scenarier där videouppspelaren pausar och se till att `trackPause` anropas korrekt. Följande scenarier kräver alla ditt appsamtal `trackPause()`:

   * Användaren träffar uttryckligen paus i appen.
   * Spelaren försätts i pausläget.
   * (*Mobilappar*) - Användaren placerar programmet i bakgrunden, men du vill att sessionen ska vara öppen.
   * (*Mobilappar*) - Alla typer av systemavbrott inträffar som gör att ett program backjordas. Användaren får t.ex. ett samtal eller ett popup-fönster från ett annat program inträffar, men du vill att sessionen ska vara aktiv så att användaren kan återuppta videon från avbrottet.

1. Identifiera händelsen från spelaren för videouppspelning och/eller videouppspelning från paus och samtal [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Detta kan vara samma händelsekälla som användes i steg 4. Se till att varje `trackPause()` API-anrop har parats med följande `trackPlay()` API-anrop när videouppspelningen återupptas.

* Spårningsscenarier: [VOD-uppspelning utan annonser](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Exempelspelare ingår i Chromecast SDK för ett fullständigt spårningsexempel.

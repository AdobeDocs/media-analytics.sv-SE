---
title: Spåra annonser på Chromecast
description: Implementera annonsspårning i Chromecast-program med Media SDK.
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra annonser på Chromecast{#track-ads-on-chromecast}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning vid implementering med SDK:er för 2.x. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Konstanter för annonsspårning

| Konstantnamn | Beskrivning |
|---|---|
| `AdBreakStart` | Konstant för spårning av AdBreak-starthändelse |
| `AdBreakComplete` | Konstant för spårning av AdBreak Complete-händelse |
| `AdStart` | Konstant för spårning av Ad Start-händelse |
| `AdComplete` | Konstant för spårning av Ad Complete-händelse |
| `AdSkip` | Konstant för spårning av Ad Skip-händelse |

## Implementeringssteg

1. Identifiera när annonsbrytningens gränser börjar, inklusive pre-roll, och skapa en `AdBreakObject` genom att använda annonsbrytningsinformationen.

   Skapa brytningsobjekt: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName); 
   ```

1. Anropa `trackEvent()` med `AdBreakStart` i `MediaHeartbeat` instansen för att börja spåra annonsbrytningen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. Identifiera när annonsresursen startar och skapa en `AdObject` instans med annonsinformationen.

   Skapa annonsobjekt: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH); 
   ```

1. Du kan också bifoga standard- och/eller annonsmetadata till mediespårningssessionen via kontextdatavariabler.

   * **Standardannonsmetadata -** För standardannonsmetadata skapar du en ordlista med nyckelvärdepar för standardannonsmetadata med hjälp av tangenterna för din plattform:
   * **Anpassade annonseringsmetadata -** För anpassade metadata skapar du ett variabelobjekt för anpassade datavariabler och fyller i med data för den aktuella annonsobjektet:

1. Anropa `trackEvent()` med `AdStart` händelsen för att börja spåra annonsuppspelningen.

   Ta med en referens till din anpassade metadatavariabel (eller ett tomt objekt) som den tredje parametern i händelseanropet: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. När annonsuppspelningen når slutet av annonsen anropar du `trackEvent()` med `AdComplete` händelsen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete); 
   ```

1. Om det finns fler annonser i samma `AdBreak`version upprepar du steg 3 till 6 igen.
1. När annonsbrytningen är klar använder du `AdBreakComplete` händelsen för att spåra: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

Mer information finns i [VOD-uppspelningen för spårningsscenariot med förrollsannonser](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) .
---
title: Lär dig spåra annonser på Chromecast
description: Implementera annonsspårning i Chromecast-program med Media SDK.
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
exl-id: 57465c42-b349-439d-b8d7-083b299a8c83
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Spåra annonser på Chromecast{#track-ads-on-chromecast}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning vid implementering med SDK:er för 2.x. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Konstanter för annonsspårning

| Konstantnamn | Beskrivning   |
|---|---|
| `AdBreakStart` | Konstant för spårning av AdBreak-starthändelse |
| `AdBreakComplete` | Konstant för spårning av AdBreak Complete-händelse |
| `AdStart` | Konstant för spårning av Ad Start-händelse |
| `AdComplete` | Konstant för spårning av Ad Complete-händelse |
| `AdSkip` | Konstant för spårning av Ad Skip-händelse |

## Implementeringssteg

1. Identifiera när annonsbrytningens gränser börjar, inklusive pre-roll, och skapa en `AdBreakObject` med hjälp av annonsbrytningsinformationen.

   Skapa brytningsobjekt: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName); 
   ```

1. Anropa `trackEvent()` med `AdBreakStart` i `MediaHeartbeat`-instansen för att börja spåra annonsbrytningen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. Identifiera när annonsresursen startar och skapa en `AdObject`-instans med annonsinformationen.

   Skapa annonsobjekt: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH); 
   ```

1. Du kan också bifoga standard- och/eller annonsmetadata till mediespårningssessionen via kontextdatavariabler.

   * **Standardannonsmetadata -** För standardannonsmetadata skapar du en ordlista med nyckelvärdepar för standardannonsmetadata med hjälp av tangenterna för din plattform:
   * **Anpassade annonseringsmetadata -** För anpassade metadata skapar du ett variabelobjekt för anpassade datavariabler och fyller i med data för den aktuella annonsobjektet:

1. Anropa `trackEvent()` med händelsen `AdStart` för att börja spåra annonsuppspelningen.

   Ta med en referens till din anpassade metadatavariabel (eller ett tomt objekt) som den tredje parametern i händelseanropet: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. När annonsobjektsuppspelningen når slutet av annonsen anropar du `trackEvent()` med händelsen `AdComplete`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete); 
   ```

1. Om det finns ytterligare annonser inom samma `AdBreak` upprepar du steg 3 till 6 igen.
1. När annonsbrytningen är klar använder du händelsen `AdBreakComplete` för att spåra: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med förrollsannonser](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md).

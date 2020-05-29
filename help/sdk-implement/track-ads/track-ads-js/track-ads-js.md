---
title: Spåra annonser med JavaScript 2.x
description: Implementera annonsspårning i webbläsarprogram (JS) med Media SDK.
uuid: 4d81d29c-c55d-4d48-b505-3260922712ff
translation-type: tm+mt
source-git-commit: 815965d1cd41e73e50666a89f4a7c450af5022da
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 4%

---


# Spåra annonser med JavaScript 2.x{#track-ads-on-javascript}

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

1. Identifiera när annonsbrytningens gränser börjar, inklusive pre-roll, och skapa en `AdBreakObject` genom att använda annonsbrytningsinformationen.

   `AdBreakObject` referens:

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Annonsbrytningsnamn som för-, för- och efterrullning. | Ja |
   | `position` | Annonsbrytningens nummerposition med början på 1. | Ja |
   | `startTime` | Spelhuvudets värde i början av annonsbrytningen. | Ja |

   Skapa brytningsobjekt:

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Anropa `trackEvent()` med `AdBreakStart` i `MediaHeartbeat` instansen för att börja spåra annonsbrytningen:

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. Identifiera när annonsen startar och skapa en `AdObject` instans med annonsinformationen.

   `AdObject` referens:

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Annonsens namn. | Ja |
   | `adId` | Unik identifierare för annonsen. | Ja |
   | `position` | Annonsens nummerposition inom annonsbrytningen, med början på 1. | Ja |
   | `length` | Annonslängd | Ja |

   Skapa annonsobjekt:

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Du kan också bifoga standard- och/eller annonsmetadata till mediespårningssessionen via kontextdatavariabler.

   * [Implementera standardmetadata för annonser i JavaScript](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
   * **Anpassade annonseringsmetadata -** Skapa ett variabelobjekt för anpassade datavariabler och fyll i med data för den aktuella annonsen:

      ```js
      /* Set custom context data */
      var adCustomMetadata = {
          affiliate: "Sample affiliate",
          campaign: "Sample ad campaign",
          creative: "Sample creative"
      };
      ```

1. Anropa `trackEvent()` med `AdStart` händelsen i `MediaHeartbeat` instansen för att börja spåra annonsuppspelningen.

   Ta med en referens till din anpassade metadatavariabel (eller ett tomt objekt) som den tredje parametern i händelseanropet:

   ```js
   _onAdStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata);
   };
   ```

1. När annonsuppspelningen når slutet av annonsen ska du ringa `trackEvent()` med `AdComplete` händelsen:

   ```js
   _onAdComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
   };
   ```

1. Om annonsuppspelningen inte slutfördes eftersom användaren valde att hoppa över annonsen, ska du spåra `AdSkip` händelsen:

   ```js
   _onAdSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
   };
   ```

1. Om det finns fler annonser i samma `AdBreak`version upprepar du steg 3 till 7 igen.
1. När annonsbrytningen är klar använder du `AdBreakComplete` händelsen för att spåra:

   ```js
   _onAdBreakComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
   };
   ```

Mer information finns i [VOD-uppspelningen för spårningsscenariot med förrollsannonser](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) .

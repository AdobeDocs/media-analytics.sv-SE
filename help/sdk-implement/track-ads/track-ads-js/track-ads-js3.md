---
title: Lär dig spåra annonser med JavaScript 3.x
description: Implementera annonsspårning i webbläsarprogram (JS) med Media SDK.
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---

# Spåra annonser med JavaScript 3.x{#track-ads-on-javascript}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning vid implementering med 3.x SDK:er. Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandböckerna här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

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

   `AdBreakObject` referens:

   | Variabelnamn | Typ | Beskrivning |
   | --- | --- | --- |
   | `name` | string | En sträng som inte är tom och som betecknar adbreak name (pre-roll, mid-roll och post-roll). |
   | `position` | tal | Annonsbrytningens nummerposition med början på 1. |
   | `startTime` | tal | Spelhuvudets värde i början av annonsbrytningen. |

   Skapa brytningsobjekt:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. Anropa `trackEvent()` med `AdBreakStart` i `MediaHeartbeat`-instansen för att börja spåra annonsbrytningen:

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. Identifiera när annonsen startar och skapa en `AdObject`-instans med annonsinformationen.

   `AdObject` referens:

   | Variabelnamn | Typ | Beskrivning |
   | --- | --- | --- |
   | `name` | string | En sträng som inte är tom betecknar annonsnamnet. |
   | `adId` | string | En sträng som inte är tom betecknar annonsidentifierare. |
   | `position` | tal | Annonsens sifferposition inom reklamen, med början på 1. |
   | `length` | tal | Positivt nummer som anger annonsens längd. |

   Skapa annonsobjekt:

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. Du kan också bifoga standard- och/eller annonsmetadata till mediespårningssessionen via kontextdatavariabler.

   * [Implementera standardmetadata för annonser i JavaScript](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **Anpassade annonseringsmetadata -** Skapa ett variabelobjekt för anpassade datavariabler och fyll i med data för den aktuella annonsen:

      ```js
      /* Set context data */
      // Standard metadata keys provided by adobe.
      adMetadata[ADB.Media.AdMetadataKeys]  ="Sample Advertiser";
      adMetadata[ADB.Media.AdMetadataKeys] = "Sample Campaign";
      
      // Custom metadata keys
      adMetadata["affiliate"] = "Sample affiliate";
      adMetadata["campaign"] = "Sample ad campaign";
      adMetadata["creative"] = "Sample creative";
      ```

1. Anropa `trackEvent()` med händelsen `AdStart` i instansen `MediaHeartbeat` för att börja spåra annonsuppspelningen.

   Ta med en referens till din anpassade metadatavariabel (eller ett tomt objekt) som den tredje parametern i händelseanropet:

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. När annonsuppspelningen når slutet av annonsen anropar du `trackEvent()` med händelsen `AdComplete`:

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. Om annonsuppspelningen inte slutfördes eftersom användaren valde att hoppa över annonsen, ska du spåra händelsen `AdSkip`:

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. Om det finns ytterligare annonser inom samma `AdBreak` upprepar du steg 3 till 7 igen.
1. När annonsbrytningen är klar använder du händelsen `AdBreakComplete` för att spåra:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med förrollsannonser](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md).

---
title: Lär dig spåra annonser med JavaScript 3.x
description: Implementera annonsspårning i webbläsarprogram (JS) med Media SDK.
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# Spåra annonser med JavaScript 3.x{#track-ads-on-javascript}

Följande instruktioner ger vägledning vid implementering med 3.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Konstanter för annonsspårning

| Konstantnamn | Beskrivning   |
|---|---|
| `AdBreakStart` | Konstant för spårning av AdBreak-starthändelse |
| `AdBreakComplete` | Konstant för spårning av AdBreak Complete-händelse |
| `AdStart` | Konstant för spårning av Ad Start-händelse |
| `AdComplete` | Konstant för spårning av Ad Complete-händelse |
| `AdSkip` | Konstant för spårning av Ad Skip-händelse |

## Implementeringssteg

1. Identifiera när annonsbrytningsgränsen börjar, inklusive pre-roll, och skapa en `AdBreakObject` med hjälp av annonsbrytningsinformationen.

   `AdBreakObject`-referens:

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

   `AdObject`-referens:

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

1. (Valfritt) Koppla standard- och/eller annonsmetadata till mediespårningssessionen via kontextdatavariabler.

   * [Implementera standardannonsmetadata på JavaScript](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **Anpassade annonseringsmetadata -** För anpassade metadata skapar du ett variabelobjekt för anpassade datavariabler och fyller i med data för den aktuella annonsen:

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

1. Om annonsuppspelningen inte slutfördes eftersom användaren valde att hoppa över annonsen, ska du spåra `AdSkip`-händelsen:

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. Om det finns ytterligare annonser i samma `AdBreak` upprepar du steg 3 till 7 igen.
1. När annonsbrytningen är klar använder du händelsen `AdBreakComplete` för att spåra:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med förhandsgranskningsannonser](/help/use-cases/tracking-scenarios/vod-preroll-ads.md).

## Detaljerad annonshantering

Standardintervallet för annonsväxling är `10 seconds`.

Du kan konfigurera detaljerad annonsspårning för att aktivera annonsspårning för `1 second`.

>[!IMPORTANT]
>
>Den här informationen måste anges när en spårningssession startas.



**Syntax**

```javascript
ADB.Media.MediaObjectKey = {
   GranularAdTracking: "media.granularadtracking"
   }
```

**Exempel**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

// Enable granular ad tracking
mediaObject[ADB.Media.MediaObjectKey.GranularAdTracking] = true;

tracker.trackSessionStart(mediaObject);
```

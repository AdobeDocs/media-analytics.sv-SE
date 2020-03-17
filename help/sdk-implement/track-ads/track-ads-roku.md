---
title: Spåra annonser på Roku
description: Implementera annonsspårning i Roku-program med Media SDK.
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra annonser på Roku{#track-ads-on-roku}

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

   `AdBreakObject` referens:

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Annonsbrytningsnamn som för-, för- och efterrullning. | Ja |
   | `position` | Annonsbrytningens nummerposition med början på 1. | Ja |
   | `startTime` | Spelhuvudets värde i början av annonsbrytningen. | Ja |

   ```
   ‘ Create an adbreak info object 
   adBreakInfo = adb_media_init_adbreakinfo() 
   adBreakInfo.name = <ADBREAK_NAME> 
   adBreakInfo.startTime = <START_TIME> 
   adBreakInfo.position = <POSITION>
   ```

1. Anropa `trackEvent()` med `AdBreakStart` i `MediaHeartbeat` instansen för att börja spåra annonsbrytningen:

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. Identifiera när annonsresursen startar och skapa en `AdObject` instans med annonsinformationen.

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration) 
   ```

1. Du kan också bifoga standard- och/eller annonsmetadata till mediespårningssessionen via kontextdatavariabler.

   * [Implementera standardannonsmetadata på Roku](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **Anpassade annonseringsmetadata -** För anpassade metadata skapar du ett variabelobjekt för anpassade datavariabler och fyller i med data för den aktuella annonsobjektet:

      ```
      contextData = {} 
      contextData["adinfo1"] = "adinfo2" 
      contextData["adinfo2"] = "adinfo2"
      ```

1. Anropa `trackEvent()` med `AdStart` händelsen i `MediaHeartbeat` instansen för att börja spåra annonsuppspelningen:

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. När annonsuppspelningen når slutet av annonsen ska du anropa `trackEvent()` med `AdComplete` händelsen.

   ```
   standardAdMetadata = {} 
   contextData = {} 
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. Om annonsuppspelningen inte slutfördes eftersom användaren valde att hoppa över annonsen, ska du spåra `AdSkip` händelsen:

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. Om det finns fler annonser i samma `AdBreak`version upprepar du steg 3 till 7 igen.
1. När annonsbrytningen är klar använder du `AdBreakComplete` händelsen för att spåra:

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

Mer information finns i [VOD-uppspelningen för spårningsscenariot med förrollsannonser](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) .

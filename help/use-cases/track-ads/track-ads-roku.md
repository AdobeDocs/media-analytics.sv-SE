---
title: Lär dig spåra annonser på Roku
description: Implementera annonsspårning i Roku-program med Media SDK.
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
exl-id: aaed828d-1aba-486e-83e3-2ffd092305e2
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Spåra annonser på Roku{#track-ads-on-roku}

Följande anvisningar ger vägledning vid implementering med SDK:er för 2.x.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

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

1. Anropa `trackEvent()` med `AdBreakStart` i `MediaHeartbeat`-instansen för att börja spåra annonsbrytningen:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. Identifiera när annonsresursen startar och skapa en `AdObject`-instans med annonsinformationen.

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration)
   ```

1. Du kan också bifoga standard- och/eller annonsmetadata till mediespårningssessionen via kontextdatavariabler.

   * [Implementera standardannonsmetadata på Roku](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **Anpassade annonseringsmetadata -** För anpassade metadata skapar du ett variabelobjekt för anpassade datavariabler och fyller i med data för den aktuella annonsobjektet:

     ```
     contextData = {}
     contextData["adinfo1"] = "adinfo2"
     contextData["adinfo2"] = "adinfo2"
     ```

1. Anropa `trackEvent()` med händelsen `AdStart` i instansen `MediaHeartbeat` för att börja spåra annonsuppspelningen:

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. När annonsobjektsuppspelningen når slutet av annonsen anropar du `trackEvent()` med händelsen `AdComplete`.

   ```
   standardAdMetadata = {}
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. Om annonsuppspelningen inte slutfördes eftersom användaren valde att hoppa över annonsen, ska du spåra `AdSkip`-händelsen:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. Om det finns ytterligare annonser i samma `AdBreak` upprepar du steg 3 till 7 igen.
1. När annonsbrytningen är klar använder du händelsen `AdBreakComplete` för att spåra:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med förhandsgranskningsannonser](/help/use-cases/tracking-scenarios/vod-preroll-ads.md).

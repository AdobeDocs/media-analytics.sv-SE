---
title: Lär dig spåra annonser på Android
description: Implementera annonsspårning i Android-program med Media SDK.
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4
exl-id: 1f96dde9-c924-4fce-8b14-7dec7137f265
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---

# Spåra annonser på Android{#track-ads-on-android}

Följande anvisningar ger vägledning vid implementering med SDK:er för 2.x.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Konstanter för annonsspårning

| Konstantnamn | Beskrivning |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | Konstant för spårning av AdBreak-starthändelse |
| `MediaHeartbeat.Event.AdBreakComplete` | Konstant för spårning av AdBreak Complete-händelse |
| `MediaHeartbeat.Event.AdStart` | Konstant för spårning av Ad Start-händelse |
| `MediaHeartbeat.Event.AdComplete` | Konstant för spårning av Ad Complete-händelse |
| `MediaHeartbeat.Event.AdSkip` | Konstant för spårning av Ad Skip-händelse |

## Implementeringssteg

1. Identifiera när annonsbrytningsgränsen börjar, inklusive pre-roll, och skapa en `AdBreakObject` med hjälp av annonsbrytningsinformationen.

   `AdBreakObject`-referens:

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Annonsbrytningsnamn som för-, för- och efterrullning. | Ja |
   | `position` | Annonsens nummerposition i innehållet, med början på 1. | Ja |
   | `startTime` | Spelhuvudets värde i början av annonsbrytningen. | Ja |

   Skapa brytningsobjekt:

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Anropa `trackEvent()` med `AdBreakStart` i `MediaHeartbeat`-instansen för att börja spåra annonsbrytningen:

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null);
   }
   ```

1. Identifiera när annonsen startar och skapa en `AdObject`-instans med annonsinformationen.

   `AdObject`-referens:

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Annonsens namn. | Ja |
   | `adId` | Unik identifierare för annonsen. | Ja |
   | `position` | Annonsens nummerposition inom annonsbrytningen, med början på 1. | Ja |
   | `length` | Annonslängd | Ja |

   Skapa annonsobjekt:

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME>
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Du kan också bifoga standard- och/eller annonsmetadata till mediespårningssessionen via kontextdatavariabler.

   * [Implementera standardannonsmetadata på Android](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)

   help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md

   * **Anpassade annonseringsmetadata -** För anpassade metadata skapar du ett variabelobjekt för anpassade datavariabler och fyller i med data för den aktuella annonsen:

     ```java
     // Setting Ad Metadata
     HashMap<String, String> adMetadata = new HashMap<String, String>();
     adMetadata.put("affiliate", "Sample affiliate");
     adMetadata.put("campaign", "Sample ad campaign");
     ```

1. Anropa `trackEvent()` med händelsen `AdStart` i instansen `MediaHeartbeat` för att börja spåra annonsuppspelningen.

   Ta med en referens till din anpassade metadatavariabel (eller ett tomt objekt) som den tredje parametern i händelseanropet:

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata);
   }
   ```

1. När annonsuppspelningen når slutet av annonsen anropar du `trackEvent()` med händelsen `AdComplete`:

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null);
   }
   ```

1. Om annonsuppspelningen inte slutfördes eftersom användaren valde att hoppa över annonsen, ska du spåra `AdSkip`-händelsen:

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null);
   }
   ```

1. Om det finns ytterligare annonser i samma `AdBreak` upprepar du steg 3 till 7 igen.
1. När annonsbrytningen är klar använder du händelsen `AdBreakComplete` för att spåra:

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null);
   }
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med förhandsgranskningsannonser](/help/use-cases/tracking-scenarios/vod-preroll-ads.md).

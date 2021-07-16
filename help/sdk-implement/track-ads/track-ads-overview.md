---
title: Spåra annonser som förklaras
description: Översikt över implementering av annonsspårning med Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# Översikt{#overview}

Följande anvisningar ger vägledning vid implementering med SDK:er för 2.x.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandböcker här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

Annonsuppspelning inkluderar spårning av annonsbrytningar, start, slutförande av annonser och hopp för annonser. Använd mediespelarens API för att identifiera viktiga spelarhändelser och fylla i obligatoriska och valfria annonsvariabler. Se den omfattande listan med metadata här: [Lägg till parametrar.](/help/metrics-and-metadata/ad-parameters.md)

## Spelarhändelser {#player-events}


### Vid start av annonsbrytning

>[!NOTE]
>Inklusive pre-roll

* Skapa en `adBreak`-objektinstans för annonsbrytningen. Exempel, `adBreakObject`.

* Ring `trackEvent` för att få annonsbrytningen att börja med din `adBreakObject`.

### Alla annonsresurser börjar

* Skapa en annonsobjektinstans för annonsresursen. Exempel, `adObject`.
* Fyll i annonsmetadata, `adCustomMetadata`.
* Ring `trackEvent` för annonsstart.

### Alla annonser är fullständiga

* Ring `trackEvent` för att få annonsen klar.

### I annonshoppa

* Ring `trackEvent` för att få en annons.

### On ad break complete

* Ring `trackEvent` för att få annonsbrytningen klar.

## Implementera annonsspårning {#implement-ad-tracking}

### Konstanter för annonsspårning

| Konstantnamn | Beskrivning   |
|---|---|
| `AdBreakStart` | Konstant för spårning av AdBreak-starthändelse |
| `AdBreakComplete` | Konstant för spårning av AdBreak Complete-händelse |
| `AdStart` | Konstant för spårning av Ad Start-händelse |
| `AdComplete` | Konstant för spårning av Ad Complete-händelse |
| `AdSkip` | Konstant för spårning av Ad Skip-händelse |

### Implementeringssteg

1. Identifiera när annonsbrytningens gränser börjar, inklusive pre-roll, och skapa en `AdBreakObject` med hjälp av annonsbrytningsinformationen.

   `AdBreakObject` referens:

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Annonsbrytningsnamn som för-, för- och efterrullning. | Ja |
   | `position` | Annonsens nummerposition i innehållet, med början på 1. | Ja |
   | `startTime` | Spelhuvudets värde i början av annonsbrytningen. | Ja |

1. Anropa `trackEvent()` med `AdBreakStart` i `MediaHeartbeat`-instansen för att börja spåra annonsbrytningen.

1. Identifiera när annonsen startar och skapa en `AdObject`-instans med annonsinformationen.

   `AdObject` referens:

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Annonsens namn. | Ja |
   | `adId` | Unik identifierare för annonsen. | Ja |
   | `position` | Annonsens nummerposition inom annonsbrytningen, med början på 1. | Ja |
   | `length` | Annonslängd | Ja |

1. Du kan också bifoga standard- och/eller annonseringsmetadata till spårningssessionen via kontextdatavariabler.

   * **Standardannonsmetadata -** För standardannonsmetadata skapar du en ordlista med nyckelvärdepar för standardannonsmetadata med hjälp av tangenterna för din plattform.
   * **Anpassade annonseringsmetadata -** För anpassade metadata skapar du ett variabelobjekt för de anpassade datavariablerna och fyller i med data för den aktuella annonsen.

1. Anropa `trackEvent()` med händelsen `AdStart` i instansen `MediaHeartbeat` för att börja spåra annonsuppspelningen.

   Ta med en referens till din anpassade metadatavariabel (eller ett tomt objekt) som den tredje parametern i händelseanropet.

1. När annonsuppspelningen når slutet av annonsen anropar du `trackEvent()` med händelsen `AdComplete`.

1. Om annonsuppspelningen inte slutfördes eftersom användaren valde att hoppa över annonsen, ska du spåra händelsen `AdSkip`.
1. Om det finns ytterligare annonser inom samma `AdBreak` upprepar du steg 3 till 7 igen.
1. När annonsbrytningen är klar använder du händelsen `AdBreakComplete` för att spåra den.

>[!IMPORTANT]
>
>Se till att du INTE ökar spelhuvudet för innehållsspelaren (`l:event:playhead`) under annonsuppspelning (`s:asset:type=ad`). Om du gör det påverkas Content Time Spent-måtten negativt.

I följande exempelkod används JavaScript 2.x SDK för en HTML5-mediespelare.

```js
/* Call on ad break start */

if (e.type == "ad break start") {
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500);
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
};

/* Call on ad start */
if (e.type == "ad start") {
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30);
    /* Set custom context data */
    var adCustomMetadata = {
        affiliate:"Sample affiliate",
        campaign:"Sample ad campaign",
        creative:"Sample creative"
    }
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);
};

/* Call on ad complete */
if (e.type == "ad complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
};

/* Call on ad skip */
if (e.type == "ad skip") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
};

/* Call on ad break complete */
if (e.type == "ad break complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
};
```

---
title: Översikt
description: Så här implementerar du kapitel- och segmentspårning med Media SDK.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Översikt{#overview}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning vid implementering med 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

Kapitel- och segmentspårning är tillgängligt för anpassade mediekapital eller segment. En del vanliga användningsområden för kapitelspårning är att definiera anpassade segment baserat på mediainnehåll (t.ex. baseboll) eller att definiera innehållssegment mellan annonsbrytningar. Kapitelspårning krävs **inte** för implementering av huvudmediespårning.

Kapitelspårning innehåller kapitelstarter, kapitelslutföranden och kapitelhopp. Du kan använda mediaspelarens API med anpassad segmenteringslogik för att identifiera kapitelhändelser och för att fylla i obligatoriska och valfria kapitelvariabler.

## Spelarhändelser

### Vid kapitelstart

* Skapa kapitelobjektinstansen för kapitlet, `chapterObject`
* Fyll i kapitelmetadata, `chapterCustomMetadata`
* Utlysning `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Vid kapitelavslutning

* Utlysning `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Hoppa över kapitel

* Utlysning `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implementera kapitelspårning {#implement-chapter-tracking}

1. Identifiera när kapitelstarthändelsen inträffar och skapa `ChapterObject` instansen med kapitelinformationen.

   Här är referensen för `ChapterObject` kapitelspårning:

   >[!NOTE]
   >
   >Dessa variabler är bara obligatoriska om du tänker spåra kapitel.

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Kapitelnamn | Ja |
   | `position` | Kapitelposition | Ja |
   | `length` | Kapitellängd | Ja |
   | `startTime` | Starttid för kapitel | Ja |

1. Om du inkluderar anpassade metadata för kapitlet skapar du kontextdatavariabler för metadata.
1. Om du vill börja spåra kapiteluppspelningen anropar du `ChapterStart` händelsen i `MediaHeartbeat` instansen.
1. När uppspelningen når kapitelslutsgränsen, som definieras av din egen kod, anropar du `ChapterComplete` händelsen i `MediaHeartbeat` instansen.
1. Om kapiteluppspelningen inte slutfördes eftersom användaren valde att hoppa över kapitlet (till exempel om användaren söker utanför kapitelgränsen) anropar du händelsen `ChapterSkip` i MediaHeartbeat-instansen.
1. Om det finns ytterligare kapitel upprepar du steg 1 till 5.

I följande exempelkod används JavaScript 2.x SDK för en HTML5-mediespelare. Du bör använda den här koden med den viktigaste mediespelningskoden.

```js
/* Call on chapter start */ 
if (e.type == "chapter start") { 
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500); 
    /* Set custom context data*/ 
    var chapterCustomMetadata = { 
        segmentType:"Baseball Innings", 
        segmentName:"Inning 5", 
        segmentInfo:"Game Six" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata); 
}; 
 
/* Call on chapter complete */ 
if (e.type == "chapter complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
}; 
 
/* Call on chapter skip */ 
if (e.type == "chapter skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
}; 
```


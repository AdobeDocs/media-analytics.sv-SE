---
title: Spåra kapitel och segment med JavaScript 2.x
description: I det här avsnittet beskrivs hur du implementerar kapitel- och segmentspårning med Media SDK i webbläsarappar (JS).
uuid: ef99edf7-7a77-46c4-8429-bc9a856b98d6
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 2%

---


# Spåra kapitel och segment med JavaScript 2.x{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning vid implementering med 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

1. Identifiera när kapitelstarthändelsen inträffar och skapa `ChapterObject` instansen med kapitelinformationen.

   `ChapterObject` kapitelspårningsreferens:

   >[!NOTE]
   >
   >Dessa variabler är bara obligatoriska om du tänker spåra kapitel.

   | Variabelnamn | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `name` | Kapitelnamn | Ja |
   | `position` | Kapitelposition | Ja |
   | `length` | Kapitellängd | Ja |
   | `startTime` | Starttid för kapitel | Ja |

   Kapitelobjekt:

   ```js
   var chapterInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Om du inkluderar anpassade metadata för kapitlet skapar du kontextdatavariabler för metadata:

   ```js
   var chapterCustomMetadata = {
       segmentType: "Sample segment type",  
       segmentName: "Sample segment name",  
       segmentInfo: "Sample segment info"
   };
   ```

1. Om du vill börja spåra kapiteluppspelningen anropar du `ChapterStart` händelsen i `MediaHeartbeat` instansen:

   ```js
   _onChapterStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata);
   };
   ```

1. När uppspelningen når kapitelslutsgränsen, som definieras av din egen kod, anropar du `ChapterComplete` händelsen i `MediaHeartbeat` instansen:

   ```js
   _onChapterComplete = function() {
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
   };
   ```

1. Om kapiteluppspelningen inte slutfördes eftersom användaren valde att hoppa över kapitlet (till exempel om användaren söker utanför kapitelgränsen), anropar du händelsen `ChapterSkip` i MediaHeartbeat-instansen:

   ```js
   _onChapterSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
   };
   ```

1. Om det finns ytterligare kapitel upprepar du steg 1 till 5.

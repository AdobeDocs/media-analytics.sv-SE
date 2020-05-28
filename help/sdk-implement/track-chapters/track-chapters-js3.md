---
title: Spåra kapitel och segment med JavaScript 3.x
description: I det här avsnittet beskrivs hur du implementerar kapitel- och segmentspårning med Media SDK i webbläsarappar (JS).
translation-type: tm+mt
source-git-commit: b14b56aea4a1821a2a160b9cd301cd181f1ba8dd
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Spåra kapitel och segment med JavaScript 3.x{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning vid implementering med 3.x SDK:er. Om du implementerar en tidigare version av SDK kan du ladda ned utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

1. Identifiera när kapitelstarthändelsen inträffar och skapa `ChapterObject` instansen med kapitelinformationen.

   `ChapterObject` kapitelspårningsreferens:

   >[!NOTE]
   >
   >Dessa variabler är bara obligatoriska om du tänker spåra kapitel.

   | Variabelnamn | Typ | Beskrivning |
   | --- | --- | --- |
   | `name` | string | Icke tom sträng som betecknar kapitelnamn. |
   | `position` | tal | Placeringen av kapitlet i innehållet, med början på 1. |
   | `length` | tal | Positivt nummer som anger kapitlets längd. |
   | `startTime` | tal | Spelhuvudsvärde i början av kapitel. |

   Kapitelobjekt:

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. Om du inkluderar anpassade metadata för kapitlet skapar du kontextdatavariabler för metadata:

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. Om du vill börja spåra kapiteluppspelningen anropar du `ChapterStart` händelsen i `MediaHeartbeat` instansen:

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. När uppspelningen når kapitelslutsgränsen, som definieras av din egen kod, anropar du `ChapterComplete` händelsen i `MediaHeartbeat` instansen:

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. Om kapiteluppspelningen inte slutfördes eftersom användaren valde att hoppa över kapitlet (till exempel om användaren söker utanför kapitelgränsen), anropar du händelsen `ChapterSkip` i MediaHeartbeat-instansen:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. Om det finns ytterligare kapitel upprepar du steg 1 till 5.

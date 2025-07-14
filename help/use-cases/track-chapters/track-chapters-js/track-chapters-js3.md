---
title: Lär dig spåra kapitel och segment med JavaScript 3.x
description: Lär dig hur du implementerar kapitel- och segmentspårning med Media SDK i webbläsarappar (JS).
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Spåra kapitel och segment med JavaScript 3.x{#track-chapters-and-segments-on-javascript}

Följande instruktioner ger vägledning vid implementering med 3.x SDK:er.

>[!IMPORTANT]
>
> Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

1. Identifiera när kapitelstarthändelsen inträffar och skapa `ChapterObject`-instansen med hjälp av kapitelinformationen.

   Referens för `ChapterObject`-kapitelspårning:

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

1. Om du vill börja spåra kapiteluppspelningen anropar du händelsen `ChapterStart` i instansen `MediaHeartbeat`:

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. När uppspelningen når kapitelslutsgränsen, enligt definitionen i din egen kod, anropar du händelsen `ChapterComplete` i instansen `MediaHeartbeat`:

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

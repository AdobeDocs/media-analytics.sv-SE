---
title: Lär dig att spåra kapitel och segment med JavaScript 2.x
description: Lär dig hur du implementerar kapitel- och segmentspårning med Media SDK i webbläsarappar (JS).
uuid: ef99edf7-7a77-46c4-8429-bc9a856b98d6
exl-id: 9964ec0c-cce9-4ccc-bd26-a2b3fcdc3e28
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---

# Spåra kapitel och segment med JavaScript 2.x{#track-chapters-and-segments-on-javascript}

Följande instruktioner ger vägledning vid implementering med 2.x SDK:er.

>[!IMPORTANT]
>
> Om du implementerar en 1.x-version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

1. Identifiera när kapitelstarthändelsen inträffar och skapa `ChapterObject` med hjälp av kapitelinformationen.

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

1. Börja spåra kapiteluppspelningen genom att anropa `ChapterStart` i `MediaHeartbeat` instans:

   ```js
   _onChapterStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata);
   };
   ```

1. Anropa `ChapterComplete` i `MediaHeartbeat` instans:

   ```js
   _onChapterComplete = function() {
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
   };
   ```

1. Om kapiteluppspelningen inte slutfördes på grund av att användaren valde att hoppa över kapitlet (till exempel om användaren söker utanför kapitelgränsen), anropar du `ChapterSkip` i MediaHeartbeat-instansen:

   ```js
   _onChapterSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
   };
   ```

1. Om det finns ytterligare kapitel upprepar du steg 1 till 5.

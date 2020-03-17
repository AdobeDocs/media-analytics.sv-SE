---
title: Spåra kapitel och segment på iOS
description: I det här avsnittet beskrivs hur du implementerar kapitel- och segmentspårning med Media SDK i iOS.
uuid: ffc5ce9f-04ba-4059-92d4-4cb4180ac9ed
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra kapitel och segment på iOS{#track-chapters-and-segments-on-ios}

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

   ```
   id chapterObject =  
     [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME] 
                        position:[POSITION] 
                        length:[LENGTH] 
                        startTime:[START_TIME]];
   ```

1. Om du inkluderar anpassade metadata för kapitlet skapar du kontextdatavariabler för metadata:

   ```
   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init]; 
   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"]; 
   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"]; 
   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
   ```

1. Om du vill börja spåra kapiteluppspelningen anropar du `ChapterStart` händelsen i `MediaHeartbeat` instansen:

   ```
   - (void)onChapterStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary]; 
   }
   ```

1. När uppspelningen når kapitelslutsgränsen, som definieras av din egen kod, anropar du `ChapterComplete` händelsen i `MediaHeartbeat` instansen:

   ```
   - (void)onChapterComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Om kapiteluppspelningen inte slutfördes eftersom användaren valde att hoppa över kapitlet (till exempel om användaren söker utanför kapitelgränsen), anropar du händelsen `ChapterSkip` i MediaHeartbeat-instansen:

   ```
   - (void)onChapterSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Om det finns ytterligare kapitel upprepar du steg 1 till 5.


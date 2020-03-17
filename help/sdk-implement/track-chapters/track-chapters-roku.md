---
title: Spåra kapitel och segment på Roku
description: I det här avsnittet beskrivs hur du implementerar kapitel- och segmentspårning med Media SDK på Roku.
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra kapitel och segment på Roku{#track-chapters-and-segments-on-roku}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning vid implementering med 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Implementera standardannonsmetadata

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
   chapterInfo =  
     adb_media_init_chapterinfo(<CHAPTER_NAME>,  
                                <POSITION>,  
                                <LENGTH>,  
                                <START_TIME>);)
   ```

1. Om du inkluderar anpassade metadata för kapitlet skapar du kontextdatavariabler för metadata:

   ```
   chapterContextData = {} 
   chapterContextData["seg_type"] = "seg_type" 
   chapterContextData["seg_name"] = "seg_name" 
   chapterContextData["seg_info"] = "seg_info"
   ```

1. Om du vill börja spåra kapiteluppspelningen anropar du `ChapterStart` händelsen i `MediaHeartbeat` instansen:

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. När uppspelningen når kapitelslutsgränsen, som definieras av din egen kod, anropar du `ChapterComplete` händelsen i `MediaHeartbeat` instansen.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Om kapiteluppspelningen inte slutfördes eftersom användaren valde att hoppa över kapitlet (till exempel om användaren söker utanför kapitelgränsen) anropar du händelsen `ChapterSkip` i MediaHeartbeat-instansen.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. Om det finns ytterligare kapitel upprepar du steg 1 till 5.


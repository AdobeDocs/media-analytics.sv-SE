---
title: Lär dig spåra kapitel och segment på Roku
description: Lär dig hur du implementerar kapitel- och segmentspårning med Media SDK på Roku.
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
exl-id: b5eb8be7-4b85-4ba7-9216-dd691be7ba46
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---

# Spåra kapitel och segment på Roku{#track-chapters-and-segments-on-roku}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning vid implementering med 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Implementera standardannonsmetadata

1. Identifiera när kapitelstarthändelsen inträffar och skapa `ChapterObject`-instansen med hjälp av kapitelinformationen.

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

1. Börja spåra kapiteluppspelningen genom att anropa händelsen `ChapterStart` i `MediaHeartbeat`-instansen:

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. När uppspelningen når kapitelslutsgränsen, enligt definitionen i den anpassade koden, anropar du händelsen `ChapterComplete` i `MediaHeartbeat`-instansen.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Om kapiteluppspelningen inte slutfördes eftersom användaren valde att hoppa över kapitlet (till exempel om användaren söker utanför kapitelgränsen), anropar du händelsen `ChapterSkip` i MediaHeartbeat-instansen.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. Om det finns ytterligare kapitel upprepar du steg 1 till 5.

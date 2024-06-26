---
title: Lär dig spåra kapitel och segment på Roku
description: Lär dig hur du implementerar kapitel- och segmentspårning med Media SDK på Roku.
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
exl-id: b5eb8be7-4b85-4ba7-9216-dd691be7ba46
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---

# Spåra kapitel och segment på Roku{#track-chapters-and-segments-on-roku}

Följande instruktioner ger vägledning vid implementering med 2.x SDK:er.

>[!IMPORTANT]
>
> Om du implementerar en 1.x-version av SDK kan du hämta utvecklarhandboken här: [Ladda ned SDK:er.](/help/getting-started/download-sdks.md)

## Implementera standardannonsmetadata

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

1. Börja spåra kapiteluppspelningen genom att anropa `ChapterStart` -händelsen i `MediaHeartbeat` instans:

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. När uppspelningen når kapitelslutsgränsen, som definieras av din egen kod, anropar du `ChapterComplete` -händelsen i `MediaHeartbeat` -instans.

   ```
   chapterContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Om kapiteluppspelningen inte slutfördes på grund av att användaren valde att hoppa över kapitlet (till exempel om användaren söker utanför kapitelgränsen), anropar du `ChapterSkip` i MediaHeartbeat-instansen.

   ```
   chapterContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. Om det finns ytterligare kapitel upprepar du steg 1 till 5.

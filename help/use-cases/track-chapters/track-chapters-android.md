---
title: Lär dig spåra kapitel och segment i Android
description: Lär dig hur du implementerar kapitel- och segmentspårning med Media SDK i Android.
uuid: 013815d7-4d9e-48f4-a2b9-3b70cb1149d3
exl-id: ada2e2a7-1383-471c-9ce6-c82ea93fa79d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 2%

---

# Spåra kapitel och segment på Android{#track-chapters-and-segments-on-android}

Följande instruktioner ger vägledning vid implementering med 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Implementera kapitelspårning

1. Identifiera när kapitelstarthändelsen inträffar och skapa `ChapterObject`-instansen med hjälp av kapitelinformationen.

   Referens för `ChapterObject`-kapitelspårning:

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

   ```java
   MediaObject chapterDataInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Om du inkluderar anpassade metadata för kapitlet skapar du kontextdatavariabler för metadata:

   ```java
   HashMap<String, String> chapterMetadata =  
     new HashMap<String,String>();
   chapterMetadata.put("segmentType", "Sample Segment Type");
   chapterMetadata.put("segmentName", "Sample Segment Name");
   chapterMetadata.put("segmentInfo", "Sample Segment Info");
   ```

1. Om du vill börja spåra kapiteluppspelningen anropar du händelsen `ChapterStart` i instansen `MediaHeartbeat`:

   ```java
   public void onChapterStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                             chapterDataInfo,  
                             chapterMetadata);
   }
   ```

1. När uppspelningen når kapitelslutsgränsen, enligt definitionen i din egen kod, anropar du händelsen `ChapterComplete` i instansen `MediaHeartbeat`:

   ```java
   public void onChapterComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null);
   }
   ```

1. Om kapiteluppspelningen inte slutfördes eftersom användaren valde att hoppa över kapitlet (till exempel om användaren söker utanför kapitelgränsen), anropar du händelsen `ChapterSkip` i MediaHeartbeat-instansen:

   ```java
   public void onChapterSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null);
   }
   ```

1. Om det finns ytterligare kapitel upprepar du steg 1 till 5.

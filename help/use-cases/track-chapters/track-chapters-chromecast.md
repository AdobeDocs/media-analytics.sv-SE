---
title: Lär dig spåra kapitel och segment i Chromecast
description: Lär dig hur du implementerar kapitel- och segmentspårning med Media SDK på Chromecast.
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
exl-id: 26b71e4d-ced7-49cb-a838-2b1c8d4ee4de
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---

# Spåra kapitel och segment i Chromecast{#track-chapters-and-segments-on-chromecast}

Följande instruktioner ger vägledning vid implementering med 2.x SDK:er.

>[!IMPORTANT]
>
> Om du implementerar en 1.x-version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

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

   Kapitelobjekt: [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

   ```js
   chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
   ```

1. Om du inkluderar anpassade metadata för kapitlet skapar du kontextdatavariabler för metadata:

   ```js
   var chapterContextData = {
       segmentType: "Sample segment type"
   };
   ```

1. Spåra `ChapterStart`-händelsen för att börja spåra kapiteluppspelningen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData);
   ```

1. När uppspelningen når kapitelslutsgränsen, enligt definitionen i din egen kod, anropar du händelsen `ChapterComplete` i `MediaHeartbeat`-instansen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. Om kapiteluppspelningen inte slutfördes eftersom användaren valde att hoppa över kapitlet (till exempel om användaren söker utanför kapitelgränsen), ska du spåra `ChapterSkip`-händelsen: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
   ```

1. Om det finns ytterligare kapitel upprepar du steg 1 till 5.

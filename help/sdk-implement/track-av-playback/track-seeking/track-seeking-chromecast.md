---
title: Spåra sökning på Chromecast
description: I det här avsnittet beskrivs hur du implementerar sökspårning med Media SDK på Chromecast.
uuid: 8018e6c4-fed9-4de7-9eae-c720da55ad8c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra sökning på Chromecast{#track-seeking-on-chromecast}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Sökspårningskonstanter

| Konstantnamn | Beskrivning |
|---|---|
| `SeekStart` | Konstant för spårning av Seek Start-händelse. |
| `SeekComplete` | Konstant för spårning av händelsen Sökning slutförd. |

## Implementeringssökning

1. Lyssna efter uppspelningssökningshändelser från mediespelaren och spåra sökning med hjälp av `SeekStart` händelsen vid sökningshändelsemeddelanden: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekStart); 
   ```

1. Spåra slutet av sökningen med händelsen när du söker ett fullständigt meddelande från mediespelaren: `SeekComplete` [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekComplete); 
   ```

Mer information finns i spårningsscenariot för [VOD-uppspelning med sökning i huvudinnehållet](/help/sdk-implement/tracking-scenarios/vod-seeking.md) .

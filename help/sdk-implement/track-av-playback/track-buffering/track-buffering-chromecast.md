---
title: Spåra buffring på Chromecast
description: Beskriver spårning av buffringshändelser i Chromecast.
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra buffring på Chromecast{#track-buffering-on-chromecast}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Konstanter för buffertspårning


| Konstantnamn | Beskrivning |
|---|---|
| `BufferStart` | Konstant för spårning av buffertens starthändelse |
| `BufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och spåra buffring med hjälp av `BufferStart` händelsen vid meddelande om buffertstart: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. Spåra slutet av buffringen med händelsen `BufferComplete` vid buffertmeddelande från mediespelaren: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

Mer information finns i [VOD-uppspelning för spårningsscenarier med buffring](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .

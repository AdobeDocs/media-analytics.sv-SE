---
title: Lär dig spåra buffring på Chromecast
description: Lär dig spåra buffringshändelser på Chromecast.
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
exl-id: 26fd1e2a-4103-486f-be12-36b088d28cb6
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Spåra buffring på Chromecast{#track-buffering-on-chromecast}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Konstanter för buffertspårning


| Konstantnamn | Beskrivning     |
|---|---|
| `BufferStart` | Konstant för spårning av buffertens starthändelse |
| `BufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och spåra buffring med händelsen `BufferStart` vid meddelande om starthändelse för buffert: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. Spåra slutet av buffringen med händelsen `BufferComplete` när bufferten är klar från mediespelaren: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med buffring](/help/sdk-implement/tracking-scenarios/vod-buffering.md).

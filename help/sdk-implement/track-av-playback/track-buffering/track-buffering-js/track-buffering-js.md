---
title: Spåra buffring med JavaScript 2.x
description: Beskriver spårning av buffringshändelser i webbläsarprogram (JS).
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Spåra buffring med JavaScript 2.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Konstanter för buffertspårning

| Konstantnamn | Beskrivning     |
|---|---|
| `BufferStart` | Konstant för spårning av buffertens starthändelse |
| `BufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och spåra buffring med hjälp av `BufferStart` händelsen vid buffertstartsmeddelanden.

   ```js
   _onBufferStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
   };
   ```

1. Spåra slutet av buffringen med händelsen `BufferComplete` när ett meddelande om att bufferten har slutförts skickas från mediespelaren.

   ```js
   _onBufferComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
   };
   ```

Mer information finns i [VOD-uppspelning för spårningsscenarier med buffring](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .

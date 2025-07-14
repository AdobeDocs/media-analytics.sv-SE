---
title: Lär dig spåra buffring med JavaScript 3.x
description: Lär dig spåra buffringshändelser i webbläsarappar (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Spåra buffring med JavaScript 3.x{#track-buffering-on-javascript}

Följande instruktioner ger vägledning för implementering i alla 3.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Konstanter för buffertspårning

| Konstantnamn | Beskrivning     |
|---|---|
| `BufferStart` | Konstant för spårning av buffertens starthändelse |
| `BufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och spåra buffring med händelsen `BufferStart` vid meddelanden om start av buffert.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Spåra slutet av buffringen med händelsen `BufferComplete` när ett meddelande om att bufferten har slutförts från mediespelaren.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med buffring](/help/use-cases/tracking-scenarios/vod-buffering.md).

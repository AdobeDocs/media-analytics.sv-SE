---
title: Lär dig spåra buffring med JavaScript 3.x
description: Lär dig hur du spårar buffringshändelser i webbläsarappar (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Spåra buffring med JavaScript 3.x{#track-buffering-on-javascript}

Följande instruktioner ger vägledning för implementering i alla 3.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandböckerna här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Konstanter för buffertspårning

| Konstantnamn | Beskrivning     |
|---|---|
| `BufferStart` | Konstant för spårning av buffertens starthändelse |
| `BufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och spåra buffring med händelsen `BufferStart` vid meddelande om start av buffert.

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

Mer information finns i spårningsscenariot [VOD-uppspelning med buffring](/help/sdk-implement/tracking-scenarios/vod-buffering.md).

---
title: Lär dig spåra buffring med JavaScript 2.x
description: Lär dig spåra buffringshändelser i webbläsarappar (JS).
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
exl-id: 62c1d5b4-2717-42b3-8343-d41e895a9da3
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Spåra buffring med JavaScript 2.x{#track-buffering-on-javascript}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK.](/help/getting-started/download-sdks.md)

## Konstanter för buffertspårning

| Konstantnamn | Beskrivning     |
|---|---|
| `BufferStart` | Konstant för spårning av buffertens starthändelse |
| `BufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och spåra buffring med händelsen `BufferStart` vid meddelanden om start av buffert.

   ```js
   _onBufferStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
   };
   ```

1. Spåra slutet av buffringen med händelsen `BufferComplete` när ett meddelande om att bufferten har slutförts från mediespelaren.

   ```js
   _onBufferComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
   };
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med buffring](/help/use-cases/tracking-scenarios/vod-buffering.md).

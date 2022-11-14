---
title: Lär dig spåra buffring med JavaScript 2.x
description: Lär dig hur du spårar buffringshändelser i webbläsarappar (JS).
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
exl-id: 62c1d5b4-2717-42b3-8343-d41e895a9da3
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Spåra buffring med JavaScript 2.x{#track-buffering-on-javascript}

Följande instruktioner ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Konstanter för buffertspårning

| Konstantnamn | Beskrivning     |
|---|---|
| `BufferStart` | Konstant för spårning av buffertens starthändelse |
| `BufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och vid meddelanden om starthändelser för buffert, spåra buffring med hjälp av `BufferStart` -händelse.

   ```js
   _onBufferStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
   };
   ```

1. Spåra slutet av buffringen med `BufferComplete` -händelse.

   ```js
   _onBufferComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
   };
   ```

Se spårningsscenariot [VOD-uppspelning med buffring](/help/use-cases/tracking-scenarios/vod-buffering.md) för mer information.

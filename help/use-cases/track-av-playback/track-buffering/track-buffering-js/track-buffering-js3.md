---
title: Lär dig spåra buffring med JavaScript 3.x
description: Lär dig hur du spårar buffringshändelser i webbläsarappar (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Spåra buffring med JavaScript 3.x{#track-buffering-on-javascript}

Följande instruktioner ger vägledning för implementering i alla 3.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandböckerna här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Konstanter för buffertspårning

| Konstantnamn | Beskrivning     |
|---|---|
| `BufferStart` | Konstant för spårning av buffertens starthändelse |
| `BufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och vid meddelanden om starthändelser för buffert, spåra buffring med hjälp av `BufferStart` -händelse.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Spåra slutet av buffringen med `BufferComplete` -händelse.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Se spårningsscenariot [VOD-uppspelning med buffring](/help/use-cases/tracking-scenarios/vod-buffering.md) för mer information.

---
title: Lär dig spåra buffring på Android
description: Lär dig spåra buffringshändelser på Android.
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Spåra buffring på Android{#track-buffering-on-android}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDks.](/help/getting-started/download-sdks.md)

## Konstanter för buffertspårning

| Konstantnamn | Beskrivning     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | Konstant för spårning av buffertens starthändelse |
| `MediaHeartbeat.Event.BufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och spåra buffring med händelsen `BufferStart` vid meddelande om buffertstart:

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null);
   }
   ```

1. Spåra slutet av buffringen med händelsen `BufferComplete` när bufferten är klar från mediespelaren:

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null);
   }
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med buffring](/help/use-cases/tracking-scenarios/vod-buffering.md).

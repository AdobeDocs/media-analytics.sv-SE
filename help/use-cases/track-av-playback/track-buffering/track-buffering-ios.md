---
title: Lär dig spåra buffring på iOS
description: Lär dig spåra buffringshändelser på iOS.
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
exl-id: 5f0a3c4b-7c9e-499d-98d0-6fcf316c4d9c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Spåra buffring på iOS{#track-buffering-on-ios}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK.](/help/getting-started/download-sdks.md)

## Konstanter för buffertspårning


| Konstantnamn | Beskrivning     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Konstant för spårning av buffertens starthändelse |
| `ADBMediaHeartbeatEventBufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och spåra buffring med händelsen `BufferStart` vid meddelande om buffertstart:

   ```
   - (void)onBufferStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Spåra slutet av buffringen med händelsen `BufferComplete` när bufferten är klar från mediespelaren:

   ```
   - (void)onBufferComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med buffring](/help/use-cases/tracking-scenarios/vod-buffering.md).

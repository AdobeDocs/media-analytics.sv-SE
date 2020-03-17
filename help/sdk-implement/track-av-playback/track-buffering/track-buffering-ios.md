---
title: Spåra buffring på iOS
description: Beskriver spårning av buffringshändelser på iOS.
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra buffring på iOS{#track-buffering-on-ios}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Konstanter för buffertspårning


| Konstantnamn | Beskrivning |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Konstant för spårning av buffertens starthändelse |
| `ADBMediaHeartbeatEventBufferComplete` | Konstant för spårning av händelsen Buffer Complete |

## Implementera buffring

1. Lyssna efter uppspelningsbuffringshändelser från mediespelaren och spåra buffring med hjälp av `BufferStart` händelsen vid meddelande om buffertstart:

   ```
   - (void)onBufferStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Spåra slutet av buffringen med händelsen `BufferComplete` vid buffertmeddelande från mediespelaren:

   ```
   - (void)onBufferComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Mer information finns i [VOD-uppspelning för spårningsscenarier med buffring](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .

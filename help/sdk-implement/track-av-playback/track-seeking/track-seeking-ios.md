---
title: Lär dig spåra sökning på iOS
description: Lär dig spåra händelserna Seek Start och Seek Complete med Media SDK på iOS.
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
exl-id: e8cb4962-2a14-4bfe-9a25-2405e503ba0b
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Spåra sökning på iOS{#track-seeking-on-ios}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Sökspårningskonstanter

| Konstantnamn | Beskrivning     |
|---|---|
| `ADBMediaHeartbeatEventSeekStart` | Konstant för spårning av Seek Start-händelse. |
| `ADBMediaHeartbeatEventSeekComplete` | Konstant för spårning av händelsen Sökning slutförd. |

## Implementeringssökning

1. Lyssna efter uppspelningssökningshändelser från mediespelaren och spåra sökning med händelsen `SeekStart` vid sökningen efter start:

   ```
   - (void)onSeekStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Spåra slutet av sökningen med händelsen `SeekComplete` när du söker efter ett fullständigt meddelande från mediespelaren:

   ```
   - (void)onSeekComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Mer information finns i spårningsscenariot [VOD-uppspelning med sökning i huvudinnehållet](/help/sdk-implement/tracking-scenarios/vod-seeking.md).

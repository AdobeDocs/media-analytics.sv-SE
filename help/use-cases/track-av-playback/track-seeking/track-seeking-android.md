---
title: Lär dig spåra sökning på Android
description: Lär dig spåra händelserna Seek Start och Seek Complete med Media SDK i Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
exl-id: 8a8fcbcf-3232-4565-8c27-4167b6741613
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Spåra sökning på Android{#track-seeking-on-android}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK.](/help/getting-started/download-sdks.md)

## Sökspårningskonstanter

| Konstantnamn | Beskrivning     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Konstant för spårning av Seek Start-händelse. |
| `MediaHeartbeat.Event.SeekComplete` | Konstant för spårning av händelsen Sökning slutförd. |

## Implementeringssökning

1. Lyssna efter uppspelningssökningshändelser från mediespelaren och spåra sökning med händelsen `SeekStart` vid sökningen efter starthändelse:

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null);
   }
   ```

1. Spåra slutet av sökningen med händelsen `SeekComplete` när du söker efter ett fullständigt meddelande från mediespelaren:

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null);
   }
   ```

Mer information finns i spårningsscenariot [VOD uppspelning med sökning i huvudinnehållet](/help/use-cases/tracking-scenarios/vod-seeking.md).

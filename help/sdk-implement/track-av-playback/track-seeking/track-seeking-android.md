---
title: Spåra sökning på Android
description: I det här avsnittet beskrivs hur du implementerar sökspårning med Media SDK på Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra sökning på Android{#track-seeking-on-android}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Sökspårningskonstanter

| Konstantnamn | Beskrivning |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Konstant för spårning av Seek Start-händelse. |
| `MediaHeartbeat.Event.SeekComplete` | Konstant för spårning av händelsen Sökning slutförd. |

## Implementeringssökning

1. Lyssna efter uppspelningssökningshändelser från mediespelaren och spåra sökning med hjälp av `SeekStart` händelsen vid sökningshändelsemeddelanden:

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. Spåra slutet av sökningen med händelsen när du söker ett fullständigt meddelande från mediespelaren: `SeekComplete`

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

Mer information finns i spårningsscenariot för [VOD-uppspelning med sökning i huvudinnehållet](/help/sdk-implement/tracking-scenarios/vod-seeking.md) .

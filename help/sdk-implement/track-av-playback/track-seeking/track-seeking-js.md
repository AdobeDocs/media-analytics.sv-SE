---
title: Spåra sökning i JavaScript
description: I det här avsnittet beskrivs hur du implementerar sökspårning med Media SDK i webbläsarprogram (JS).
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra sökning i JavaScript{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>Följande instruktioner ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Sökspårningskonstanter

| Konstantnamn | Beskrivning |
|---|---|
| `SeekStart` | Konstant för spårning av Seek Start-händelse. |
| `SeekComplete` | Konstant för spårning av händelsen Sökning slutförd. |

## Implementeringssökning

1. Lyssna efter uppspelningssökningshändelser från mediespelaren och spåra sökning med hjälp av `SeekStart` händelsen vid sökningshändelsemeddelanden:

   ```js
   _onSeekStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
   };
   ```

1. Spåra slutet av sökningen med händelsen när du söker ett fullständigt meddelande från mediespelaren: `SeekComplete`

   ```js
   _onSeekComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
   };
   ```

Mer information finns i spårningsscenariot för [VOD-uppspelning med sökning i huvudinnehållet](/help/sdk-implement/tracking-scenarios/vod-seeking.md) .

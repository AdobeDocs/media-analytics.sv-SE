---
title: Lär dig spåra sökning med JavaScript 2.x
description: Lär dig spåra händelserna Seek Start och Seek Complete med Media SDK i webbläsarappar (JS 2.x).
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
exl-id: 90f35376-24d8-405d-82b4-d6b737acf7b9
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Spåra sökning med JavaScript 2.x{#track-seeking-on-javascript}

Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK.](/help/getting-started/download-sdks.md)

## Sökspårningskonstanter

| Konstantnamn | Beskrivning     |
|---|---|
| `SeekStart` | Konstant för spårning av Seek Start-händelse. |
| `SeekComplete` | Konstant för spårning av händelsen Sökning slutförd. |

## Implementeringssökning

1. Lyssna efter uppspelningssökningshändelser från mediespelaren och spåra sökning med händelsen `SeekStart` vid sökningen efter starthändelse:

   ```js
   _onSeekStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
   };
   ```

1. Spåra slutet av sökningen med händelsen `SeekComplete` när du söker efter ett fullständigt meddelande från mediespelaren:

   ```js
   _onSeekComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
   };
   ```

Mer information finns i spårningsscenariot [VOD uppspelning med sökning i huvudinnehållet](/help/use-cases/tracking-scenarios/vod-seeking.md).

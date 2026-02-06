---
title: Spåra sökning med JavaScript 3.x
description: Lär dig spåra händelserna Seek Start och Seek Complete med Media SDK i webbläsarappar (JS 3.x).
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Spåra sökning med JavaScript 3.x{#track-seeking-on-javascript}

Följande instruktioner ger vägledning för implementering i alla 3.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandboken här: [Hämta SDK:er.](/help/getting-started/download-sdks.md)

## Sökspårningskonstanter

| Konstantnamn | Beskrivning     |
|---|---|
| `SeekStart` | Konstant för spårning av Seek Start-händelse. |
| `SeekComplete` | Konstant för spårning av händelsen Sökning slutförd. |

## Implementeringssökning

1. Lyssna efter uppspelningssökningshändelser från mediespelaren och spåra sökning med händelsen `SeekStart` vid sökningen efter starthändelse:

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. Spåra slutet av sökningen med händelsen `SeekComplete` när du söker efter ett fullständigt meddelande från mediespelaren:

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

Mer information finns i spårningsscenariot [VOD uppspelning med sökning i huvudinnehållet](/help/use-cases/tracking-scenarios/vod-seeking.md).

---
title: Lär dig spåra sökning med JavaScript 3.x
description: Lär dig hur du spårar händelserna Seek Start och Seek Complete med Media SDK i webbläsarappar (JS 3.x).
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Spåra sökning med JavaScript 3.x{#track-seeking-on-javascript}

Följande instruktioner ger vägledning för implementering i alla 3.x SDK:er.

>[!IMPORTANT]
>
>Om du implementerar en tidigare version av SDK kan du hämta utvecklarhandböckerna här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Sökspårningskonstanter

| Konstantnamn | Beskrivning     |
|---|---|
| `SeekStart` | Konstant för spårning av Seek Start-händelse. |
| `SeekComplete` | Konstant för spårning av händelsen Sökning slutförd. |

## Implementeringssökning

1. Lyssna efter uppspelningssökningshändelser från mediespelaren och spåra sökning med händelsen `SeekStart` vid sökningen efter start:

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

Mer information finns i spårningsscenariot [VOD-uppspelning med sökning i huvudinnehållet](/help/sdk-implement/tracking-scenarios/vod-seeking.md).

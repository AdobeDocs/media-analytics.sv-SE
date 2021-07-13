---
title: Lär dig spåra sökning med JavaScript 2.x
description: Lär dig hur du spårar händelserna Seek Start och Seek Complete med Media SDK i webbläsarappar (JS 2.x).
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
exl-id: 90f35376-24d8-405d-82b4-d6b737acf7b9
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Spåra sökning med JavaScript 2.x{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Sökspårningskonstanter

| Konstantnamn | Beskrivning     |
|---|---|
| `SeekStart` | Konstant för spårning av Seek Start-händelse. |
| `SeekComplete` | Konstant för spårning av händelsen Sökning slutförd. |

## Implementeringssökning

1. Lyssna efter uppspelningssökningshändelser från mediespelaren och spåra sökning med händelsen `SeekStart` vid sökningen efter start:

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

Mer information finns i spårningsscenariot [VOD-uppspelning med sökning i huvudinnehållet](/help/sdk-implement/tracking-scenarios/vod-seeking.md).

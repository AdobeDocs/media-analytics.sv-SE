---
title: Spåra sökning på Roku
description: I det här avsnittet beskrivs hur du implementerar sökspårning med Media SDK på Roku.
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra sökning på Roku{#track-seeking-on-roku}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

## Sökspårningskonstanter

| Konstantnamn | Beskrivning |
|---|---|
| `SeekStart` | Konstant för spårning av Seek Start-händelse. |
| `SeekComplete` | Konstant för spårning av händelsen Sökning slutförd. |

## Implementeringssökning

1. Lyssna efter uppspelningssökningshändelser från mediespelaren och spåra sökning med hjälp av `SeekStart` händelsen vid sökningshändelsemeddelanden.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. Spåra slutet av sökningen med händelsen när du söker efter ett fullständigt meddelande från mediespelaren `SeekComplete` .

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

Mer information finns i spårningsscenariot för [VOD-uppspelning med sökning i huvudinnehållet](/help/sdk-implement/tracking-scenarios/vod-seeking.md) .

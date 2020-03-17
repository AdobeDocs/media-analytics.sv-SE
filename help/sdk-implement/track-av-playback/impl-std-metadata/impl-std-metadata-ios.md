---
title: Implementera standardmetadata på iOS
description: Beskriver hur du ställer in standardmetadata för video och annonsering som ska skickas med spårningsanrop på iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementera standardmetadata på iOS{#implement-standard-metadata-on-ios}

## Metadatakonstanter

| Konstantnamn | Beskrivning |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Konstant för att bifoga standardmetadata på `MediaInfo ADBMediaObject` |

## Implementering

1. Skapa en ordlista med standardvärdepar för metadata med `ADBStandardMetadataKeys`
   [IOS-metadatanycklar](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Ange standardmetadataordlistan för `MediaInfo``ADBMediaObject` instansen med standardmetadatakonstanten för metadata.

1. Ange det här `MediaInfo` objektet när du anropar `trackSessionStart` API:t.

### Exempel på implementering

Instansiera ett metadataobjekt av standardtyp, fyll i önskade variabler och ange metadataobjektet i objektet Mediepulsslag. Exempel:

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```


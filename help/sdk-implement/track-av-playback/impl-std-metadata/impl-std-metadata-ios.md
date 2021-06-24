---
title: Lär dig hur du implementerar standardmetadata i iOS
description: Lär dig hur du ställer in standardmetadata för video och annonsering som ska skickas med spårningsanrop på iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 8%

---

# Implementera standardmetadata i iOS{#implement-standard-metadata-on-ios}

## Metadatakonstanter

| Konstantnamn | Beskrivning   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Konstant för att bifoga standardmetadata på `MediaInfo ADBMediaObject` |

## Implementering

1. Skapa en ordlista med standardvärdepar för metadata med `ADBStandardMetadataKeys`
   [IOS-metadatanycklar](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Ange standardmetadataordlistan på `MediaInfo` `ADBMediaObject`-instansen med standardmetadatakonstanten för metadata.

1. Ange det här `MediaInfo`-objektet när du anropar API:t `trackSessionStart`.

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

---
title: Lär dig hur du implementerar standardmetadata i iOS
description: Lär dig hur du ställer in standardmetadata för video och annonsering som ska skickas med spårningsanrop till iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 3%

---

# Implementera standardmetadata på iOS{#implement-standard-metadata-on-ios}

## Metadatakonstanter

| Konstantnamn | Beskrivning   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Konstant för att bifoga standardmetadata på `MediaInfo ADBMediaObject` |

## Implementering

1. Skapa en ordlista med standardvärdepar för metadata med `ADBStandardMetadataKeys`
   [IOS metadatanycklar](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Ange standardmetadataordlistan för instansen `MediaInfo` `ADBMediaObject` med standardmetadatakonstanten för metadata.

1. Ange det här `MediaInfo`-objektet när `trackSessionStart`-API:t anropas.

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

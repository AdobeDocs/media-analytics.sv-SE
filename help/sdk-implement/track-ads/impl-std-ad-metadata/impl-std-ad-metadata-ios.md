---
title: Implementera standardannonsmetadata på iOS
description: Så här använder du standardmetadata för annonser i annonsspårning på iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementera standardannonsmetadata på iOS{#implement-standard-ad-metadata-on-ios}

## Annonskonstanter

| Konstantnamn | Beskrivning |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Konstant för att bifoga standardannonsmetadata på `AdInfo ADBMediaObject` |

## Implementera standardannonsmetadata

För standardannonsmetadata skapar du en ordlista med nyckelvärdepar för standardannonsmetadata med hjälp av tangenterna för din plattform:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS-metadatanycklar](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

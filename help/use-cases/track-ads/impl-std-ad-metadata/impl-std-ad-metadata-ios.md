---
title: Lär dig hur du implementerar standardmetadata för annonsering på iOS
description: Så här använder du standardmetadata för annonser i annonsuppföljning på iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# Implementera standardannonsmetadata på iOS{#implement-standard-ad-metadata-on-ios}

## Annonskonstanter

| Konstantnamn | Beskrivning   |
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

[iOS metadatanycklar](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

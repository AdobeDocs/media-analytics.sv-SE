---
title: Implementera standardannonsmetadata på Android
description: Så här använder du standardmetadata för annonser i annonsspårning på Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementera standardannonsmetadata på Android{#implement-standard-ad-metadata-on-android}

## Annonskonstanter

| Konstantnamn | Beskrivning |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Konstant för att bifoga standardannonsmetadata på annons `MediaObject`. |

## Implementera standardannonsmetadata

För standardannonsmetadata skapar du en ordlista med nyckelvärdepar för standardannonsmetadata med hjälp av tangenterna för din plattform:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```


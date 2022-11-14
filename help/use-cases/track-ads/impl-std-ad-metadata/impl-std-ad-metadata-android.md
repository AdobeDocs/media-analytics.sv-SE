---
title: Lär dig hur du implementerar standardmetadata för annonsering på Android
description: Så här använder du standardmetadata för annonser i annonsspårning på Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 11%

---

# Implementera standardmetadata för annonser i Android{#implement-standard-ad-metadata-on-android}

## Annonskonstanter

| Konstantnamn | Beskrivning   |
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

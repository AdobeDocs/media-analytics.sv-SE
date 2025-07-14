---
title: Lär dig hur du implementerar standardmetadata för annonsering på Android
description: Så här använder du standardmetadata för annonser i annonsuppföljning på Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Implementera standardannonsmetadata på Android{#implement-standard-ad-metadata-on-android}

## Annonskonstanter

| Konstantnamn | Beskrivning   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Konstant för att bifoga standardannonsmetadata på annonsen `MediaObject`. |

## Implementera standardannonsmetadata

För standardannonsmetadata skapar du en ordlista med nyckelvärdepar för standardannonsmetadata med hjälp av tangenterna för din plattform:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

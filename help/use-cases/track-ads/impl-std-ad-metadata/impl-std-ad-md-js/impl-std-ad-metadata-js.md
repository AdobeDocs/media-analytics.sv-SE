---
title: Lär dig implementera standardmetadata för annonsering med JavaScript 2.x
description: Så här använder du standardmetadata för annonser i annonsspårning i en webbläsare med JavaScript 2.x-appar.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
exl-id: b331db87-ab4e-44fa-a97c-9691974cacd4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 1%

---

# Implementera standardannonsmetadata med JavaScript 2.x{#implement-standard-ad-metadata-on-javascript}

## Annonskonstanter

| Konstantnamn | Beskrivning   |
|---|---|
| `StandardAdMetadata` | Konstant för att bifoga standardannonsmetadata i annonsobjekt |

## Implementera standardannonsmetadata

För standardannonsmetadata skapar du en ordlista med nyckelvärdepar för standardannonsmetadata med hjälp av tangenterna för din plattform:

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>);

// Set standard Ad Metadata
var standardAdMetadata = {};
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```

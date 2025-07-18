---
title: Lär dig implementera standardmetadata för annonsering med JavaScript 3.x
description: Så här använder du standardmetadata för annonser i annonsspårning i en webbläsare med JavaScript 3.x-appar.
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Implementera standardannonsmetadata med JavaScript 3.x{#implement-standard-ad-metadata-on-javascript}

## Implementera standardannonsmetadata

För standardannonsmetadata skapar du en ordlista med nyckelvärdepar för standardannonsmetadata med hjälp av tangenterna för din plattform:

```js
var adObject =
ADB.Media.createAdObject(<AD_NAME>,
                              <AD_ID>,
                              <POSITION>,
                              <LENGTH>);

// Set standard Ad Metadata
var adMetadata = {};
adMetadata[MediaHeartbeat.AdMetadataKeys.Advertiser] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CampaignId] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```

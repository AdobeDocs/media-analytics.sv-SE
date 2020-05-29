---
title: Implementera standardannonsmetadata med JavaScript 3.x
description: Så här använder du standardmetadata för annonser i annonsspårning i en webbläsare med JavaScript 3.x-appar.
translation-type: tm+mt
source-git-commit: 83b38ac8f7fc88f982d194e776efccf8d5b983e4
workflow-type: tm+mt
source-wordcount: '54'
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

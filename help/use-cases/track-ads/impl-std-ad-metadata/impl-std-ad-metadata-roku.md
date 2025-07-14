---
title: Lär dig hur du implementerar standardmetadata för annonsering på Roku
description: Så här använder du standardmetadata för annonser i annonsuppföljning på Roku.
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
exl-id: d2c0a1e0-8d40-4f60-a82d-5860550ac152
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Implementera standardannonsmetadata på Roku{#implement-standard-ad-metadata-on-roku}

## Implementera standardannonsmetadata

För standardannonsmetadata skapar du en ordlista med nyckelvärdepar för standardannonsmetadata med hjälp av tangenterna för din plattform:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

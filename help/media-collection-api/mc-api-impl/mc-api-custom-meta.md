---
title: Stöd för anpassade metadata
description: Stöd för anpassade metadata
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Stöd för anpassade metadata{#custom-metadata-support}

Du kan ange anpassade nyckel:värde-par för händelserna `sessionStart`, `chapterStart` och `adStart`. Den här informationen måste anges i JSON-nyckeln, `customMetadata`, placerad bredvid `params`-tangenten.

JSON-nyckeln `customMetadata` ska innehålla ett objekt med nyckelvärdepar. Nyckeln får endast innehålla alfanumeriska tecken, understrykning och punkt/punkt.

[API-händelser för MA-samling](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

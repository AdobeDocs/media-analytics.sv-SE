---
title: Stöd för anpassade metadata
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Stöd för anpassade metadata{#custom-metadata-support}

Du kan ange anpassade nyckel:värde-par för händelserna `sessionStart`, `chapterStart`och `adStart` . Denna information måste anges i JSON-nyckeln, `customMetadata`placerad bredvid `params` nyckeln.

JSON- `customMetadata` tangenten ska innehålla ett objekt med nyckel:value-par. Nyckeln får endast innehålla alfanumeriska tecken, understrykning och punkt/punkt.

[API-händelser för MA-samling](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)


---
title: Stöd för anpassade metadata
description: "Lär dig hur du anger anpassade nyckel:värde-par för händelserna sessionStart, ChapterStart och adStart."
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# Stöd för anpassade metadata{#custom-metadata-support}

Du kan ange anpassade nyckel:värde-par på `sessionStart`, `chapterStart`och `adStart` händelser. Denna information måste anges i JSON-nyckeln. `customMetadata`, placerad bredvid `params` nyckel.

The `customMetadata` JSON-tangenten ska innehålla ett objekt med nyckel:värde-par. Nyckeln får endast innehålla alfanumeriska tecken, understruken text och punkt/punkt.

[API-händelser för MA-samling](../mc-api-ref/mc-api-events-req.md)

## Exempel

För närvarande kan du skicka en `sessionStart` händelse med följande nyckel:value-par:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

För konfigurationen ovan är rapportdata som skickas till analyser följande:

`c.a.media.channel=channel-2`

### Rekommendation

Vi rekommenderar att du använder ett separat namnutrymme för anpassade metadata. Exempel:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

I det rekommenderade exemplet är rapportdata för anpassade metadata som skickas till analyser följande:

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`

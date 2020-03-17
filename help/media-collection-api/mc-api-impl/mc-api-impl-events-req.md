---
title: Implementera en eventförfrågan
description: null
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Implementera en eventförfrågan{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Använd [händelsebegäran](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) för alla efterföljande spårningsanrop när du har fått ett sessions-ID med hjälp av [sessionsbegäran.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Ange spelhuvudets plats och tidsstämpel, händelsetyp och eventuella parametrar som du vill inkludera i JSON-brödtexten för begäran.

JSON-begärandetexten för [händelsebegäran](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) har samma struktur som Sessions-begäran, men kontrollera [JSON-valideringsscheman](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) för parameterkrav och typer.

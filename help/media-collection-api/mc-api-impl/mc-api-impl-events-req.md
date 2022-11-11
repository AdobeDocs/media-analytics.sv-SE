---
title: Implementera en händelsebegäran
description: Lär dig hur du använder slutpunkten för händelsebegäran för alla efterföljande spårningsanrop när du har fått ett sessions-ID
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 4%

---

# Implementera en eventförfrågan{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Använd [Händelsebegäran](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) för alla efterföljande spårningsanrop efter att du har fått ett sessions-ID med [Sessionsbegäran.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Ange spelhuvudets plats och tidsstämpel, händelsetyp och eventuella parametrar som du vill inkludera i JSON-brödtexten för begäran.

JSON-begärandetexten för [Händelsebegäran](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) har samma struktur som Sessions-begäran, men kontrollera [JSON-valideringsscheman](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) för parameterkrav och -typer.

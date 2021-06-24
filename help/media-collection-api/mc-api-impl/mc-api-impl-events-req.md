---
title: Implementera en händelsebegäran
description: Lär dig hur du använder slutpunkten för händelsebegäran för alla efterföljande spårningsanrop när du har fått ett sessions-ID
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 3%

---

# Implementera en eventförfrågan{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Använd [Händelsebegäran](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) för alla efterföljande spårningsanrop när du har fått ett sessions-ID med [sessionsbegäran.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Ange spelhuvudets plats och tidsstämpel, händelsetyp och eventuella parametrar som du vill inkludera i JSON-brödtexten för begäran.

JSON-begärandetexten för [händelsebegäran](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) har samma struktur som Sessions-begäran, men kontrollera [JSON-valideringsscheman](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) för parameterkrav och typer.

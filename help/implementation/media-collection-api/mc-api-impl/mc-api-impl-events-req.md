---
title: Implementera en händelsebegäran
description: Lär dig hur du använder slutpunkten för händelsebegäran för alla efterföljande spårningsanrop när du har fått ett sessions-ID
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Implementera en eventförfrågan{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Använd [Händelsebegäran](../mc-api-ref/mc-api-events-req.md) för alla efterföljande spårningsanrop när du har fått ett sessions-ID med hjälp av [sessionsbegäran.](../mc-api-ref/mc-api-sessions-req.md) Ange spelhuvudets plats och tidsstämpel, händelsetyp och eventuella parametrar som du vill inkludera i JSON-delen av begäran.

JSON-begärandetexten för [Händelsebegäran](../mc-api-ref/mc-api-events-req.md) har samma struktur som Sessions-begäran, men kontrollera [JSON-valideringsscheman](../mc-api-ref/mc-api-json-validation.md) för parameterkrav och typer.

---
title: Skicka QoE-data
description: Lär dig hur du skickar händelser med en qoeData JSON-nyckel.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '57'
ht-degree: 5%

---

# Skicka QoE-data{#sending-qoe-data}

Alla händelser kan dekoreras med en extra JSON-nyckel som heter `qoeData`, som placeras bredvid `params`-nyckeln i JSON-begärandetexten.

>[!NOTE]
>
>Du bör kontrollera [JSON-valideringsscheman](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md) för att kontrollera parametertyper och om de är obligatoriska eller valfria.

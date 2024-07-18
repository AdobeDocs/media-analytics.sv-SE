---
title: Skicka QoE-data
description: Lär dig hur du skickar händelser med en qoeData JSON-nyckel.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 0%

---

# Skicka QoE-data{#sending-qoe-data}

Alla händelser kan dekoreras med en extra JSON-nyckel som heter `qoeData`, som placeras bredvid `params`-nyckeln i JSON-begärandetexten.

>[!NOTE]
>
>Du bör kontrollera [JSON-valideringsscheman](mc-api-validate-reqs.md) för att verifiera parametertyper och om de är obligatoriska eller valfria.

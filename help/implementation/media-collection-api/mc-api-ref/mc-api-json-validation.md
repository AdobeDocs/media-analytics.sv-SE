---
title: JSON-valideringsscheman för direktuppspelning av medietjänster
description: Vad är JSON-valideringsscheman för strömmande media och hur används de för att fastställa rätt innehållsparametrar för begäran för varje typ av händelse.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# JSON-valideringsscheman{#json-validation-schemas}

Back-end för Streaming Media Collection validerar parametrarna för förfrågningar för varje händelsetyp med JSON-valideringsscheman. Dessa scheman är tillgängliga för dig och fungerar som den aktuella behörigheten för parametertyper som används i MA API.

`GET https://{uri}/api/v1/schemas/{event-type}`

Mer information om hur du använder JSON-valideringsscheman finns i [Validera händelsebegäranden.](../mc-api-impl/mc-api-validate-reqs.md)

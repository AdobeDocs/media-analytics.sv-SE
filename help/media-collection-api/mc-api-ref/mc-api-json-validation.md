---
title: JSON-valideringsscheman för direktuppspelad medieanalys
description: Vad är JSON-valideringsscheman för strömmande media och hur används de för att fastställa rätt innehållsparametrar för begäran för varje typ av händelse.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# JSON-valideringsscheman{#json-validation-schemas}

Baksidan av Media Analytics validerar parametrarna för förfrågningar för varje händelsetyp med JSON-valideringsscheman. Dessa scheman är tillgängliga för dig och fungerar som den aktuella behörigheten för parametertyper som används i MA API.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Mer information om hur du använder JSON-valideringsscheman finns i [Validera händelsebegäranden.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

---
title: JSON-valideringsscheman
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: 9b2f8b14ddb5b814f57c752665b78409e31173e8
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 0%

---


# JSON-valideringsscheman{#json-validation-schemas}

Baksidan av Media Analytics validerar parametrarna för förfrågningar för varje händelsetyp med JSON-valideringsscheman. Dessa scheman är tillgängliga för dig och fungerar som den aktuella behörigheten för parametertyper som används i MA API.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Mer information om hur du använder JSON-valideringsscheman finns i [Validerar händelsebegäranden.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

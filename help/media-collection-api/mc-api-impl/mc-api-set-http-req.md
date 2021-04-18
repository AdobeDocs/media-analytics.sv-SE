---
title: Ställa in HTTP-begärantypen i spelaren
description: Ställa in HTTP-begärantypen i spelaren
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# Ange HTTP-begärantypen {#setting-the-http-request-type}

Begärandetexten för alla Media Collection API-begäranden måste vara i JSON-format, så du bör ange innehållets begärandetyp i spelaren. I JavaScript skulle du till exempel ange begärandehuvudet `Content-Type` enligt följande:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

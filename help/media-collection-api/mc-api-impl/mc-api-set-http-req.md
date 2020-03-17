---
title: Ställa in HTTP-begärantypen i spelaren
description: null
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Ange HTTP-begärantyp {#setting-the-http-request-type}

Begärandetexten för alla Media Collection API-begäranden måste vara i JSON-format, så du bör ange innehållets begärandetyp i spelaren. I JavaScript skulle du till exempel ange begärandehuvudet på följande sätt `Content-Type` :

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```


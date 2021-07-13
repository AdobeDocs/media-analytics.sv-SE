---
title: Ange typ av HTTP-begäran i spelaren
description: 'Begärandetexten för alla API-begäranden för direktuppspelad mediainsamling måste vara i JSON-format. Lär dig hur du ställer in innehållets begärandetyp i spelaren. '
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 10%

---

# Ange HTTP-begärantyp {#setting-the-http-request-type}

Begärandetexten för alla Media Collection API-begäranden måste vara i JSON-format, så du bör ange innehållets begärandetyp i spelaren. I JavaScript skulle du till exempel ange begärandehuvudet `Content-Type` enligt följande:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

---
title: Ange typ av HTTP-begäran i spelaren
description: Begärandetexten för alla API-begäranden för direktuppspelad mediainsamling måste vara i JSON-format. Lär dig hur du ställer in innehållets begärandetyp i spelaren.
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '76'
ht-degree: 10%

---

# Ange HTTP-begärantyp {#setting-the-http-request-type}

Begärandetexten för alla Media Collection API-begäranden måste vara i JSON-format, så du bör ange innehållets begärandetyp i spelaren. I JavaScript skulle du till exempel ange `Content-Type` begäranhuvud enligt följande:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

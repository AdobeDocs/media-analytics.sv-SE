---
title: Hämta ett sessions-ID
description: Lär dig hur du kodar en sessionsbegäran för att hämta sessions-ID från platshuvudet i ett svar.
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
exl-id: 4a1c4ade-4a5e-4af0-8117-19d718dd8bda
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 6%

---

# Hämta ett sessions-ID{#obtaining-a-session-id}

I det här kodfragmentet från referensspelaren visas ett sätt att koda en [sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) tillsammans med att extrahera sessions-ID (och API-versionen för Media Collection) från platshuvudet i svaret:

```js
var  
sessionData = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
...

const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    ...
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data": sessionData             // Mandatory params 
     }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    ...
```

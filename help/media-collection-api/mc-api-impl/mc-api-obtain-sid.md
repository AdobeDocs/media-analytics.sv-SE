---
title: Hämta ett sessions-ID
description: null
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Hämta ett sessions-ID{#obtaining-a-session-id}

I det här kodfragmentet från referensspelaren visas ett sätt att koda en [sessionsbegäran,](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) tillsammans med att extrahera sessions-ID (och API-versionen för Media Collection) från platshuvudet i svaret:

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


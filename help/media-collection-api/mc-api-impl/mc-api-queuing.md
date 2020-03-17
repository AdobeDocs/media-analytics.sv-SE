---
title: Köa händelser när sessionens svar är långsamt
description: null
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Köa händelser när sessionens svar är långsamt{#queueing-events-when-sessions-response-is-slow}

Media Collection API är RESTful: Du gör alltså en HTTP-begäran och väntar på svaret. Detta är bara en viktig punkt när du begär [att få ett sessions-ID i början av videouppspelningen när du gör en](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) sessionsbegäran. Detta är viktigt eftersom sessions-ID krävs för alla efterföljande spårningsanrop.

Det är möjligt att spelaren kan utlösa händelser _innan sessionssvaret returnerar_ (med parametern Session ID) från serverdelen. Om detta inträffar måste programmet placera eventuella spårningshändelser i kö som kommer mellan [sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) och dess svar. När sessionssvaret kommer, bör du först bearbeta alla [händelser](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)som står i kö och sedan börja bearbeta _live_ -händelser med [händelsenropen](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) .

>[!NOTE]
>
>Begäran [om](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) händelser returnerar inte data till klienten efter en HTTP-svarskod.

I referensspelaren i din distribution finns ett sätt att bearbeta händelser innan du får ett sessions-ID. Exempel:

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**Bearbeta händelser som står i kö -** Referensspelaren bearbetar händelser som står i kö enligt följande:

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

Fortsätt bearbeta spårningshändelser när de inträffar.

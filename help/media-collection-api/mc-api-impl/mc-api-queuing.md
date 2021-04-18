---
title: Köa händelser när sessionens svar är långsamt
description: Köa händelser när sessionens svar är långsamt
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---

# Köa händelser när sessionsvar är långsamt{#queueing-events-when-sessions-response-is-slow}

Media Collection API är RESTful: Du gör alltså en HTTP-begäran och väntar på svaret. Detta är bara en viktig punkt när du begär [sessioner](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) för att få ett sessions-ID i början av videouppspelningen. Detta är viktigt eftersom sessions-ID krävs för alla efterföljande spårningsanrop.

Det är möjligt att spelaren kan utlösa händelser _innan sessionssvaret returnerar_ (med parametern för sessions-ID) från serverdelen. Om detta inträffar måste programmet placera eventuella spårningshändelser i kö som kommer mellan [sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) och dess svar. När sessionssvaret kommer, bör du först bearbeta alla [händelser](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) som står i kö och sedan starta bearbetningen av _live_-händelser med [händelserna](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)-anropen.

>[!NOTE]
>
>[Händelsebegäran](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) returnerar inte data till klienten efter en HTTP-svarskod.

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

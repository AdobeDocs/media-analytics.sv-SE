---
title: Köa händelser när sessioner svarar långsamt
description: Lär dig hur du gör när sessions-ID returneras efter att spelaren har aktiverat händelser.
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 4%

---

# Köa händelser när sessionens svar är långsamt{#queueing-events-when-sessions-response-is-slow}

Media Collection API är RESTful: Du gör alltså en HTTP-begäran och väntar på svaret. Detta är bara en viktig punkt när du skapar [Sessionsbegäran](../mc-api-ref/mc-api-sessions-req.md) om du vill hämta ett sessions-ID i början av videouppspelningen. Detta är viktigt eftersom sessions-ID krävs för alla efterföljande spårningsanrop.

Det är möjligt att din spelare kan utlösa händelser _innan sessionerna returneras_ (med parametern för sessions-ID) från serverdelen. Om detta inträffar måste programmet placera eventuella spårningshändelser i kö mellan [Sessionsbegäran](../mc-api-ref/mc-api-sessions-req.md) och dess svar. När sessionens svar kommer bör du först bearbeta alla som står i kö [händelser](../mc-api-ref/mc-api-events-req.md)kan du påbörja bearbetningen _live_ med [Händelser](../mc-api-ref/mc-api-events-req.md) samtal.

>[!NOTE]
>
>The [Händelsebegäran](../mc-api-ref/mc-api-events-req.md) returnerar inte data tillbaka till klienten efter en HTTP-svarskod.

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

**Bearbeta alla händelser som står i kö -** Referensspelaren bearbetar händelser i kö enligt följande:

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

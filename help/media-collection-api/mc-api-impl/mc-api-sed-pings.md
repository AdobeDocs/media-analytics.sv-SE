---
title: Skicka ping-händelser
description: null
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Skicka ping-händelser{#sending-ping-events}

**För huvudinnehåll måste du utlösa ping-händelser var 10:e sekund, med början efter 10 sekunder av uppspelningen, oavsett andra API-händelser som du har skickat. För annonsspårning måste du utlösa pinghändelser var 1:e sekund.**

ping-händelserna är bokstavligen&quot;hjärtslagen&quot; i Media Analytics. De enda obligatoriska parametrarna för ett ping-anrop är `eventType: ping` tillsammans med `playerTime` objektet (spelhuvudets position och tidsstämpel).

I följande kodutdrag visas ett sätt att implementera en tidsbestämd pingmekanism för huvudinnehållet (10 sekunder):

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```


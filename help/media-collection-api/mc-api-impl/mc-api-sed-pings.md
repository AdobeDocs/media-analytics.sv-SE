---
title: Skicka ping-händelser
description: Skicka ping-händelser
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Skicka ping-händelser{#sending-ping-events}

**För huvudinnehåll måste du utlösa ping-händelser var 10:e sekund, med början efter 10 sekunder av uppspelningen, oavsett andra API-händelser som du har skickat. För annonsspårning måste du utlösa ping-händelser var 1:e sekund.**

ping-händelserna är bokstavligen&quot;hjärtslagen&quot; i Media Analytics. De enda obligatoriska parametrarna för ett ping-anrop är `eventType: ping` tillsammans med `playerTime`-objektet (spelhuvudets position och tidsstämpel).

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

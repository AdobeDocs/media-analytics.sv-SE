---
title: Skicka pinghändelser
description: Ping-händelser är takten i Streaming Media Analytics. Lär dig hur du skickar en tidsbestämd ping för huvudinnehåll eller annonsspårning.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 2%

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

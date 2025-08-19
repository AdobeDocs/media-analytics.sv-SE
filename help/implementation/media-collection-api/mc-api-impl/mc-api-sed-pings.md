---
title: Skicka Ping-händelser
description: Ping-händelser är den bästa takten i Adobe direktuppspelande medietjänster. Lär dig hur du skickar en tidsbestämd ping för huvudinnehåll eller annonsspårning.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Skicka ping-händelser{#sending-ping-events}

**Du måste utlösa ping-händelser var 10:e sekund, med början efter 10 sekunder av uppspelningen, oavsett andra API-händelser som du har skickat. Detta gäller både huvudinnehåll och annonsspårning.**

ping-händelserna är&quot;hjärtslagen&quot; i Adobe direktuppspelande medietjänster. De enda obligatoriska parametrarna för ett ping-anrop är `eventType: ping` tillsammans med objektet `playerTime` (spelhuvudets position och tidsstämpel).

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

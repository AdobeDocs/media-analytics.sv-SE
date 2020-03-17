---
title: Översikt
description: En översikt över upplevelsespårningskvalitet (QoE, QoS) med Media SDK.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Översikt{#overview}

>[!IMPORTANT]
>
>Följande anvisningar ger vägledning för implementering i alla 2.x SDK:er. Om du implementerar en 1.x-version av SDK kan du hämta 1.x-utvecklarhandboken här: [Hämta SDK:er.](/help/sdk-implement/download-sdks.md)

Kvaliteten på upplevelsespårningen innefattar QoS (Quality of Service) och felspårning, båda är valfria element och behövs **inte** för implementering av huvudmediespårning. Du kan använda mediespelarens API för att identifiera variabler som är relaterade till QoS och felspårning. Här är de viktigaste elementen för att hålla koll på upplevelsekvaliteten:

## Spelarhändelser {#player-events}

### Om QoS-mätvärden ändras:

Skapa eller uppdatera QoS-objektinstansen för uppspelningen. [QoS API-referens](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Alla bithastighetsändringshändelser

Utlysning `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementera QOS

1. Identifiera när någon av mätvärdena för QOS ändras under medieuppspelning, skapa materialet `MediaObject` med QoS-informationen och uppdatera den nya QoS-informationen.

   QoSObject-variabler:

   >[!TIP]
   >
   >Dessa variabler är bara obligatoriska om du tänker spåra QoS.

   | Variabel | Beskrivning | Obligatoriskt |
   | --- | --- | :---: |
   | `bitrate` | Aktuell bithastighet | Ja |
   | `startupTime` | Starttid | Ja |
   | `fps` | FPS-värde | Ja |
   | `droppedFrames` | Antal uteslutna bildrutor | Ja |

1. Se till att den `getQoSObject()` metoden returnerar den senaste QoS-informationen.
1. När uppspelningen växlar bithastigheter anropar du `BitrateChange` händelsen i Media Heartbeat-instansen.

   >[!IMPORTANT]
   >
   >Uppdatera QoS-objektet och anropa bithastighetsändringshändelsen för varje bithastighetsändring. Detta ger de mest exakta QoS-data.

I följande exempelkod används JavaScript 2.x SDK för en HTML5-mediespelare. Du bör använda den här koden med den viktigaste mediespelningskoden.

```js
var mediaDelegate = new MediaHeartbeatDelegate(); 
...  
 
// This is called periodically by MediaHeartbeat instance 
mediaDelegate.prototype.getQoSObject = function() { 
    return this.qosInfo; 
}; 
 
if (e.type == "qos_update") { 
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>); 
    mediaDelegate.qosInfo = qosInfo; 
}; 
 
if (e.type == "bitrate_change") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
};
```


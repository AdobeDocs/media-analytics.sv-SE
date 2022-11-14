---
title: Ställa in Media SDK med JavaScript 2.x
description: Följ de här stegen för att konfigurera Media SDK-programmet på JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 3%

---

# Konfigurera JavaScript 2.x{#set-up-javascript}

## Förutsättningar

* **Hämta giltiga konfigurationsparametrar**
Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.
* **Implementera `AppMeasurement` för JavaScript i ditt medieprogram**
Mer information om Adobe Mobile SDK-dokumentationen finns i [Implementera Analytics med JavaScript.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html)

* **Tillhandahåll följande funktioner i din mediespelare:**

   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som tillhandahåller spelarinformation* - Den här informationen innehåller information som medienamnet och spelhuvudets position.

1. Lägg till [nedladdad](/help/getting-started/download-sdks.md) till ditt projekt. Skapa lokala referenser till klasserna.

   1. Expandera `MediaSDK-js-v2.*.zip` som du har laddat ned.
   1. Verifiera att `MediaSDK.min.js` filen finns i `libs` katalog:

   1. Värd för `MediaSDK.min.js` -fil.

      Denna JavaScript-huvudfil måste finnas på en webbserver som är tillgänglig för alla sidor på din plats. Du behöver sökvägen till de här filerna för nästa steg.

   1. Referens `MediaSDK.min.js` på alla webbplatssidor.

      Inkludera `MediaSDK` för JavaScript genom att lägga till följande kodrad i `<head>` eller `<body>` på varje sida. Exempel:

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Du kan snabbt verifiera att biblioteket har importerats genom att instansiera `ADB.va.MediaHeartbeatConfig` klassen.

      >[!NOTE]
      >
      >Från version 2.1.0 är JavaScript SDK kompatibelt med AMD- och CommonJS-modulspecifikationerna, och `VideoHeartbeat.min.js` kan även användas med kompatibla modulinläsare.

1. Skapa lokala referenser till `MediaHeartbeat` klasser.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Skapa en `MediaHeartbeatConfig` -instans.

   Det här avsnittet hjälper dig att förstå `MediaHeartbeat` konfigurationsparametrar och hur du ställer in korrekta konfigureringsvärden på dina `MediaHeartbeat` för korrekt spårning.

   Här följer ett exempel på `MediaHeartbeatConfig`-initiering:

   ```js
   //Media Heartbeat initialization
   var mediaConfig = new MediaHeartbeatConfig();
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
   mediaConfig.playerName = Configuration.PLAYER.NAME;
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL;
   mediaConfig.debugLogging = true;
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK;
   mediaConfig.ssl = false;
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP;
   ```

1. Implementera `MediaHeartbeatDelegate` -protokoll.

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate();
   
   // Replace <currentPlaybackTime> with the video player current playback time
   mediaDelegate.getCurrentPlaybackTime = function() {
       return <currentPlaybackTime>;
   };
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() {
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
   };
   ```

1. Skapa `MediaHeartbeat` -instans.

   Använd `MediaHeartbeatConfig` och `MediaHeartbeatDelegate` för att skapa `MediaHeartbeat` -instans.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Se till att `MediaHeartbeat` -instansen är tillgänglig och tas inte bort förrän mediesessionen är slut. Den här instansen används för alla följande spårningshändelser.

   >[!TIP]
   >
   >`MediaHeartbeat` kräver en instans av `AppMeasurement` för att ringa Adobe Analytics. Här är ett exempel på en `AppMeasurement` instans:

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## Migrera från JavaScript 1.x till 2.x

I version 2.x konsolideras alla publika metoder i `ADB.va.MediaHeartbeat` för utvecklare. Dessutom konsolideras nu alla konfigurationer i `ADB.va.MediaHeartbeatConfig` klassen.

Mer information om hur du migrerar från 1.x till 2.x finns i dokumentationen för den äldre implementeringen.

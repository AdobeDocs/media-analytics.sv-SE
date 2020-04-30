---
title: Konfigurera JavaScript
description: Installation av Media SDK-program för implementering i JavaScript.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Konfigurera JavaScript{#set-up-javascript}

## Förutsättningar

* **Hämta giltiga konfigurationsparametrar** Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.
* **Implementera`AppMeasurement`för JavaScript i ditt medieprogram** Mer information om dokumentationen för Adobe Mobile SDK finns i [Implementera analys med JavaScript.](https://docs.adobe.com/content/help/en/analytics/implementation/js/overview.html)

* **Tillhandahåll följande funktioner i din mediespelare:**

   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som tillhandahåller spelarinformation* - Den här informationen innehåller information som medienamnet och spelhuvudets position.

1. Lägg till ditt [hämtade](/help/sdk-implement/download-sdks.md#download-2x-sdks) bibliotek i projektet. Skapa lokala referenser till klasserna.

   1. Expandera den `MediaSDK-js-v2.*.zip` fil du hämtade.
   1. Kontrollera att `MediaSDK.min.js` filen finns i `libs` katalogen:

   1. Lägg `MediaSDK.min.js` filen som värd.

      Denna JavaScript-huvudfil måste finnas på en webbserver som är tillgänglig för alla sidor på din plats. Du behöver sökvägen till de här filerna för nästa steg.

   1. Referens `MediaSDK.min.js` på alla webbplatssidor.

      Inkludera `MediaSDK` för JavaScript genom att lägga till följande kodrad i `<head>` - eller `<body>` -taggen på varje sida. Exempel:

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Du kan snabbt verifiera att biblioteket har importerats genom att instansiera `ADB.va.MediaHeartbeatConfig` klassen.

      >[!NOTE]
      >
      >Från version 2.1.0 är JavaScript SDK kompatibelt med AMD- och CommonJS-modulspecifikationerna, och `VideoHeartbeat.min.js` kan även användas med kompatibla modulinläsare.

1. Skapa lokala referenser till `MediaHeartbeat` klasserna för enkel åtkomst till API:erna.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Skapa en `MediaHeartbeatConfig` instans.

   I det här avsnittet får du hjälp med att förstå `MediaHeartbeat` konfigurationsparametrar och hur du ställer in rätt konfigureringsvärden för `MediaHeartbeat` instansen för korrekt spårning.

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

1. Implementera `MediaHeartbeatDelegate` protokollet.

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

1. Skapa `MediaHeartbeat` instansen.

   Använd `MediaHeartbeatConfig` och `MediaHeartbeatDelegate` för att skapa `MediaHeartbeat` instansen.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Kontrollera att din `MediaHeartbeat` instans är tillgänglig och inte tas bort förrän mediesessionen är slut. Den här instansen används för alla följande spårningshändelser.

   >[!TIP]
   >
   >`MediaHeartbeat` kräver en instans av `AppMeasurement` för att skicka anrop till Adobe Analytics. Här är ett exempel på en `AppMeasurement` instans:

   ```js
   var appMeasurement = new AppMeasurement(); 
   appMeasurement.visitor = visitor; 
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
   appMeasurement.account = <rsid>; 
   appMeasurement.pageName = <page_name>; 
   appMeasurement.charSet = "UTF­8";
   ```

## Migrera från version 1.x till 2.x i JavaScript

I version 2.x konsolideras alla publika metoder i `ADB.va.MediaHeartbeat` klassen så att det blir enklare för utvecklare. Dessutom konsolideras nu alla konfigurationer i `ADB.va.MediaHeartbeatConfig` klassen.

Mer information om hur du migrerar från 1.x till 2.x finns i [VHL 1.x till 2.x-migrering.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

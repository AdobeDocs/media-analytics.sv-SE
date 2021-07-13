---
title: Ställa in media-SKD med JavaScript 2.x
description: Följ de här stegen för att konfigurera Media SDK-programmet på JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# Konfigurera JavaScript 2.x{#set-up-javascript}

## Förutsättningar

* **Hämta giltiga**
konfigurationsparametrarDessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat analyskontot.
* **Implementera  `AppMeasurement` för JavaScript i**
medieprogrammetMer information om Adobe Mobile SDK-dokumentationen finns i  [Implementera analys med JavaScript.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html)

* **Tillhandahåll följande funktioner i din mediespelare:**

   * *Ett API för att prenumerera på spelarhändelser*  - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som tillhandahåller spelarinformation*  - Den här informationen innehåller information som medienamnet och spelhuvudets position.

1. Lägg till ditt [hämtade](/help/sdk-implement/download-sdks.md#download-2x-sdks)-bibliotek i ditt projekt. Skapa lokala referenser till klasserna.

   1. Expandera `MediaSDK-js-v2.*.zip`-filen som du hämtade.
   1. Kontrollera att filen `MediaSDK.min.js` finns i katalogen `libs`:

   1. Lägg `MediaSDK.min.js`-filen som värd.

      Denna JavaScript-huvudfil måste finnas på en webbserver som är tillgänglig för alla sidor på din plats. Du behöver sökvägen till de här filerna för nästa steg.

   1. Referens `MediaSDK.min.js` för alla webbplatssidor.

      Inkludera `MediaSDK` för JavaScript genom att lägga till följande kodrad i taggen `<head>` eller `<body>` på varje sida. Exempel:

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Du kan snabbt verifiera att biblioteket har importerats genom att instansiera klassen `ADB.va.MediaHeartbeatConfig`.

      >[!NOTE]
      >
      >Från version 2.1.0 är JavaScript SDK kompatibelt med AMD- och CommonJS-modulspecifikationerna, och `VideoHeartbeat.min.js` kan även användas med kompatibla modulinläsare.

1. Skapa lokala referenser till klasserna `MediaHeartbeat` för enkel åtkomst till API:erna.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Skapa en `MediaHeartbeatConfig`-instans.

   I det här avsnittet får du hjälp med att förstå `MediaHeartbeat`-konfigurationsparametrar och hur du ställer in korrekta konfigurationsvärden för din `MediaHeartbeat`-instans för korrekt spårning.

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

1. Implementera `MediaHeartbeatDelegate`-protokollet.

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

1. Skapa `MediaHeartbeat`-instansen.

   Använd `MediaHeartbeatConfig` och `MediaHeartbeatDelegate` för att skapa `MediaHeartbeat`-instansen.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Se till att din `MediaHeartbeat`-instans är tillgänglig och inte tas bort förrän i slutet av mediesessionen. Den här instansen används för alla följande spårningshändelser.

   >[!TIP]
   >
   >`MediaHeartbeat` kräver en instans av  `AppMeasurement` för att skicka anrop till Adobe Analytics. Här är ett exempel på en `AppMeasurement`-instans:

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## Migrera från JavaScript 1.x till 2.x

I version 2.x konsolideras alla publika metoder i klassen `ADB.va.MediaHeartbeat` så att det blir enklare för utvecklare. Dessutom konsolideras nu alla konfigurationer i klassen `ADB.va.MediaHeartbeatConfig`.

Mer information om hur du migrerar från 1.x till 2.x finns i [VHL 1.x till 2.x-migrering.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

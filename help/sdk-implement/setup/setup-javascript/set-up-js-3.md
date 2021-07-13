---
title: Ställa in media-SKD med JavaScript 3.x
description: Följ de här stegen för att konfigurera Media SDK-programmet på JavaScript 3.x.
exl-id: 35e27495-e480-4463-9f00-4b60a54d02c1
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 2%

---

# Konfigurera JavaScript 3.x{#set-up-javascript}

## Förutsättningar

* **Hämta giltiga**
konfigurationsparametrarDessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat analyskontot.
* **Implementera  `AppMeasurement` och  `Experience Cloud Identity Service` för JavaScript i ditt**
medieprogramMer information finns i  [Implementera Analytics med ](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) JavaScript och  [Implementera identitetstjänsten](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html) för Experience Cloud.

* **Tillhandahåll följande funktioner i din mediespelare:**

   * *Ett API för att prenumerera på spelarhändelser*  - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som innehåller spelarinformation*  - Detta innehåller information om aktuella uppspelningsmedier, annonser och kapitel.

1. Lägg till ditt [hämtade](/help/sdk-implement/download-sdks.md#download-3x-sdks)-bibliotek i ditt projekt. Skapa lokala referenser till klasserna.

   1. Expandera `MediaSDK-js-v3*.zip`-filen som du hämtade.
   1. Kontrollera att filen `MediaSDK.js` finns i katalogen `libs`.

   1. Lägg `MediaSDK.js`-filen som värd.

      Denna JavaScript-huvudfil måste finnas på en webbserver som är tillgänglig för alla sidor på din plats. Du behöver sökvägen till de här filerna för nästa steg.

   1. Referens `MediaSDK.js` för alla webbplatssidor.

      Inkludera `MediaSDK` för JavaScript genom att lägga till följande kodrad i taggen `<head>` eller `<body>` på varje sida. Exempel:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Om du snabbt vill verifiera att biblioteket har importerats, kontrollerar du att `ADB.Media` har exporterats till Window-objektet.

      >[!NOTE]
      >
      >JavaScript SDK är kompatibelt med AMD- och CommonJS-modulspecifikationerna, och `MediaSDK.js` kan även användas med kompatibla modulinläsare.

1. Skapa en instans av `AppMeasurement` och konfigurera `visitor`.

   Konfigurationen av Media SDK kräver en instans av `AppMeasurement` med `visitor` konfigurerad.

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. Konfigurera Media SDK

   Media SDK bör konfigureras en gång per webbsida och konfigurationen gäller för alla spårningsinstanser som skapas.

   >[!IMPORTANT]
   >
   > Media SDK (3.x) använder Media Collection API för att spåra media som skiljer sig från HB-slutpunkten som används i 2.x SDK:er. Kontakta din Adobe-representant om du vill ha mer information.

   Här följer ett exempel på `MediaConfig`-initiering:

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   ```

1. Skapa `MediaTracker`-instansen.

   När Media SDK har konfigurerats kan spårningsinstanser för att spåra medieinnehåll skapas med hjälp av API:t `getInstance`.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Se till att din `tracker`-instans är tillgänglig och inte tas bort förrän i slutet av mediesessionen. Den här instansen används för att spåra alla följande händelser för den sessionen.

## Migrera från JavaScript 2.x till 3.x

Mer information om migrering från 2.x till 3.x finns i [2.x till 3.x-migrering.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)

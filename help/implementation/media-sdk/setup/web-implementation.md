---
title: Konfigurera en webbimplementering för Analytics for Streaming Media
description: Lär dig hur du implementerar Adobe Streaming Media för webbprogram.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---


# Installera webb-SDK:er {#install-web-sdks}

Konfigurera Media SDK v3.x för JavaScript >> vad Calis vill ha på nedladdningssidan/länken

Det här avsnittet innehåller information om hur du installerar web SDK och konfigurerar JavaScript.


## Förutsättningar {#prerequesites}

* **Hämta giltiga konfigurationsparametrar**

   Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.

* **Implementera `AppMeasurement` och `Experience Cloud Identity Service` för JavaScript i ditt medieprogram**

   Mer information finns i [Implementera analys med JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) och [Implementera Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html).

* **Inkludera följande API:er i mediespelaren**

   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som tillhandahåller spelarinformation* - Detta innehåller information om hur du spelar upp media, annonser och kapitel.

## Konfigurera JavaScript 3.x {#set-up-javascript}

1. Lägg till [nedladdad](/help/getting-started/download-sdks.md) till ditt projekt. Skapa lokala referenser till klasserna.

   1. Expandera `MediaSDK-js-v3*.zip` som du har laddat ned.
   1. Verifiera att `MediaSDK.js` filen finns i `libs` katalog.

   1. Värd för `MediaSDK.js` -fil.

      Denna JavaScript-huvudfil måste finnas på en webbserver som är tillgänglig för alla sidor på din plats. Du behöver sökvägen till de här filerna för nästa steg.

   1. Referens `MediaSDK.js` på alla webbplatssidor.

      Inkludera `MediaSDK` för JavaScript genom att lägga till följande kodrad i `<head>` eller `<body>` på varje sida. Exempel:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Kontrollera att biblioteket har importerats `ADB.Media` exporteras på Window-objekt.

      >[!NOTE]
      >
      >JavaScript SDK är kompatibelt med AMD- och CommonJS-modulspecifikationerna, och `MediaSDK.js` kan även användas med kompatibla modulinläsare.

1. Skapa en instans av `AppMeasurement` och konfigurera `visitor`.

   Konfiguration av Media SDK kräver en instans av `AppMeasurement` med `visitor` konfigurerad.

   ```js
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
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

1. Skapa `MediaTracker` -instans.

   När Media SDK har konfigurerats kan spårningsinstanser för att spåra medieinnehåll skapas med `getInstance` API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Se till att `tracker` -instansen är tillgänglig och tas inte bort förrän mediesessionen är slut. Den här instansen används för att spåra alla följande händelser för den sessionen.

## Migrera från JavaScript 2.x till 3.x

Mer information om hur du migrerar från 2.x till 3.x finns i [2.x till 3.x-migrering.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)

Mer information om äldre innehåll finns i [Äldre implementeringar](/help/legacy/media-sdk/setup/setup-overview.md)

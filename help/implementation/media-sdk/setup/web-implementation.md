---
title: Konfigurera en webbimplementering för Analytics for Streaming Media
description: Lär dig hur du implementerar Adobe Streaming Media för webbprogram.
feature: Streaming Media
role: User, Admin, Developer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 1%

---

# Installera media SDK med JavaScript {#install-web-sdks}

Informationen på den här sidan beskriver hur du installerar den fristående webbversionen av SDK och konfigurerar JavaScript.

Du kan också använda Adobe Media Analytics-tillägget för att implementera direktuppspelande medietjänster, vilket beskrivs i [Installera direktuppspelande medietjänster med Media Analytics-tillägget](/help/implementation/media-sdk/setup/web-implementation-tags.md).

## Förutsättningar {#prerequesites}

* **Hämta giltiga konfigurationsparametrar**

  Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.

* **Implementera `AppMeasurement` och `Experience Cloud Identity Service` för JavaScript i ditt medieprogram**

  Mer information finns i [Implementera analys med JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=sv-SE) och [Implementera Experience Cloud identitetstjänst](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=sv-SE).

* **Ta med följande API:er i mediespelaren**

   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som innehåller spelarinformation* - Detta innehåller information om media, annonser och kapitel som spelas upp just nu.

## Konfigurera JavaScript 3.x {#set-up-javascript}

1. Lägg till ditt [hämtade](/help/getting-started/download-sdks.md)-bibliotek i ditt projekt. Skapa lokala referenser till klasserna.

   1. Expandera filen `MediaSDK-js-v3*.zip` som du hämtade.
   1. Kontrollera att filen `MediaSDK.js` finns i katalogen `libs`.

   1. Värd för filen `MediaSDK.js`.

      Den här JavaScript-huvudfilen måste finnas på en webbserver som är tillgänglig för alla sidor på webbplatsen. Du behöver sökvägen till de här filerna för nästa steg.

   1. Referens `MediaSDK.js` på alla webbplatssidor.

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
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   ```

1. Konfigurera Media SDK

   Media SDK bör konfigureras en gång per webbsida och konfigurationen gäller för alla spårningsinstanser som skapas.

   >[!IMPORTANT]
   >
   > Media SDK (3.x) använder Media Collection API för att spåra media som skiljer sig från HB-slutpunkten som används i 2.x SDK:er. Kontakta Adobe om du vill ha mer information.

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

1. Skapa instansen `MediaTracker`.

   När du har konfigurerat Media SDK kan du skapa spårningsinstanser för att spåra medieinnehåll med hjälp av `getInstance` API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Se till att din `tracker`-instans är tillgänglig och inte tas bort förrän mediesessionen är slut. Den här instansen används för att spåra alla följande händelser för den sessionen.

## Migrera från JavaScript 2.x till 3.x

Mer information om migrering från 2.x till 3.x finns i [2.x till 3.x-migrering.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)

Mer information om äldre innehåll finns i [Äldre implementeringar](/help/legacy/media-sdk/setup/setup-overview.md)

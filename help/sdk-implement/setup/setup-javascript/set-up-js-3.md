---
title: Konfigurera JavaScript 3.x
description: Installation av Media SDK-program för implementering i JavaScript 3.x.
translation-type: tm+mt
source-git-commit: a73536bd7a818ac23ad322a15f109644e75ee0d5
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 2%

---


# Konfigurera JavaScript 3.x{#set-up-javascript}

## Förutsättningar

* **Hämta giltiga konfigurationsparametrar** Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.
* **Implementera`AppMeasurement`och`Experience Cloud Identity Service`för JavaScript i ditt medieprogram** Mer information finns i [Implementera analys med JavaScript](https://docs.adobe.com/content/help/en/analytics/implementation/js/overview.html) och [Implementera Experience Cloud Identity Service.](https://docs.adobe.com/content/help/en/id-service/using/implementation/setup-analytics.html)

* **Tillhandahåll följande funktioner i din mediespelare:**

   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som innehåller spelarinformation* - Detta innehåller information om aktuella uppspelningsmedier, annonser och kapitel.

1. Lägg till ditt [hämtade](/help/sdk-implement/download-sdks.md#download-3x-sdks) bibliotek i projektet. Skapa lokala referenser till klasserna.

   1. Expandera den `MediaSDK-js-v3*.zip` fil du hämtade.
   1. Kontrollera att `MediaSDK.js` filen finns i `libs` katalogen.

   1. Lägg `MediaSDK.js` filen som värd.

      Denna JavaScript-huvudfil måste finnas på en webbserver som är tillgänglig för alla sidor på din plats. Du behöver sökvägen till de här filerna för nästa steg.

   1. Referens `MediaSDK.js` på alla webbplatssidor.

      Inkludera `MediaSDK` för JavaScript genom att lägga till följande kodrad i `<head>` - eller `<body>` -taggen på varje sida. Exempel:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Om du snabbt vill verifiera att biblioteket har importerats, `ADB.Media` exporteras kontrollen på Window-objektet.

      >[!NOTE]
      >
      >JavaScript SDK är kompatibelt med AMD- och CommonJS-modulspecifikationerna, och `MediaSDK.js` kan även användas med kompatibla modulinläsare.

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
   
1. Skapa `MediaTracker` instansen.

   När Media SDK har konfigurerats kan spårningsinstanser för att spåra medieinnehåll skapas med `getInstance` API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Kontrollera att din `tracker` instans är tillgänglig och inte tas bort förrän mediesessionen är slut. Den här instansen används för att spåra alla följande händelser för den sessionen.

## Migrera från JavaScript 2.x till 3.x

Mer information om hur du migrerar från 2.x till 3.x finns i Migrering från [2.x till 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)

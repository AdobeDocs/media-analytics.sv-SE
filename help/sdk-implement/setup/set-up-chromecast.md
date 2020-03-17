---
title: Konfigurera kromecast
description: Installation av Media SDK-program för implementering på Chromecast.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Konfigurera kromecast{#set-up-chromecast}

## Vanliga frågor

_Bör jag använda JavaScript SDK i Chromecast eller kan jag använda JavaScript SDK som standard?_

Det korrekta svaret är &quot;Chromecast&quot; av följande skäl:
* AppMeasurement- och VisitorAPI-biblioteken i standard-JS SDK är inte certifierade för att fungera på OTT-plattformar. I Chromecast JS SDK är Video Heartbeats Library (VHL), Analytics och VisitorAPI inbyggda i en enda, enhetlig, certifierad för Chromecast SDK.
* Chromecast SDK är mycket lättare än standard-JS SDK. Detta är mycket viktigt för den maskinvara med lägre prestanda som används av OTT-plattformar.

## Förutsättningar

* **Hämta giltiga konfigurationsparametrar för Heartbeats** Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt medieanalyskonto.
* **Tillhandahåll följande funktioner i din mediespelare:**
   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som tillhandahåller spelarinformation* - Den här informationen innehåller information som medienamnet och spelhuvudets position.

Adobes mobiltjänster har ett nytt användargränssnitt som samlar funktioner för mobilmarknadsföring för mobilappar från hela Adobe Marketing Cloud. Från början erbjuder mobiltjänsten smidig integrering av funktioner för appanalys och målinriktning för Adobe Analytics- och Adobe Target-lösningarna. Läs mer i dokumentationen för [Adobe Mobile Services.](https://marketing.adobe.com/resources/help/en_US/mobile/)

Med Chromecast SDK 2.x for Experience Cloud Solutions kan ni mäta Chromecast-applikationer som skrivits i JavaScript, utnyttja och samla in målgruppsdata via målgruppshantering och mäta videoengagemang med videohjärtslag.

## SDK-implementering

1. Lägg till ditt [hämtade](/help/sdk-implement/download-sdks.md#download-2x-sdks) Chromecast-bibliotek i ditt projekt.

   1. ZIP- `AdobeMobileLibrary-Chromecast-[version]` filen består av följande programvarukomponenter:

      * `adbmobile-chromecast.min.js`:

         Den här biblioteksfilen inkluderas i din Chromecast-appkällmapp.

      * `ADBMobileConfig` config

         Den här SDK-konfigurationsfilen är anpassad för ditt program. Ett exempel på `ADBMobileConfig` implementering ingår i SDK (under `samples/`). Hämta rätt inställningar från en Adobe-representant.
   1. Lägg till biblioteksfilen i din `index.html` fil och skapa den `ADBMobileConfig` globala variabeln enligt följande (den globala variabeln som används för att konfigurera Adobe Mobile för Heartbeats har en exklusiv nyckel med namnet `mediaHeartbeat`):

      ```js
      <script> 
          var ADBMobileConfig = { 
            "marketingCloud": { 
              "org": "972C898555E9F7BC7F000101@AdobeOrg" 
            }, 
            "target": { 
              "clientCode": "", 
              "timeout": 5 
            }, 
            "audienceManager": { 
              "server": "obumobile5.demdex.net" 
            }, 
            "analytics": { 
              "rsids": "mobile5vhl.sample.player", 
              "server": "obumobile5.sc.omtrdc.net", 
              "ssl": false, 
              "offlineEnabled": false, 
              "charset": "UTF-8", 
              "lifecycleTimeout": 300, 
              "privacyDefault": "optedin", 
              "batchLimit": 0, 
              "timezone": "MDT", 
              "timezoneOffset": -360, 
              "referrerTimeout": 0, 
              "poi": [] 
            }, 
            "mediaHeartbeat": { 
              "server": "obumobile5.hb.omtrdc.net", 
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg", 
              "channel": "test-channel-chromecast", 
              "ssl": false, 
              "ovp": "chromecast-player", 
              "sdkVersion": "chromecast-sdk", 
              "playerName": "Chromecast" 
            } 
          }; 
        </script> 
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >Om `mediaHeartbeat` inte är korrekt konfigurerad försätts mediemodulen i ett feltillstånd och skickar inga spårningsanrop.

      ADBMoble Config-parametrar för nyckeln mediaHeartbeat:
   | Konfigurationsparameter | Beskrivning |
   | --- | --- |
   | `server` | Sträng som representerar URL:en för spårningsslutpunkten på backend-objektet. |
   | `publisher` | En sträng som representerar den unika identifieraren för innehållsutgivaren. |
   | `channel` | En sträng som representerar namnet på innehållsdistributionskanalen. |
   | `ssl` | Boolean som representerar om SSL ska användas för att spåra anrop. |
   | `ovp` | Sträng som representerar namnet på videospelarleverantören. |
   | `sdkversion` | Sträng som representerar den aktuella versionen av programmet/SDK. |
   | `playerName` | En sträng som representerar spelarens namn. |


1. Konfigurera Experience Cloud Visitor-ID.

   Experience Cloud Visitor ID-tjänsten tillhandahåller ett universellt Visitor-ID för alla Experience Cloud-lösningar. Tjänsten för besökar-ID krävs av pulsslag för video och andra Marketing Cloud-integreringar.

   Kontrollera att din `ADBMobileConfig` konfiguration innehåller ditt `marketingCloud` organisations-ID.

   ```js
   "marketingCloud": { 
       "org": YOUR-MCORG-ID" 
   }
   ```

   Organisations-ID för Experience Cloud identifierar unikt varje klientföretag i Adobe Marketing Cloud och ser ut ungefär som följande värde: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Se till att du inkluderar `@AdobeOrg`.

   När konfigurationen är klar skapas ett Experience Cloud Visitor-ID som ingår i alla träffar. Andra besökar-ID:n, till exempel `custom` och `automatically-generated`, fortsätter att skickas med varje träff.

   **Tjänstmetoder för Experience Cloud Visitor ID**

   >[!TIP]
   >
   >Experience Cloud Visitor ID-metoder har prefixet `visitor`.

   | Metod | Beskrivning |
   | --- | --- |
   | `getMarketingCloudID()` | Hämtar Experience Cloud-besökar-ID:t från besökar-ID-tjänsten.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Med Experience Cloud Visitor ID kan ni ange ytterligare kund-ID:n som kan kopplas till varje besökare. Besökar-API:t godkänner flera kund-ID:n för samma besökare och en kundtypsidentifierare för att skilja omfattningen för olika kund-ID:n åt. Den här metoden motsvarar den `setCustomerIDs()` i JavaScript-biblioteket.  Exempel: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |


<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->


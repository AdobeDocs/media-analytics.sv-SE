---
title: Konfigurera Roku
description: Installation av Media SDK-program för implementering på Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Konfigurera Roku{#set-up-roku}

## Förutsättningar

* **Hämta giltiga konfigurationsparametrar för Heartbeats** Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt medieanalyskonto.
* **Tillhandahåll följande funktioner i din mediespelare:**
   * _Ett API för att prenumerera på spelarhändelser_ - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * _Ett API som tillhandahåller spelarinformation_ - Den här informationen innehåller information som medienamnet och spelhuvudets position.

Adobes mobiltjänster har ett nytt användargränssnitt som samlar funktioner för mobilmarknadsföring för mobilappar från hela Adobe Marketing Cloud. Från början erbjuder mobiltjänsten smidig integrering av funktioner för appanalys och målinriktning för Adobe Analytics- och Adobe Target-lösningarna.

Läs mer i dokumentationen för [Adobe Mobile Services.](https://docs.adobe.com/content/help/en/mobile-services/using/home.html)

Med Roku SDK 2.x för Experience Cloud Solutions kan ni mäta Roku-applikationer som skrivits i BrightScript, utnyttja och samla in målgruppsdata via målgruppshantering och mäta videoengagemang med videohjärtslag.

## SDK-implementering

1. Lägg till ditt [hämtade](/help/sdk-implement/download-sdks.md#download-2x-sdks) Roku-bibliotek i ditt projekt.

   1. Den `AdobeMobileLibrary-2.*-Roku.zip` hämtade filen består av följande programvarukomponenter:

      * `adbmobile.brs`: Den här biblioteksfilen inkluderas i Roku-appens källmapp.

      * `ADBMobileConfig.json`: Den här SDK-konfigurationsfilen är anpassad för ditt program.
   1. Lägg till biblioteksfilen och JSON-konfigurationsfilen i projektkällan.

      Den JSON som används för att konfigurera Adobe Mobile har en exklusiv nyckel för mediefärger som kallas `mediaHeartbeat`. Här tillhör konfigurationsparametrarna för mediets pulsslag.

      >[!TIP]
      >
      >Paketet innehåller ett exempel på en `ADBMobileConfig` JSON-fil. Kontakta Adobe för att få veta vilka inställningar du har.

      Exempel:

      ```
      {
        "version":"1.0", 
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8", 
          "ssl":false, 
          "offlineEnabled":false, 
          "lifecycleTimeout":30, 
          "batchLimit":50, 
          "privacyDefault":"optedin", 
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{ 
        "clientCode":"", 
        "timeout":5
      },
      "audienceManager":{ 
        "server":""
      },
      "acquisition":{ 
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{ 
         "server":"example.com", 
         "publisher":"sample-publisher", 
         "channel":"sample-channel", 
         "ssl":false,
         "ovp":"sample-ovp", 
         "sdkVersion":"sample-sdk", 
         "playerName":"roku"
         }    
      }
      ```

      | Konfigurationsparameter | Beskrivning     |
      | --- | --- |
      | `server` | Sträng som representerar URL:en för spårningsslutpunkten på backend-objektet. |
      | `publisher` | En sträng som representerar den unika identifieraren för innehållsutgivaren. |
      | `channel` | En sträng som representerar namnet på innehållsdistributionskanalen. |
      | `ssl` | Boolean som representerar om SSL ska användas för att spåra anrop. |
      | `ovp` | Sträng som representerar namnet på videospelarleverantören. |
      | `sdkversion` | Sträng som representerar den aktuella versionen av programmet/SDK. |
      | `playerName` | En sträng som representerar spelarens namn. |

      >[!IMPORTANT]
      >
      >Om `mediaHeartbeat` inte är korrekt konfigurerad försätts mediemodulen i ett feltillstånd och skickar inga spårningsanrop.


1. Konfigurera Experience Cloud Visitor-ID.

   Experience Cloud Visitor ID-tjänsten tillhandahåller ett universellt Visitor-ID för alla Experience Cloud-lösningar. Tjänsten för besökar-ID krävs av pulsslag för video och andra Marketing Cloud-integreringar.

   Kontrollera att din `ADBMobileConfig` konfiguration innehåller ditt `marketingCloud` organisations-ID.

   ```
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

   |  Metod   | Beskrivning |
   | --- | --- |
   | `visitorMarketingCloudID` | Hämtar besökar-ID:t för Experience Cloud från besökar-ID-tjänsten.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Med Experience Cloud Visitor ID kan ni ange ytterligare kund-ID:n som kan kopplas till varje besökare. Besökar-API:t godkänner flera kund-ID:n för samma besökare och en kundtypsidentifierare för att skilja omfattningen för olika kund-ID:n åt. Den här metoden motsvarar `setCustomerIDs`. Exempel: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Används för att ange Roku-ID för annonsering (RIDA) på SDK. Exempel: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Hämta Roku ID för Advertising (RIDA) med hjälp av API:t [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) för Roku SDK. |

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://docs.adobe.com/content/help/en/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->

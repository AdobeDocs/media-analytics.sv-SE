---
title: Så här konfigurerar du Media SDK för Roku
description: Följ de här stegen för att konfigurera Media SDK-programmet på Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 2%

---

# Konfigurera Roku{#set-up-roku}

## Förutsättningar

* **Hämta giltiga konfigurationsparametrar för Heartbeats**
Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt medieanalyskonto.
* **Tillhandahåll följande funktioner i din mediespelare:**
   * _Ett API för att prenumerera på spelarhändelser_ - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * _Ett API som tillhandahåller spelarinformation_ - Den här informationen innehåller information som medienamnet och spelhuvudets position.

Adobe Mobile-tjänster har ett nytt användargränssnitt som samlar funktioner för mobilmarknadsföring för mobilappar från hela Adobe Marketing Cloud. Från början erbjuder mobiltjänsten smidig integrering av funktioner för appanalys och målinriktning för Adobe Analytics- och Adobe Target-lösningarna.

Läs mer på [Adobe Mobile Services-dokumentation.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html)

Med Roku SDK 2.x för Experience Cloud Solutions kan du mäta Roku-applikationer som skrivits i BrightScript, utnyttja och samla in målgruppsdata med hjälp av målgruppshantering och mäta videoengagemang med hjälp av videohjärtslag.

## SDK-implementering

1. Lägg till [nedladdad](/help/sdk-implement/download-sdks.md#download-2x-sdks) Roku-bibliotek till ditt projekt.

   1. The `AdobeMobileLibrary-2.*-Roku.zip` hämtningsfilen består av följande programvarukomponenter:

      * `adbmobile.brs`: Den här biblioteksfilen inkluderas i Roku-appens källmapp.

      * `ADBMobileConfig.json`: Den här SDK-konfigurationsfilen är anpassad för ditt program.
   1. Lägg till biblioteksfilen och JSON-konfigurationsfilen i projektkällan.

      JSON som används för att konfigurera Adobe Mobile har en exklusiv nyckel för mediefärger som kallas `mediaHeartbeat`. Här tillhör konfigurationsparametrarna för mediets pulsslag.

      >[!TIP]
      >
      >Ett exempel `ADBMobileConfig` JSON-filen medföljer paketet. Kontakta Adobe för att få hjälp med inställningarna.

      Exempel:

      ```
      {
        "version":"1.0",
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8",
          "ssl":true,
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
         "ssl":true,
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
      >If `mediaHeartbeat` är felaktigt konfigurerad, kommer mediemodulen (VHL) att försättas i ett feltillstånd och kommer att sluta skicka spårningsanrop.


1. Konfigurera Experience Cloud Visitor-ID.

   Experience Cloud Visitor ID-tjänsten tillhandahåller ett universellt besökar-ID för olika Experience Cloud-lösningar. Tjänsten för besökar-ID krävs av pulsslag för video och andra integreringar med Marketing Cloud.

   Verifiera att `ADBMobileConfig` config innehåller `marketingCloud` organisations-ID.

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Experience Cloud organisations-ID:n är unika för alla klientföretag i Adobe Marketing Cloud och ser ut ungefär som följande värde: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Se till att du inkluderar `@AdobeOrg`.

   När konfigurationen är klar skapas ett Experience Cloud Visitor-ID som ingår i alla träffar. Andra besökar-ID, t.ex. `custom` och `automatically-generated`, fortsätter att skickas med varje träff.

   **Tjänstmetoder för Experience Cloud Visitor ID**

   >[!TIP]
   >
   >Experience Cloud Visitor-ID-metoder har prefixet `visitor`.

   |  Metod   | Beskrivning |
   | --- | --- |
   | `visitorMarketingCloudID` | Hämtar besökar-ID:t för Experience Cloud från besökarens ID-tjänst.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Med besökar-ID:t för Experience Cloud kan du ange ytterligare kund-ID:n som kan kopplas till varje besökare. Besökar-API:t godkänner flera kund-ID:n för samma besökare och en kundtypsidentifierare för att skilja omfattningen för olika kund-ID:n åt. Den här metoden motsvarar `setCustomerIDs`. Exempel: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Används för att ange Roku-ID för annonsering (RIDA) på SDK. Exempel: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Hämta Roku-ID:t för annonsering (RIDA) med Roku SDK [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API. |
   | `getAllIdentifiers` | Returnerar en lista med alla identifierare som lagras av SDK, inklusive Analytics, Visitor, Audience Manager och anpassade identifierare. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   **Ytterligare offentliga API:er**

   **DebugLogging**

   |  Metod   | Beskrivning |
   | --- | --- |
   | `setDebugLogging` | Används för att aktivera eller inaktivera felsökningsloggning för SDK.  <br/><br/>`ADBMobile().setDebugLogging(true)` |
   | `getDebugLogging` | Returnerar true om felsökningsloggning är aktiverad.  <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   **PrivacyStatus**

   |  Konstant   | Beskrivning |
   | --- | --- |
   | `PRIVACY_STATUS_OPT_IN` | En konstant som ska skickas när setPrivacyStatus anropas för att anmäla sig. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN` |
   | `PRIVACY_STATUS_OPT_OUT` | En konstant som ska skickas när setPrivacyStatus anropas för att avanmäla sig. <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT` |

   |  Metod   | Beskrivning |
   | --- | --- |
   | `setPrivacyStatus` | Anger sekretessstatus för SDK.  <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Hämtar den aktuella sekretessstatusen som angetts för SDK.  <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   >[!IMPORTANT]
   >
   >Se till att du ringer `processMessages` och `processMediaMessages` funktionen i huvudhändelseslingan var 250:e ms för att säkerställa att SDK skickar ut pingarna korrekt.

   |  Metod   | Beskrivning |
   | --- | --- |
   | `processMessages` | Ansvarig för att skicka Analytics-händelser till SDK som ska hanteras.  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Ansvarig för att skicka mediahändelser till den SDK som ska hanteras. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->

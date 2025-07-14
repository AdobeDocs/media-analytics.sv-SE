---
title: Så här konfigurerar du Media SDK för Chromecast
description: Följ de här stegen för att konfigurera Media SDK på Chromecast.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Konfigurera Mobile SDK v3.x för Chromecast {#set-up-chromecast}

I det här avsnittet beskrivs förutsättningarna för att konfigurera en Chromecast-installation för Streaming Media Collection.

## Förutsättningar

* **Hämta giltiga konfigurationsparametrar**

  Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt medieanalyskonto.
* **Ta med följande API:er i mediespelaren**

   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som tillhandahåller spelarinformation* - Den här informationen innehåller information som medienamnet och spelhuvudets position.

Adobe mobiltjänster har ett nytt användargränssnitt som samlar funktioner för mobilmarknadsföring för mobilappar från hela Adobe Marketing Cloud. Från början erbjuder mobiltjänsten smidig integrering av funktioner för appanalys och målinriktning för Adobe Analytics- och Adobe Target-lösningarna. Läs mer på [Adobe Mobile Services-dokumentation.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=sv-SE)

Med Adobe Mobile Library for Chromecast v3.x for Experience Cloud Solutions kan ni mäta Chromecast-applikationer som skrivits i JavaScript, utnyttja och samla in målgruppsdata via målgruppshantering och mäta videoengagemang.

## Mobilbibliotek/SDK-implementering

1. Lägg till ditt hämtade Chromecast-bibliotek i ditt projekt.

   1. ZIP-filen `AdobeMobileLibrary-Chromecast-[version]` består av följande programvarukomponenter:

      * `adbmobile-chromecast.min.js`:

        Den här biblioteksfilen inkluderas i din Chromecast-appkällmapp.

      * `ADBMobileConfig` config

        Den här SDK-konfigurationsfilen är anpassad för ditt program. Ett exempel på `ADBMobileConfig`-implementering finns i SDK (under `samples/`). Hämta rätt inställningar från en Adobe-representant.

   1. Lägg till biblioteksfilen i din `index.html`-fil och skapa den globala variabeln `ADBMobileConfig` enligt följande (den globala variabeln som används för att konfigurera Adobe Mobile för Media Analytics har en exklusiv nyckel med namnet `mediaHeartbeat`):

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
              "rsids": "example.sample.player",
              "server": "example.sc.omtrc.net",
              "ssl": true,
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
              "server": "example.hb-api.omtrdc.net",
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg",
              "channel": "test-channel-chromecast",
              "ssl": true,
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
      >Om `mediaHeartbeat` är felaktigt konfigurerad försätts mediemodulen i ett feltillstånd och skickar inga spårningsanrop.

      ADBMoble Config-parametrar för nyckeln mediaHeartbeat:

   | Konfigurationsparameter | Beskrivning     |
   | --- | --- |
   | `server` | Sträng som representerar URL:en för spårningsslutpunkten på backend-objektet. |
   | `publisher` | En sträng som representerar den unika identifieraren för innehållsutgivaren. |
   | `channel` | En sträng som representerar namnet på innehållsdistributionskanalen. |
   | `ssl` | Boolean som representerar om SSL ska användas för att spåra anrop. |
   | `ovp` | Sträng som representerar namnet på videospelarleverantören. |
   | `sdkversion` | Sträng som representerar den aktuella versionen av programmet/SDK. |
   | `playerName` | Sträng som representerar spelarens namn. |


1. Konfigurera Experience Cloud Visitor-ID.

   Experience Cloud Visitor ID-tjänsten tillhandahåller ett universellt Visitor-ID för alla Experience Cloud-lösningar. Tjänsten för besökar-ID krävs av Media Analytics och andra Marketing Cloud-integreringar.

   Kontrollera att din `ADBMobileConfig`-konfiguration innehåller ditt organisations-ID för `marketingCloud`.

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
   }
   ```

   Experience Cloud organisations-ID:n identifierar unikt varje klientföretag i Adobe Marketing Cloud och ser ut ungefär som följande värde: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Se till att du inkluderar `@AdobeOrg`.

   När konfigurationen är klar genereras ett Experience Cloud Visitor-ID som ingår i alla träffar. Andra besökar-ID:n, som `custom` och `automatically-generated`, fortsätter att skickas med varje träff.

   **Tjänstmetoder för Experience Cloud Visitor ID**

   >[!TIP]
   >
   >Experience Cloud Visitor ID-metoder har prefixet `visitor`.

   | Metod | Beskrivning |
   | --- | --- |
   | `getMarketingCloudID()` | Hämtar Experience Cloud Visitor-ID:t från Visitor-ID-tjänsten.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Med Experience Cloud Visitor-ID kan du ange ytterligare kund-ID:n som kan kopplas till varje besökare. Besökar-API:t godkänner flera kund-ID:n för samma besökare och en kundtypsidentifierare för att skilja omfattningen för olika kund-ID:n åt. Den här metoden motsvarar `setCustomerIDs()` i JavaScript bibliotek.  Till exempel: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |

1. Implementera MediaDelegate-protokollet för spårning av media

   ```js
    var delegate = {
      // Replace <currentPlaybackTime> with the video player current playback time
      getCurrentPlaybackTime = function() {
        return <currentPlaybackTime>;
      },
      // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.
      getQoSObject = function() {
         return ADBMobile.media.createQoSObject(<bitrate>, <startupTime>, <fps>, <droppedFrames>);
      }
    }
   
    ADBMobile.media.setDelegate(delegate);
   }
   ```

<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html?lang=sv-SE) -->

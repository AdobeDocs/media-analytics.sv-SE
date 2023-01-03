---
title: Avanmäl dig och sekretess förklaras
description: Lär dig hur du hanterar anmälan, avanmälan och sekretess.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d2d0f34c64ecb2a900412d5959449c8c36328730
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 1%

---

# Avanmäl dig och sekretess{#opt-out-and-privacy}

## Opt-out / Opt-in {#opt-out-opt-in}

Du kan kontrollera om spårningsaktivitet tillåts på en viss enhet:

* **Mobilappar -** Media Extensions respekterar sekretessinställningarna i datainsamling. Om du vill avanmäla dig från spårning måste du konfigurera sekretess till [Utvalt i taggar](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/#create-a-mobile-property) eller [Uppdatera sekretessstatus för Mobile SDK](https://developer.adobe.com/client-sdks/documentation/privacy-and-gdpr/#getprivacystatus).
* **JavaScript-/webbläsarappar -** VA-biblioteket respekterar `VisitorAPI` sekretess- och alternativinställningar. Om du vill välja bort spårning måste du avanmäla dig från Visitor API-tjänsten. Mer information om avanmälan och sekretess finns på [Adobe Experience Platform identitetstjänst.](https://experienceleague.adobe.com/docs/id-service/using/home.html).
* **OTT-appar (Chromecast, Roku) -** OTT SDK:er tillhandahåller GDPR-klara API:er som gör att du kan ange `opt` statusflaggor för datainsamling och överföring samt för hämtning av lokalt lagrade identiteter.

   >[!NOTE]
   >
   >Anrop till spårning av pulsslag inaktiveras också om sekretessstatusen är inställd på avanmälan.

   Du kan kontrollera om Analytics-data skickas på en viss enhet med följande inställningar:

   * The `privacyDefault` i `ADBMobile.json` config-fil. Detta styr den inledande inställningen och kvarstår tills den ändras i koden.

   * The `ADBMobile().setPrivacyStatus()` -metod.

      * **Avanmäl dig:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
            ```
         >[!IMPORTANT]
         >
         >När en användare väljer bort spårning rensas alla beständiga enhetsdata och ID:n tills användaren väljer tillbaka.

      * **Gå tillbaka:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **Returnera den aktuella inställningen:**

         * **Chromecast:**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku:**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   När sekretessinställningarna har ändrats med `setPrivacyStatus`ändras ändringen permanent tills den ändras igen med den här metoden, eller så avinstalleras och installeras appen igen.

## Hämtar lagrade identifierare (OTT-appar) {#retrieving-stored-identifiers-ott-apps}

Den här informationen hjälper dig att hämta lokalt lagrade användaridentiteter från din Roku-app.

>[!IMPORTANT]
>
>Metoden för att hämta alla identifierare hämtar alla användaridentiteter som är kända och beständiga av SDK:n. Du måste anropa den här metoden **före** en användare avanmäler sig.

De lokalt lagrade identiteterna returneras i en JSON-sträng som kan innehålla:

* Företagskontext - IMS-organisations-ID
* Användar-ID
* Experience Cloud ID (MCID)
* ID för datakälla (DPID, DPUUID)
* Analys-ID:n (AVID, AID, VID och associerade RSID)
* Audience Manager ID (UUID)

Exempel:

* **Chromecast:**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku:**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```

---
title: Anmäl dig och förklara sekretess
description: Lär dig hur du hanterar anmälan, avanmälan och sekretess.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c00c9850d5ea924cef6b4842ecb770df1e78eb21
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Avanmäl dig och integritet{#opt-out-and-privacy}

## Opt-out / Opt-in {#opt-out-opt-in}

Du kan kontrollera om spårningsaktivitet tillåts på en viss enhet:

* **Mobilappar -** Medietilläggen respekterar sekretessinställningarna i datainsamling. Om du vill avanmäla dig från spårning måste du konfigurera sekretess till [Avanmäld i taggar](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/#create-a-mobile-property) eller [Uppdatera sekretessstatus i Mobile SDK](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#getprivacystatus).
* **JavaScript-/webbläsarappar -** VA-biblioteket respekterar inställningarna för sekretess och avvisning i `VisitorAPI` . Om du vill avanmäla spårning måste du avanmäla dig från Visitor API-tjänsten. Mer information om avanmälan och sekretess finns i [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html).
* **OTT-appar (Chromecast, Roku) -** OTT SDK:er tillhandahåller GDPR-förberedda API:er (General Data Protection Regulation) som gör att du kan ange `opt`-statusflaggor för datainsamling och överföring samt hämta lokalt lagrade identiteter.

  >[!NOTE]
  >
  >Anrop till spårning av pulsslag inaktiveras också om sekretessstatusen är inställd på avanmälan.

  Du kan kontrollera om Analytics-data skickas på en viss enhet med följande inställningar:

   * Inställningen `privacyDefault` i konfigurationsfilen `ADBMobile.json`. Detta styr den inledande inställningen och kvarstår tills den ändras i koden.

   * Metoden `ADBMobile().setPrivacyStatus()`.

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

      * **Välj tillbaka:**

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

  När sekretessinställningen har ändrats med `setPrivacyStatus` blir ändringen permanent tills den ändras igen med den här metoden, eller så avinstalleras och installeras appen igen.

## Hämtar lagrade identifierare (OTT-appar) {#retrieving-stored-identifiers-ott-apps}

Den här informationen hjälper dig att hämta lokalt lagrade användaridentiteter från din Roku-app.

>[!IMPORTANT]
>
>Metoden för att hämta alla identifierare hämtar alla användaridentiteter som är kända och beständiga av SDK:n. Du måste anropa den här metoden **innan** en användare avanmäler sig.

De lokalt lagrade identiteterna returneras i en JSON-sträng som kan innehålla:

* Företagskontext - IMS-organisations-ID
* Användar-ID
* Experience Cloud ID (MCID)
* Data-Source-id:n (DPID, DPUUID)
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

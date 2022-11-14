---
title: Avanmäl dig och sekretess förklaras
description: Lär dig hur du hanterar anmälan, avanmälan och sekretess.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 1%

---

# Avanmäl dig och sekretess{#opt-out-and-privacy}

## Opt-out / Opt-in {#opt-out-opt-in}

Du kan kontrollera om spårningsaktivitet tillåts på en viss enhet:

* **Mobilappar -** VA-biblioteket respekterar `AdobeMobile` bibliotekets inställningar för sekretess och avanmälan. Om du vill avanmäla dig från spårning måste du använda `AdobeMobile` bibliotek. Mer information om `AdobeMobile` bibliotekets avanmälan och sekretessinställningar, se [Inställningar för avanmälan och sekretess](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/privacy.html).
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

                &quot;
                ADBMoble.config.setPrivacyStatus(ADBMomobile.config.PRIVACY_STATUS_OPT_OUT)
                &quot;
            
         * **Roku:**

                &quot;
                ADBMomobile().setPrivacyStatus(ADBMomobile().PRIVACY_STATUS_OPT_OUT)
                &quot;
            
            >[!IMPORTANT]
            >
            >När en användare väljer bort spårning rensas alla beständiga enhetsdata och ID:n tills användaren väljer tillbaka.
      * **Gå tillbaka:**

         * **Chromecast:**

                &quot;
                ADBMoble.config.setPrivacyStatus(ADBMomobile.config.PRIVACY_STATUS_OPT_IN)
                &quot;
            
         * **Roku:**

                &quot;
                ADBMomobile().setPrivacyStatus(ADBMomobile().PRIVACY_STATUS_OPT_IN)
                &quot;
            * **Returnera den aktuella inställningen:**

         * **Chromecast:**

                &quot;
                ADBMoble.config.getPrivacyStatus()
                &quot;
            
         * **Roku:**

                &quot;
                ADBMoble().getPrivacyStatus()
                &quot;
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

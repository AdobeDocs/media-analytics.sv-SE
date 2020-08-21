---
title: Konfigurera Adobe Debug
description: I det här avsnittet beskrivs hur du konfigurerar Adobe Debug, som du kan använda för att felsöka Media SDK-implementeringar.
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: tm+mt
source-git-commit: f0f04ffab851999becb2b7771eef36ad7477c9f3
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 1%

---


# Konfigurera Adobe Debug{#configure-adobe-debug}

## Åtkomst till Adobe Debug {#accessing-adobe-debug}

Så här öppnar du Adobe Debug:

1. Gå till [Experience Cloud](https://www.marketing.adobe.com) och skapa en ny Adobe Experience Cloud-användare.

   >[!TIP]
   >
   >Inloggningen är inte samma användarnamn/lösenord som du använder för att logga in på Adobe Analytics.

1. När du har ett Experience Cloud-konto kontaktar du din Adobe-representant för att begära åtkomst till Adobe Debug.
1. När åtkomst har beviljats går du till [https://debug.adobe.com](https://debug.adobe.com) och logga in med hjälp av autentiseringsuppgifterna för Experience Cloud.

   ![](assets/adobe-debug-login.png)

   Följande webbläsare stöds för det här verktyget:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer, version 9-11

De rekommenderade webbläsarna är de senaste versionerna av Chrome och Firefox.

## Felsökningsproxy {#debug-proxy}

Hämta och konfigurera felsökningsproxy:

1. Hämta felsökningsproxyappen på [Apphämtningar.](https://debug.adobe.com/#/downloads)

   Följande operativsystem stöds:
   * OS X 10,7 64-bitars eller högre
   * Windows 7.1 64-bitars eller högre

   ![](assets/debug-proxy-app.png)

1. Proxyservern för felsökning körs på den lokala datorn på port 33284 och anges som systemproxy.

   Du kan behöva justera webbläsarinställningen baserat på operativsystemet och webbläsaren.

## Hämta och installera SSL-certifikatet på skrivbordet eller apparna {#download-and-install-sSL-desktop}

Första gången du kör Adobe Debug genereras ett unikt SSL-certifikat. Om du stöder HTTPS-trafik över skrivbordet och/eller Apps måste du hämta och installera vårt SSL-certifikat.

Hämta och installera SSL-certifikatet:

1. När Adobe Debug har installerats och startats går du till [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) och ladda ned certifieringen.
1. Importera certifikatet

   **Mac OS**
   1. Dubbelklicka på rotcertifikatutfärdarcertifikatet för att öppna det i Keychain Access.
   1. Rotcertifikatutfärdarcertifikatet visas i inloggningen.
   1. Flytta (dra) rotcertifikatutfärdarcertifikatet till System.
   1. Du måste kopiera certifikatet till System för att säkerställa att det är betrott av alla användare och lokala systemprocesser.
   1. Öppna rotcertifikatutfärdarcertifikatet, expandera Förtroende, markera Alltid Förtroende och spara ändringarna.

   **Windows**
   1. Gör något av följande:

      * [Lägga till certifikat i arkivet Betrodda rotcertifikatutfärdare för en lokal dator](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
   1. För Firefox ska du slutföra proceduren i [Installerar rotcertifikat i Mozilla Firefox.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)

      Du kan behöva avsluta och öppna Firefox igen för att se ändringen.
   **iOS-enheter**
   1. Ange iOS-enheten som ska använda Adobe Debug som HTTP-proxy genom att klicka på **[!UICONTROL Settings app]** **>** **[!UICONTROL Wifi settings]**.

   1. I Safari, gå till [Felsök.](https://proxy.debug.adobe.com/ssl)

      Safari kommer att uppmana dig att installera SSL-certifikatet.




## Installera SSL-certifikatet för din mobila enhet {#install-sSL-for-mobile-device}

Om HTTPS-anropen saknas i Adobe Debug måste du installera SSL-certifikatet för Adobe Debug på den mobila enheten.

### iOS

Så här installerar du SSL-certifikatet på en iOS-enhet:

1. Aktivera felsökningsproxy på din bärbara dator och gå till [Adobe Debug.](https://debug.adobe.com)
1. Slutför följande steg på iOS-enheten:
   1. Vrid enheten till flygplansläge.
   1. Markera samma Wi-Fi-signal som används av din bärbara dator.
   1. På din bärbara dator ställer du in IP och port manuellt som visas på felsökningsproxyappen.
   1. Öppna ett webbläsarfönster för Apple Safari.
   1. Gå till [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl)
   1. Hämta och installera SSL-certifikatet.

1. Starta din Adobe Debug-session på din bärbara dator.
1. Börja testa på iOS-enheten.

### Android

Så här installerar du SSL-certifikatet på en Android-enhet:

1. Aktivera felsökningsproxy på din bärbara dator och gå till [Adobe Debug.](https://debug.adobe.com)
1. Slutför följande steg på Android-enheten:
   1. Ställ enheten i flygplansläge.
   1. Markera samma Wi-Fi-signal som används av din bärbara dator.
   1. På din bärbara dator ställer du in IP och port manuellt som visas på felsökningsproxyappen.
   1. Öppna ett webbläsarfönster.
   1. Gå till [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl)
   1. Hämta och installera SSL-certifikatet.

1. Starta din Adobe Debug-session på din bärbara dator.
1. Börja testa på Android-enheten.


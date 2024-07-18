---
title: Konfigurera Adobe Debug
description: "Lär dig konfigurera Adobe Debug, som du kan använda för att felsöka implementeringar av Media SDK."
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
exl-id: 48ad3f23-f36d-44f3-b8d9-b0b3a2ee06bc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Konfigurera Adobe Debug{#configure-adobe-debug}

## Åtkomst till Adobe Debug {#accessing-adobe-debug}

Så här öppnar du Adobe Debug:

1. Gå till [Experience Cloud](https://www.marketing.adobe.com/) och skapa en ny Adobe Experience Cloud-användare.

   >[!TIP]
   >
   >Inloggningen är inte samma användarnamn/lösenord som du använder för att logga in på Adobe Analytics.

1. När du har ett Experience Cloud-konto kontaktar du Adobe och ber om åtkomst till felsökningen i Adobe.
1. När åtkomst har beviljats går du till [https://debug.adobe.com](https://debug.adobe.com) och loggar in med dina inloggningsuppgifter för Experience Cloud.

   ![](assets/adobe-debug-login.png)

   Följande webbläsare stöds för det här verktyget:
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer 9-11

Rekommenderade webbläsare är de senaste versionerna av Chrome och Firefox.

## Felsökningsproxy {#debug-proxy}

Hämta och konfigurera felsökningsproxyn:

1. Hämta appen Debug Proxy på [App Downloads.](https://debug.adobe.com/#/downloads)

   Följande operativsystem stöds:
   * OS X 10.7 64-bitars eller högre
   * Windows 7.1 64-bitars eller senare

   ![](assets/debug-proxy-app.png)

1. Felsökningsproxyservern körs på den lokala datorn på port 33284 och kommer att anges som systemproxy.

   Du kan behöva justera webbläsarinställningen baserat på operativsystemet och webbläsaren.

## Hämta och installera SSL-certifikatet på datorn eller i appar {#download-and-install-sSL-desktop}

Första gången du kör Adobe Debug skapas ett unikt SSL-certifikat. Om du har stöd för HTTPS-trafik mellan datorer och/eller appar måste du hämta och installera vårt SSL-certifikat.

Hämta och installera SSL-certifikatet:

1. När Adobe Debug har installerats och startats går du till [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) och hämtar certifieringen.
1. Importera certifikatet

   **Mac OS**
   1. Dubbelklicka på certifikatutfärdarens rotcertifikat för att öppna det i Nyckelhanterare.
   1. Rotcertifikatutfärdarcertifikatet visas i inloggningen.
   1. Flytta (dra) certifikatutfärdarens rotcertifikat till System.
   1. Du måste kopiera certifikatet till systemet för att säkerställa att det är betrott av alla användare och lokala systemprocesser.
   1. Öppna rotcertifikatutfärdarens certifikat, utöka pålitlighet, välj Alltid pålitlig och spara ändringarna.

   **Windows**
   1. Gör något av följande:

      * [Lägger till certifikat i arkivet Betrodda rotcertifikatutfärdare för en lokal dator](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)

   1. För Firefox slutför du proceduren i [Installera rotcertifikat i Mozilla Firefox.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)

      Du kan behöva stänga och öppna Firefox igen för att se ändringen.

   **iOS-enheter**
   1. Ange att iOS-enheten ska använda Adobe Debug som HTTP-proxy genom att klicka på **[!UICONTROL Settings app]** **>** **[!UICONTROL Wifi settings]**.

   1. Gå till [Felsök i Safari.](https://proxy.debug.adobe.com/ssl)

      Safari uppmanar dig att installera SSL-certifikatet.

## Installera SSL-certifikatet för din mobila enhet {#install-sSL-for-mobile-device}

Om du saknar HTTPS-anrop i Adobe Debug måste du installera SSL-certifikatet för Adobe Debug på den mobila enheten.

### iOS

Så här installerar du SSL-certifikatet på en iOS-enhet:

1. På din bärbara dator aktiverar du felsökningsproxyn och går till [Adobe Debug.](https://debug.adobe.com)
1. Utför följande steg på din iOS-enhet:
   1. Vrid enheten till flygplansläge.
   1. Välj samma Wi-Fi-signal som används av din bärbara dator.
   1. På din bärbara dator anger du IP-adressen och porten som visas i felsökningsproxyappen manuellt.
   1. Öppna webbläsarfönstret i Apple Safari.
   1. Gå till [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Hämta och installera SSL-certifikatet.

1. Starta din Adobe Debug-session på din bärbara dator.
1. Börja testa på din iOS-enhet.

### Android

Så här installerar du SSL-certifikatet på en Android-enhet:

1. Starta felsökningsproxyn på din bärbara dator och gå till [Adobe Debug.](https://debug.adobe.com)
1. Utför följande steg på din Android-enhet:
   1. Ställ in enheten till Flygplansläge.
   1. Välj samma Wi-Fi-signal som används av din bärbara dator.
   1. På din bärbara dator anger du IP-adressen och porten som visas i felsökningsproxyappen manuellt.
   1. Öppna ett webbläsarfönster.
   1. Gå till [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Hämta och installera SSL-certifikatet.

1. Starta din Adobe Debug-session på din bärbara dator.
1. Börja testa på din Android-enhet.

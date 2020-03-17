---
title: Audience Manager-aktivering
description: null
uuid: 8a7f9343-ebc3-4087-9d7e-5972640d2455
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Audience Manager-aktivering{#audience-manager-enablement}

Adobe Audience Manager (AAM), en plattform för datahantering (DMP), hjälper er att samla ihop era målgruppsdata, vilket gör det enkelt att samla in kommersiellt relevant information om webbplatsbesökare, skapa marknadsföringsbara segment och leverera riktad reklam och innehåll till rätt målgrupp.

Med AAM är du inte knuten till någon dataförsäljare, utbytesplattform eller DSP (Demand-Side Platform). Dessutom är AAM helt oberoende när det gäller dina partners datatillgångar. Med tillgång till flera datakällor ger AAM digitala utgivare möjlighet att använda en mängd olika tredjepartsdata och vårt samarbete med privata data. Mer information om AAM finns i AAM-dokumentationen [Audience Manager Product Documentation.](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)

**Dataöverföring från VA till AAM -** För både videoinnehåll och videoannonser kan mätvärden och metadata som samlas in med hjälp av lösningens (reserverade) variabler skickas automatiskt till AAM. Dataöverföringen är tillgänglig på alla plattformar, inklusive datorer, mobiler och OTT. Om du vill aktivera dataöverföringen på serversidan måste du kontakta Adobe Client Care och be om att denna feed aktiveras.

>[!IMPORTANT]
>
>För att säkerställa en smidig överföring av data till AAM bör du ha tillgång till de senaste versionerna av Media SDK-biblioteken.

Federated Data har fullt stöd för datadelning till AAM. Kontakta Adobe-teamet för att få en bekräftelse på Federated Data-inställningarna.

## OTT-/AAM-metoder {#ott-aam-methods}

Du kan använda dessa metoder för att skicka signaler och hämta besökarsegment från Audience Manager:

### Kromecast {#am-chromecast}

* `getVisitorProfile() -`

   Returnerar den besökarprofil som senast hämtades. Returnerar ett tomt objekt om ingen signal har skickats ännu.

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   Returnerar den besökarprofil som senast hämtades. Returnerar ett tomt objekt om ingen signal har skickats ännu.

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   Returnerar aktuellt DPUID.

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   Anger DPID och DPUID. Om DPID och DPUID anges skickas de med varje signal.

   ```js
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   Skickar målgruppshantering en signal med egenskaper.

   ```js
   ADBMobile.audienceManager.SubmitSignal();
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   Returnerar den besökarprofil som senast hämtades. Returnerar ett tomt objekt om ingen signal har skickats ännu.

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   Returnerar den besökarprofil som senast hämtades. Returnerar ett tomt objekt t om ingen signal har skickats ännu.

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   Returnerar aktuellt DPUID.

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   Anger DPID och DPUID. Om DPID och DPUID anges skickas de med varje signal.

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   Skickar målgruppshantering en signal med egenskaper.

   ```js
   ADBMobile().audienceSubmitSignal()
   ```


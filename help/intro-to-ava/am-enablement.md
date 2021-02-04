---
title: Vad är Adobe Audience Manager aktivering?
description: Lär dig hur du länkar programåtgärder till mediespårningsdata utan att behöva använda ytterligare bearbetningsregler och anpassade variabler.
translation-type: tm+mt
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Audience Manager enablement{#audience-manager-enablement}

Adobe Audience Manager (AAM), en plattform för datahantering (DMP), hjälper er att samla ihop era målgruppsdata, vilket gör det enkelt att samla in kommersiellt relevant information om webbplatsbesökare, skapa marknadsföringsbara segment och leverera riktad reklam och innehåll till rätt målgrupp.

Med AAM är du inte knuten till någon dataförsäljare, utbytesplattform eller efterfrågeplattform. Dessutom är AAM helt oberäkneligt när det gäller dina partners datatillgångar. Med tillgång till flera datakällor erbjuder AAM digitala utgivare möjlighet att använda en mängd olika tredjepartsdata och vår privata datainsamling. Mer information om AAM finns i AAM dokumentation [Audience Manager produktdokumentation.](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html).

**VA för AAM dataöverföring -** För både videoinnehåll och videoannonser kan mätvärden och metadata som samlas in med hjälp av lösningens (reserverade) variabler skickas automatiskt till AAM. Dataöverföringen är tillgänglig på alla plattformar, inklusive datorer, mobiler och OTT. Om du vill aktivera dataöverföringen på serversidan måste du kontakta Adobe Client Care och be om att denna feed aktiveras.

>[!IMPORTANT]
>
>För att säkerställa en smidig överföring av data till AAM bör du ha tillgång till de senaste versionerna av Media SDK-biblioteken.

Federated Data har fullt stöd för datadelning till AAM. Kontakta ditt Adobe-team för att få en bekräftelse på Federated Data-inställningarna.

## OTT/AAM metoder {#ott-aam-methods}

Du kan använda dessa metoder för att skicka signaler och hämta besökarsegment från Audience Manager:

### Chromecast {#am-chromecast}

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

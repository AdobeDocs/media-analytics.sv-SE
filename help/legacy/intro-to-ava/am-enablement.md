---
title: Vad är Adobe Audience Manager aktivering?
description: Lär dig hur du länkar programåtgärder till mediespårningsdata utan att behöva använda ytterligare bearbetningsregler och anpassade variabler.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Audience Manager aktivering{#audience-manager-enablement}

Adobe Audience Manager (AAM), en plattform för datahantering (DMP), hjälper er att samla ihop era målgruppsdata, vilket gör det enkelt att samla in kommersiellt relevant information om webbplatsbesökare, skapa marknadsföringsbara segment och leverera riktad reklam och innehåll till rätt målgrupp.

Med AAM är du inte knuten till någon dataförsäljare, utbytesplattform eller efterfrågeplattform. Dessutom är AAM helt oberäkneligt när det gäller dina partners datatillgångar. Med tillgång till flera datakällor erbjuder AAM digitala utgivare möjlighet att använda en mängd olika tredjepartsdata. Mer information om AAM finns i AAM [Audience Manager produktdokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=sv-SE).

**VA för AAM dataöverföring -** För både videoinnehåll och videoannonser kan mätvärden och metadata som samlas in med hjälp av lösningsvariabler (reserverade) skickas automatiskt till AAM. Dataöverföringen är tillgänglig på alla plattformar, inklusive datorer, mobiler och OTT. Om du vill aktivera dataöverföringen på serversidan måste du kontakta Adobe Client Care och be om att denna feed aktiveras.

>[!IMPORTANT]
>
>För att säkerställa en smidig överföring av data till AAM bör du ha tillgång till de senaste versionerna av Media SDK-biblioteken.

Federated Data har fullt stöd för delning av data till AAM. Kontakta ditt Adobe-team för att få en bekräftelse på Federated Data-inställningarna.

## OTT/AAM {#ott-aam-methods}

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
  ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
  ```

* `submitSignal() -`

  Skickar målgruppshantering en signal med egenskaper.

  ```js
  ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
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
  traitData = {}
  traitData["sampleTrait"] = "sampleValue"
  ADBMobile().audienceSubmitSignal(traitData)
  ```

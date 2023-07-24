---
title: Implementera direktuppspelningsmedia för Adobe Analytics eller Customer Journey Analytics
description: Lär dig mer om implementeringsvägar för Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 984f058fda15b1c5e960e4c8d8e2378308d2b541
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Implementera direktuppspelningsmedia för Adobe Analytics eller Customer Journey Analytics

Det finns olika sätt att implementera Streaming Media. En detaljerad jämförelse av enheter och plattformar som stöds för de implementeringsmetoder som beskrivs på den här sidan finns på [Enheter och plattformar som stöds](/help/getting-started/supported-devices.md).

## Implementeringsmetoder för Edge

Vi rekommenderar att du använder Edge när du implementerar Media Analytics för alla nya Adobe Analytics- och Customer Journey Analytics-kunder.

* **Media för Edge Network SDK / Extension:** Samlar in data från iOS- och Android-enheter och skickar dem till Edge. Data kan sedan skickas till Customer Journey Analytics eller Adobe Analytics.

  Mer information om media för Edge Network SDK / Exention finns i [Installera Media Analytics med Experience Platform Edge](/help/implementation/edge/implementation-edge.md).

  >[!NOTE]
  >
  >Den här implementeringsmetoden stöder för närvarande inte Web SDK eller Roku. Båda stöds dock vid implementering med Media Edge API.

* **Media Edge API:** Kan anpassas för att samla in data från alla enheter och format (inklusive mobila enheter, webbenheter och toppmoderna enheter) och skicka data till Edge. Data kan sedan skickas till Customer Journey Analytics eller Adobe Analytics.

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![CJA-arbetsflöde](assets/cja-implementation.png)

## Implementeringsmetoder som endast fungerar i Adobe Analytics

De implementeringsmetoder för Edge som beskrivs ovan rekommenderas för både Customer Journey Analytics och Adobe Analytics, särskilt för nya implementeringar.

Förutom implementeringsmetoderna för Edge finns det andra implementeringsmetoder. Dessa implementeringsmetoder har utformats för användning med Adobe Analytics. Befintliga kunder med någon av följande implementeringsmetoder kan dock fortfarande göra data tillgängliga i Customer Journey Analytics genom att skapa en [Källanslutning för analys](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html).

* **Medietillägg med taggar:** Tillägget Adobe Media Analytics for Audio och Video innehåller funktioner för att lägga till Media Tracker-instansen till en tagghanteringsaktiverad webbplats eller ett tagghanterat projekt. Data skickas till Adobe Analytics.

  Information om hur du installerar, konfigurerar och implementerar medietillägget med taggar finns i [Adobe Media Analytics (3.x SDK) for Audio and Video extension overview](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **Media SDK:**  Med Media SDK kan du mäta flera mediaplattformar, inklusive webbplatser, mobiltelefoner, anslutna TV-apparater, surfplattor, OTT-enheter, digitalboxar och spelkonsoler. (Mer information finns i [Enheter och plattformar som stöds](/help/getting-started/supported-devices.md).)

  Media SDK:er använder Media Collection-API:erna för spårning. Data skickas till Adobe Analytics.

  Mer information om hur du hämtar och installerar SDK:er och tillägg för Media finns i [Hämta SDK:er för media, tillägg med hjälp av taggar och OTT SDK:er](/help/getting-started/download-sdks.md).

* **Media Collection-API:er:** Eftersom API:erna för Media Collection är anpassningsbara kan de användas för program som kräver anpassade spårningsfunktioner och för enheter som inte stöds av Media SDK:er. Media Collection-API:erna spårar ljud- och videohändelser med RESTful HTTP-anrop. Data skickas till Adobe Analytics.

  Mer information om hur du använder API:er för mediainsamling finns i [Media Collection API:er](media-collection-api/mc-api-overview.md).


![Arbetsflöde för analyser](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->

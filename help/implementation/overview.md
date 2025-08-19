---
title: Implementera direktuppspelande medietjänster för Adobe Analytics eller Customer Journey Analytics
description: Läs om implementeringsmöjligheterna för Adobe direktuppspelande medietjänster.
uuid: null
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Implementera direktuppspelande medietjänster för Adobe Analytics eller Customer Journey Analytics

Det finns olika sätt att implementera Adobe direktuppspelade medietjänster. En detaljerad jämförelse av enheter och plattformar som stöds för de implementeringsmetoder som beskrivs på den här sidan finns i [Enheter och plattformar som stöds](/help/getting-started/supported-devices.md).

## Edge implementeringsmetoder

Vi rekommenderar att du använder Edge när du implementerar direktuppspelade medietjänster för alla nya Adobe Analytics- eller Customer Journey Analytics-kunder.

Edge implementeringsmetoder använder tillägget Streaming Media Collection.

* **Media för Edge Network SDK/tillägg:** Samlar in data från webben, iOS- och Android-enheter eller Roku-enheter och skickar dem till Edge Network. Data kan sedan skickas antingen till Customer Journey Analytics eller Adobe Analytics.

  Mer information om Media for Edge Network SDK/Extension finns i [Implementera direktuppspelningsmediesamlingen med Edge Network](/help/implementation/edge/implementation-edge.md).

* **Media Edge API:** Kan anpassas för att samla in data från alla enheter och format (inklusive mobila enheter, webbenheter och toppmoderna enheter) och skicka data till Edge Network. Data kan sedan skickas antingen till Customer Journey Analytics eller Adobe Analytics.

  Mer information om Media Edge API finns i [Översikt över Media Edge API](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![CJA-arbetsflöde](assets/streaming-media-edge.png)

## Implementeringsmetoder som endast fungerar i Adobe Analytics

Edge implementeringsmetoder som beskrivs ovan rekommenderas för både Customer Journey Analytics och Adobe Analytics, särskilt för nya implementeringar.

Förutom Edge implementeringsmetoder finns det andra implementeringsmetoder. Dessa implementeringsmetoder har utformats för användning med Adobe Analytics. Befintliga kunder med någon av följande implementeringsmetoder kan dock fortfarande göra data tillgängliga i Customer Journey Analytics genom att skapa en [Analytics-källanslutning](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html).

Implementeringsmetoderna för Adobe Analytics använder Adobe Analytics for Streaming Media Add-on.

* **Medietillägg med taggar:** Adobe Media Analytics för ljud och video-tillägg innehåller funktioner för att lägga till Media Tracker-instansen till en tagghanteringsaktiverad webbplats eller ett tagghanteringsprojekt. Data skickas till Adobe Analytics.

  Information om hur du installerar, konfigurerar och implementerar medietillägget med taggar finns i [Adobe Media Analytics (3.x SDK) för en översikt över ljud- och videotillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **Media SDK:** Med Media SDK kan du mäta flera medieplattformar, inklusive webbplatser, mobiltelefoner, anslutna TV-apparater, surfplattor, OTT-enheter, digitalboxar och spelkonsoler. (Mer information finns i [Enheter och plattformar som stöds](/help/getting-started/supported-devices.md).)

  Media SDK:er använder Media Collection-API:erna för spårning. Data skickas till Adobe Analytics.

  Information om hur du hämtar och installerar SDK:er och tillägg för media finns i [Hämta SDK:er för media, tillägg med hjälp av taggar och OTT SDK:er](/help/getting-started/download-sdks.md).

* **API:er för mediainsamling:** Eftersom API:erna för mediainsamling är anpassningsbara kan de användas för program som kräver anpassade spårningsfunktioner och för enheter som inte stöds av Media SDK:er. Media Collection-API:erna spårar ljud- och videohändelser med RESTful HTTP-anrop. Data skickas till Adobe Analytics.

  Mer information om hur du använder API:er för mediainsamling finns i [API:er för mediainsamling](media-collection-api/mc-api-overview.md).


![Analysarbetsflöde](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->

---
title: Implementeringssökvägar
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Implementeringssökvägar {#implementation-paths}

Media Analytics (Heartbeats) är Adobes standardiserade videolösning. Den har ersatt Adobes gamla milstolpe-modell.

För var och en av dessa implementeringsvägar måste kunderna kontakta sin säljare/kontoansvarige för att signera en ny försäljningsorder eftersom Media Analytics har en unik SKU och ändringar från en prismodell som baseras på serversamtal till en modell som baseras på videoströmmar:

* **Klientsidan -** Dessa är bara integrering med Media Analytics. Du kan välja SDK för pulsslag och/eller API-integreringar för Media Collection. Den här sökvägen kan användas i alla videospelare, inklusive kund- och/eller OVP-spelare som Brightcove, Ooyala, thePlatform osv.

   Om Media Analytics är den avsedda vägen ska du läsa [Media SDK-implementering](/help/sdk-implement/setup/setup-overview.md) och API:t för [Media Collection.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >För att kunna använda Media Analytics måste kunderna också använda Adobe Analytics.

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch, den efterföljande produkten till Dynamic Tag Management, har ett Media Analytics Launch Extension som gör det lättare att implementera videospårning i era spelare.

   Du kan läsa mer om Experience Platform Launch här: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
* **Adobe Primetime -** Adobe Primetime är en Adobe Experience Cloud-lösning som hjälper innehållsprogrammerare och distributörer att tjäna pengar på medier på alla anslutna skärmar.

   Primetime eliminerar komplexiteten i att nå, tjäna pengar på och aktivera globala målgrupper över olika enheter genom att tillhandahålla en modulär plattform för videopublicering, annonsering, personalisering och analys. Primetime erbjuder dessutom lösningar och värde kring följande:

   * Stöd för exakt mätning av linjära och VOD-innehållstyper.
   * Stöd för mätning av annonsbrytningar med (eller utan) dynamisk annonsinfogning.
   * TVSDK:s smidiga annonsinfogningsmodell möjliggör analyser som direkt mäter annonsuppspelningen, vilket ökar noggrannheten.
   * Robusta uppsättningar av händelser och metadata för att säkerställa exakthet i QoS-buffring eller avbrott i mobilanslutningen samt användarinteraktioner som sökning, pausning och bakgrundsbeläggning på mobilen.
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK är redan integrerat med SDK:n för medieanalys (Heartbeats), som gör implementeringen mycket enklare och snabbare på alla plattformar som stöds. <!--Primetime also supports the partnership with Nielsen.--> Om du vill utnyttja Primetime måste du följa samma riktlinjer och krav som finns i [Client-side](/help/intro-to-ava/implementation-paths/client-side-path.md) tillsammans med följande dokument för din/dina plattform/plattformar: Användarhandbok [för Primetime.](https://helpx.adobe.com/primetime/user-guide.html)

Kontakta även din säljare/kontoansvarige för att diskutera vad du behöver göra för att köpa TVSDK.

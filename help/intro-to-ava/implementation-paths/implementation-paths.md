---
title: Implementeringsvägar
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0bc3928b8e3076feb8e9a16e005cd0415f723408
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 3%

---


# Implementeringsvägar {#implementation-paths}

För varje implementeringsväg måste kunderna kontakta sin säljare/kontoansvarige för att signera en ny försäljningsorder eftersom Media Analytics har en unik SKU och ändringar från en prismodell som baseras på serveranrop till en modell som baseras på videoströmmar.

* **Adobe Launch med Adobe Media Analytics-tillägget**

   Adobe Launch är nästa generations tagghanteringslösning från Adobe. Launch är ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser. Om du vill skapa och underhålla egna integreringar med Launch använder du tillägg. Ett tillägg är ett JavaScript-, HTML- och CSS-paket som utökar startgränssnittet och klientfunktionerna. Mer information finns i användarhandboken för [Experience Platform Launch](https://docs.adobe.com/content/help/en/launch/using/overview.html)

   Adobe Media Analytics-tillägget (MA) lägger till JavaScript Media SDK (Media 2.x SDK) för ljud och video. Det här tillägget innehåller funktioner för att lägga till spårningsinstansen till en startwebbplats eller ett startprojekt. `MediaHeartbeat`

   Adobe Launch med Media Analytics-tillägget kräver följande:
   * Du måste vara en Adobe Experience Cloud-kund.
   * Du måste distribuera Launch- eller DTM-inbäddningskoden på dina webbsidor.
   * [Analystillägg](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Experience Cloud ID-tillägg](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **Klientsidan -** Dessa är bara integrering med Media Analytics. Du kan välja SDK för pulsslag och/eller API-integreringar för Media Collection. Den här sökvägen kan användas i alla videospelare, inklusive kund- och/eller OVP-spelare som Brightcove, Ooyala, thePlatform osv.

   Om Media Analytics är den avsedda vägen ska du läsa [Media SDK-implementering](/help/sdk-implement/setup/setup-overview.md) och API:t för [Media Collection.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >För att kunna använda Media Analytics måste kunderna också använda Adobe Analytics.

* **Adobe Primetime -** Adobe Primetime är en Adobe Experience Cloud-lösning som hjälper innehållsprogrammerare och distributörer att tjäna pengar på medier på alla anslutna skärmar.

   Primetime eliminerar komplexiteten i att nå, tjäna pengar på och aktivera globala målgrupper över olika enheter genom att tillhandahålla en modulär plattform för videopublicering, annonsering, personalisering och analys. Primetime erbjuder dessutom lösningar och värde kring följande:

   * Stöd för exakt mätning av linjära och VOD-innehållstyper.
   * Stöd för mätning av annonsbrytningar med (eller utan) dynamisk annonsinfogning.
   * TVSDK:s smidiga annonsinfogningsmodell möjliggör analyser som direkt mäter annonsuppspelningen, vilket ökar noggrannheten.
   * Robusta uppsättningar av händelser och metadata för att säkerställa exakthet i QoS-buffring eller avbrott i mobilanslutningen samt användarinteraktioner som sökning, pausning och bakgrundsbeläggning på mobilen.
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK är redan integrerat med SDK:n för medieanalys (Heartbeats), som gör implementeringen mycket enklare och snabbare på alla plattformar som stöds. <!--Primetime also supports the partnership with Nielsen.--> Om du vill utnyttja Primetime måste du följa samma riktlinjer och krav som finns i [Client-side](/help/intro-to-ava/implementation-paths/client-side-path.md) tillsammans med följande dokument för din/dina plattform/plattformar: [Användarhandbok för Primetime.](https://helpx.adobe.com/se/primetime/user-guide.html)

Kontakta även din säljare/kontoansvarige för att diskutera vad du behöver göra för att köpa TVSDK.

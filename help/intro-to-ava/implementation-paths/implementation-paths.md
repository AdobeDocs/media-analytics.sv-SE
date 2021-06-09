---
title: Vilka möjligheter till implementering av direktuppspelningsmedia finns?
description: Läs mer om implementeringsvägar för Adobe Streaming Media, inklusive Adobe Launch.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Implementeringsvägar {#implementation-paths}

För varje implementeringsväg måste kunderna kontakta sin säljare/kontoansvarige för att signera en ny försäljningsorder eftersom Streaming Media Analytics har en unik SKU och ändringar från en prismodell som baseras på serveranrop till en modell som baseras på videoströmmar.

* **Adobe Launch med tillägget Adobe Media Analytics**

   Adobe Launch är nästa generation av tagghanteringslösning från Adobe. Launch är ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser. Om du vill skapa och underhålla egna integreringar med Launch använder du tillägg. Ett tillägg är ett JavaScript-, HTML- och CSS-paket som utökar startgränssnittet och klientfunktionerna. Mer information finns i [användarhandboken för Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/overview.html)

   Adobe Media Analytics-tillägget (MA) lägger till JavaScript Media SDK (Media 2.x SDK) för ljud och video. Det här tillägget innehåller funktioner för att lägga till spårningsinstansen `MediaHeartbeat` på en startwebbplats eller ett startprojekt.

   Adobe Launch med Media Analytics-tillägget kräver följande:
   * Du måste vara kund hos Adobe Experience Cloud.
   * Du måste distribuera Launch- eller DTM-inbäddningskoden på dina webbsidor.
   * [Analystillägg](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Experience Cloud ID-tillägg](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **Klientsidan -** Dessa är bara integrering med Media Analytics. Du kan välja SDK för pulsslag och/eller API-integreringar för Media Collection. Den här sökvägen kan användas i alla videospelare, inklusive kund- och/eller OVP-spelare som Brightcove, Ooyala, thePlatform osv.

   Om Media Analytics är den avsedda vägen ska du läsa [Media SDK-implementering](/help/sdk-implement/setup/setup-overview.md) och [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >För att kunna använda Media Analytics måste kunderna också använda Adobe Analytics.

* **Adobe Primetime-** Adobe Primetime är en Adobe Experience Cloud-lösning som hjälper innehållsprogrammerare och distributörer att tjäna pengar på medier på alla anslutna skärmar.

   Primetime eliminerar komplexiteten i att nå, tjäna pengar på och aktivera globala målgrupper över olika enheter genom att tillhandahålla en modulär plattform för videopublicering, annonsering, personalisering och analys. Primetime erbjuder dessutom lösningar och värde kring följande:

   * Stöd för exakt mätning av linjära och VOD-innehållstyper.
   * Stöd för mätning av annonsbrytningar med (eller utan) dynamisk annonsinfogning.
   * TVSDK:s smidiga annonsinfogningsmodell möjliggör analyser som direkt mäter annonsuppspelningen, vilket ökar noggrannheten.
   * Robusta uppsättningar av händelser och metadata för att säkerställa exakthet över QoS-buffring eller avbrott i den mobila anslutningen och slutanvändarinteraktioner som sökning, pausning och bakgrundsrundning på mobilen.

<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK är redan integrerat med SDK:n för medieanalys (Heartbeats), som gör implementeringen mycket enklare och snabbare på alla plattformar som stöds. <!--Primetime also supports the partnership with Nielsen.--> Om du vill utnyttja Primetime måste du följa samma riktlinjer och krav som finns i  [Client-](/help/intro-to-ava/implementation-paths/client-side-path.md) sidetillsammans med följande dokument för din/dina plattform/plattformar:  [Användarhandbok för Primetime.](https://helpx.adobe.com/se/primetime/user-guide.html)

Kontakta även din säljare/kontoansvarige för att diskutera vad du behöver göra för att köpa TVSDK.

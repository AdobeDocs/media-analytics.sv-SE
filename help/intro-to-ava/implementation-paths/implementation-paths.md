---
title: Vilka möjligheter till implementering av direktuppspelningsmedia finns?
description: Läs mer om implementeringsvägar för Adobe Streaming Media, inklusive Adobe Experience Platform Data Collection.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Implementeringsvägar {#implementation-paths}

För varje implementeringsväg måste kunderna kontakta sin säljare/kontoansvarige för att signera en ny försäljningsorder eftersom Streaming Media Analytics har en unik SKU och ändringar från en prismodell som baseras på serveranrop till en modell som baseras på videoströmmar.

## Adobe Experience Platform Data Collection med tillägget Adobe Media Analytics

>[!NOTE]
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) för en konsoliderad hänvisning till terminologiska förändringar.


Taggar i Adobe Experience Platform är nästa generation av tagghanteringsfunktioner från Adobe. Taggar ger kunderna ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser. Adobe Experience Cloud-kunder erbjuds märkord som en av de funktioner som tillför mervärde.

Taggar ger alla möjlighet att bygga och underhålla egna integreringar, så kallade tillägg. Dessa tillägg är tillgängliga för Adobe Experience Cloud-kunder i en appbutik så att de snabbt kan installera, konfigurera och distribuera sina taggar.

Ett tillägg är ett kodpaket (JavaScript, HTML och CSS) som utökar taggfunktionaliteten. Bygg, hantera och uppdatera integreringarna med hjälp av ett praktiskt taget självbetjäningsgränssnitt. Du kan tänka dig tillägg som appar som du använder för att utföra dina uppgifter.Mer information finns i *Översikt över taggar* artikel i [Adobe Experience Platform Documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)

Adobe Media Analytics-tillägget (MA) lägger till JavaScript Media SDK (Media 2.x SDK) för ljud och video. Det här tillägget innehåller funktioner för att lägga till `MediaHeartbeat` spårningsinstans till en datainsamlingswebbplats eller ett projekt.

Adobe Data Collection med Media Analytics-tillägget kräver följande:
* Du måste vara kund hos Adobe Experience Cloud.
* Du måste distribuera datainsamling eller DTM-inbäddningskod på dina webbsidor.
* [Analystillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html)
* [Experience Cloud ID-tillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html)


## Klientsida

Det här är bara integreringar med Media Analytics. Du kan välja SDK för pulsslag och/eller API-integreringar för Media Collection. Den här sökvägen kan användas i alla videospelare, inklusive kund- och/eller OVP-spelare som Brightcove, Ooyala, thePlatform osv.

Om Media Analytics är er avsedda väg kan du läsa [Media SDK-implementering](/help/sdk-implement/setup/setup-overview.md) och [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>För att kunna använda Media Analytics måste kunderna också använda Adobe Analytics.

## Adobe Primetime

Adobe Primetime är en Adobe Experience Cloud-lösning som hjälper innehållsprogrammerare och distributörer att tjäna pengar på medier på alla anslutna skärmar.

Primetime eliminerar komplexiteten i att nå, tjäna pengar på och aktivera globala målgrupper över olika enheter genom att tillhandahålla en modulär plattform för videopublicering, annonsering, personalisering och analys. Primetime erbjuder dessutom lösningar och värde kring följande:

* Stöd för exakt mätning av linjära och VOD-innehållstyper.
* Stöd för mätning av annonsbrytningar med (eller utan) dynamisk annonsinfogning.
* TVSDK:s smidiga annonsinfogningsmodell möjliggör analyser som direkt mäter annonsuppspelningen, vilket ökar noggrannheten.
* Robusta uppsättningar av händelser och metadata för att säkerställa exakthet i QoS-buffring eller avbrott i mobilanslutningen samt användarinteraktioner som sökning, pausning och bakgrundsbeläggning på mobilen.
* Integrerat stöd för Nielsen DTVR (linjär) med ID3-metadata och DCR med CMS-metadata.


TVSDK är redan integrerat med SDK:n för medieanalys (Heartbeats), som gör implementeringen mycket enklare och snabbare på alla plattformar som stöds. Om du vill utnyttja Primetime måste du följa samma riktlinjer och krav som finns i [Klientsidan](/help/intro-to-ava/implementation-paths/client-side-path.md) tillsammans med följande dokument för din/dina plattform/plattformar: [Användarhandbok för Primetime.](https://helpx.adobe.com/se/primetime/user-guide.html)

Kontakta även din säljare/kontoansvarige för att diskutera vad du behöver göra för att köpa TVSDK.

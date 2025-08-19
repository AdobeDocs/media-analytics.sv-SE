---
title: Vilka möjligheter till implementering av direktuppspelningsmedia finns?
description: Läs om implementeringsvägar för Adobe Streaming Media, inklusive Adobe Experience Platform Data Collection.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 4%

---

# Implementeringssökvägar {#implementation-paths}

**DET HÄR INNEHÅLLET FLYTTADES TILL DEN AKTUELLA IMPLEMENTERINGSBANSFILEN**

För varje implementeringsväg måste kunderna kontakta sin säljare eller Adobe Account Team för att signera en ny försäljningsorder eftersom Customer Journey Analytics Streaming Media Collection och Adobe Analytics for Streaming Media har en unik SKU och ändringar från en prismodell som baseras på serversamtal till en modell som baseras på videoströmmar.

## Adobe Experience Platform Data Collection med Adobe Media Analytics-tillägget

>[!NOTE]
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=sv-SE) för en konsoliderad referens av terminologiändringarna.


Taggar i Adobe Experience Platform är nästa generation av tagghanteringsfunktioner från Adobe. Taggar ger kunderna ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser. Adobe Experience Cloud-kunder erbjuds märkord som en av de funktioner som tillför mervärde.

Taggar ger alla möjlighet att bygga och underhålla egna integreringar, så kallade tillägg. Dessa tillägg är tillgängliga för Adobe Experience Cloud-kunder i en appbutik så att de snabbt kan installera, konfigurera och distribuera sina taggar.

Ett tillägg är ett kodpaket (JavaScript, HTML och CSS) som utökar taggfunktionaliteten. Bygg, hantera och uppdatera integreringarna med hjälp av ett praktiskt taget självbetjäningsgränssnitt. Du kan tänka dig tillägg som appar som du använder för att utföra dina uppgifter.Mer information finns i artikeln *Taggreöversikt* i [Adobe Experience Platform-dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv-SE)

Adobe Media Analytics-tillägget (MA) lägger till JavaScript Media SDK (Media 2.x SDK) för ljud och video. Det här tillägget innehåller funktioner för att lägga till spårningsinstansen `MediaHeartbeat` till en datainsamlingswebbplats eller ett projekt.

Adobe Data Collection med Media Analytics-tillägget kräver följande:
* Du måste vara kund hos Adobe Experience Cloud.
* Du måste distribuera datainsamling eller DTM-inbäddningskod på dina webbsidor.
* [Analystillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=sv-SE)
* [Experience Cloud ID-tillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=sv-SE)


## Klientsida

Det här är bara integreringar med Media Analytics. Du kan välja mellan SDK och/eller API-integreringar för Media Collection. Den här sökvägen kan användas i alla videospelare, inklusive kund- och/eller OVP-spelare som Brightcove, Ooyala, thePlatform osv.

Om Media Analytics är den avsedda vägen ska du läsa [Media SDK Implementation](/help/legacy/setup/legacy-setup-overview.md) och [Media Collection API.](/help/implementation/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>För att kunna använda Media Analytics måste kunderna också använda Adobe Analytics.

## Adobe Primetime

Adobe Primetime är en Adobe Experience Cloud-lösning som hjälper innehållsprogrammerare och distributörer att tjäna pengar på medier på alla anslutna skärmar.

Primetime eliminerar komplexiteten i att nå, tjäna pengar på och aktivera globala målgrupper över olika enheter genom att tillhandahålla en modulär plattform för videopublicering, annonsering, personalisering och analys. Primetime erbjuder dessutom lösningar och värde kring följande:

* Stöd för exakt mätning av VOD och linjär innehållstyp.
* Stöd för mätning av annonsbrytningar med (eller utan) dynamisk annonsinfogning.
* TVSDK:s smidiga annonsinfogningsmodell möjliggör analyser som direkt mäter annonsuppspelningen, vilket ökar noggrannheten.
* Robusta uppsättningar av händelser och metadata för att säkerställa exakthet över QoS-buffring eller avbrott i den mobila anslutningen och slutanvändarinteraktioner som sökning, pausning och bakgrundsbeläggning på mobilen.
* Integrerat stöd för Nielsen DTVR (linjärt) med ID3-metadata och DCR med CMS-metadata.


TVSDK är redan integrerat med SDK Media Analtyics (Heartbeats), som gör implementeringen mycket enklare och snabbare på alla plattformar som stöds. Om du vill utnyttja Primetime måste du följa samma riktlinjer och krav som finns i [Klientsidan](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md) tillsammans med följande dokument för plattformarna: [Användarhandbok för Primetime.](https://helpx.adobe.com/se/primetime/user-guide.html)

Kontakta även din säljare/kontoansvarige för att diskutera vad du behöver göra för att köpa TVSDK.

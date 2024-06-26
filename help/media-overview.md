---
title: Adobe Streaming Media Collection - översikt
description: Använd tillägget Streaming Media Collection för att få kraftfulla insikter om innehåll, ljud och annonser.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 9%

---

# Adobe Streaming Media Collection - översikt

![Banderoll](./assets/media_analytics_banner.png)

Tillägget Adobe Streaming Media Collection innehåller kraftfulla verktyg för insamling, mätning och anpassning av direktuppspelat mediematerial, som ljud, video och reklam för leverantörer av direktuppspelade media. Ni kan kombinera data för direktuppspelande media med funktioner som Audience Analytics, Mobile eller Cross-Device Analytics.

Strömmande mediedata kan enkelt integreras i följande Adobe Experience Platform-produkter:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Kontakta din säljare eller ditt kontoteam på Adobe för att se till att tillägget för direktuppspelad mediesamling ingår i din produktportfölj om du vill implementera en mediesamling för direktuppspelning.

## Viktiga funktioner

Fördelarna med tillägget Streaming Media Collection är bland annat övervakning i realtid, detaljerad analys, användbara insikter, intäktsmöjligheter med mera.

* **Realtidsanalys**: Fatta konkreta beslut i realtid med nyckeltal som mediestart, över flera kanaler.

  Med tillägget Streaming Media Collection får du nästan detaljinformation om varaktighet, stopp och start i realtid så att du kan utvärdera och kombinera video- och ljudstatistik. Dessa insikter gör att ni kan förstå kundernas tittande och avlyssningsvanor och öka engagemanget med personaliserade rekommendationer.

* **Engagera med andra**: Engagera användarna genom färre buffringshändelser och genom att förstå var och när annonser ska spelas upp i innehållet för att skapa en smidig och mindre påträngande upplevelse som levererar återkommande besök.

* **Holistisk bild**: Kombinera flera datapunkter för alla era innehållsdistributörer för att få en fullständig bild av all medieaktivitet. Mät engagemanget och se/lyssna på alla möjliga kanaler.

  Med tillägget Streaming Media Collection kan ni spåra hela kundresan på hela webbplatsen och direktuppspelande appar för att visualisera kundens väg och intressen och för att ge förbättrade rekommendationer och personalisera kundupplevelser.  Med mediemätning kan ni kategorisera data i flera dimensioner och segment och samla in alla metadata ni behöver för att göra en fullständig och detaljerad analys. Sedan kan ni analysera data och attribuera framgångsmått för helt konsumerad media, genomsnittlig tid som tillbringats på platsen och slutförda annonser.

* **Vitala mått**: Mät viktiga leveransvärden relaterade till Experience Quality of Experience (QoE), t.ex. uteslutna bildrutor, använd buffringstid och genomsnittlig bithastighet.

* **Ökad granularitet**: Utvärdera visningsbeteendet på den mest detaljerade nivån, inklusive besökarnas tid på dygnet, samtidigt återkommande tittare eller avlyssnare per minut och genomsnittlig tid som innehållet förbrukades.

* **Exakt mätning**: Mät på olika enheter som används för mediekonsumtion, inklusive OTT, smarttelefon, surfplatta, dator med mera, för att övervaka användarnas engagemangsmönster och vanor.

* **Segmentering**: Använd klassificeringar på spelare, enheter, genrer, kapitel och bildspel för att se hur de påverkar era övergripande vyer/avlyssningar och kundernas engagemang med innehåll, ljud, annonser och kombinationer.


## Så här fungerar det

Spårningsdata för direktuppspelande media samlas in från en spelare med Media for Edge Network SDK/Extension, Media Extension with Tags, Media SDKs, Media Edge API eller Media Collection API.

Alla detaljerade data (upp till 10 sekunder) skickas antingen till tjänsten Media Analytics eller Experience Edge (beroende på [implementeringsmetod](/help/implementation/overview.md) du väljer), som samlar in och bearbetar data för varje enskild uppspelningssession.

När uppspelningssessionen är slut skickas beräknade spårningsdata antingen till Adobe Analytics eller Customer Journey Analytics för lagring och rapportering.

>[!NOTE]
>
>Med Customer Journey Analytics-implementeringar kan data skickas till Customer Journey Analytics antingen med Experience Edge eller med hjälp av Analytics Data Connector (ADC).


Detaljerad information om de olika implementeringsmetoderna finns i [Implementera tillägget Streaming Media Collection för Adobe Analytics eller Customer Journey Analytics](/help/implementation/overview.md).

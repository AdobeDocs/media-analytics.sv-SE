---
title: Adobe Analytics for Streaming Media - översikt
description: Använd Streaming Media Analytics för att få kraftfulla insikter om innehåll, ljud och annonser.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 9%

---

# Adobe Analytics for Streaming Media - översikt

![Banderoll](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media innehåller kraftfulla mätverktyg för ljud, video och reklam. Ni kan kombinera Streaming Media-statistik med andra Adobe Analytics-funktioner, som Audience Analytics, Mobile eller Cross-Device Analytics.

Direktuppspelningsmedia kan köpas som tillägg till Adobe Analytics<!-- update this when SKUs are available for other AEP products -->och Streaming Media-statistik kan enkelt integreras i följande Adobe Experience Platform-produkter:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Om du vill implementera Adobe Analytics Streaming Media kontaktar du säljaren på Adobe eller kontoteamet på Adobe för att försäkra dig om att Streaming Media ingår i din produktportfölj.

## Viktiga funktioner

Fördelarna med Adobe Analytics för Streaming Media är bland annat övervakning i realtid, detaljerad analys, användbara insikter, intäktsmöjligheter med mera.

* **Realtidsanalys**: Fatta konkreta beslut i realtid med nyckeltal som mediestart, över flera kanaler.

  Med Analytics for Streaming Media får ni nästan detaljrika detaljer om varaktighet, stopp och start i realtid så att ni kan utvärdera och kombinera video- och ljudmätvärden. Dessa insikter gör att ni kan förstå kundernas tittande och avlyssningsvanor och öka engagemanget med personaliserade rekommendationer.

* **Engagera med andra**: Engagera användarna genom färre buffringshändelser och genom att förstå var och när annonser ska spelas upp i innehållet för att skapa en smidig och mindre påträngande upplevelse som levererar återkommande besök.

* **Holistisk bild**: Kombinera flera datapunkter för alla era innehållsdistributörer för att få en fullständig bild av all medieaktivitet. Mät engagemanget och se/lyssna på alla möjliga kanaler.

  Med Adobe Analytics for Streaming Media kan ni spåra hela kundresan på hela webbplatsen och direktuppspelningsappar för att visualisera kundens kundväg och intressen och tillhandahålla förbättrade rekommendationer och personalisera kundupplevelser.  Med mediemätning kan ni kategorisera data i flera dimensioner och segment och samla in alla metadata ni behöver för att göra en fullständig och detaljerad analys. Sedan kan ni analysera data och attribuera framgångsmått för helt konsumerad media, genomsnittlig tid som tillbringats på platsen och slutförda annonser.

* **Vitala mått**: Mät viktiga leveransvärden relaterade till Experience Quality of Experience (QoE), t.ex. uteslutna bildrutor, använd buffringstid och genomsnittlig bithastighet.

* **Ökad granularitet**: Utvärdera visningsbeteendet på den mest detaljerade nivån, inklusive besökarnas tid på dygnet, samtidigt återkommande tittare eller avlyssnare per minut och genomsnittlig tid som innehållet förbrukades.

* **Exakt mätning**: Mät på olika enheter som används för mediekonsumtion, inklusive OTT, smarttelefon, surfplatta, dator med mera, för att övervaka användarnas engagemangsmönster och vanor.

* **Segmentering**: Använd klassificeringar på spelare, enheter, genrer, kapitel och bildspel för att se hur de påverkar era övergripande vyer/avlyssningar och kundernas engagemang med innehåll, ljud, annonser och kombinationer.


## Så här fungerar det

Spårningsdata för direktuppspelande media samlas in från en spelare med Media for Edge Network SDK/Extension, Media Extension med taggar, Media SDK, Media Edge API eller Media Collection API.

Alla detaljerade data (upp till 10 sekunder) skickas antingen till tjänsten Media Analytics eller Experience Edge (beroende på [implementeringsmetod](/help/implementation/overview.md) du väljer), som samlar in och bearbetar data för varje enskild uppspelningssession.

När uppspelningssessionen är slut skickas beräknade spårningsdata antingen till Adobe Analytics eller Customer Journey Analytics för lagring och rapportering.

>[!NOTE]
>
>Med Customer Journey Analytics-implementeringar kan data skickas till Customer Journey Analytics antingen med Experience Edge eller med hjälp av Analytics Data Connector (ADC).


Detaljerad information om de olika implementeringsmetoderna finns i [Implementera direktuppspelningsmedia för Adobe Analytics eller Customer Journey Analytics](/help/implementation/overview.md).

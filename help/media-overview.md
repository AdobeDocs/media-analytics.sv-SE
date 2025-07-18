---
title: Adobe Streaming Media Collection - översikt
description: Använd Streaming Media Collection för att få kraftfulla insikter om innehåll, ljud och annonser.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 9%

---

# Adobe Streaming Media Collection - översikt

![Banderoll](./assets/media_analytics_banner.png)

Adobe Streaming Media Collection innehåller kraftfulla verktyg för insamling, mätning och personalisering av direktuppspelat mediematerial som ljud, video och reklam för medieföretag som levererar direktuppspelande media. Ni kan kombinera data för direktuppspelande media med funktioner som Audience Analytics, Mobile eller Cross-Device Analytics.

Strömmande mediedata kan enkelt integreras i följande Adobe Experience Platform-produkter:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Plattform för kunddata i realtid

>[!IMPORTANT]
>
>Om du vill implementera Streaming Media Collection kontaktar du Adobe eller Adobe Account Team för att kontrollera att Streaming Media Collection-tillägget ingår i din produktportfölj.

## Viktiga funktioner

Fördelarna med Streaming Media Collection är bland annat övervakning i realtid, detaljerad analys, användbara insikter, intäktsmöjligheter med mera.

* **Realtidsanalys**: Fatta konkreta, åtgärdbara beslut i realtid med hjälp av nyckeltal som mediefrekvenser som startar i flera kanaler.

  Med Streaming Media Collection får du nästan detaljinformation om varaktighet, stopp och start i realtid så att du kan utvärdera och kombinera video- och ljudstatistik. Dessa insikter gör att ni kan förstå kundernas tittande och avlyssningsvanor och öka engagemanget med personaliserade rekommendationer.

* **Öka engagemanget**: Engagera användarna fullständigt genom färre buffringshändelser och förstå var och när annonser ska spelas upp i innehållet för att skapa en smidig, mindre påträngande upplevelse som levererar upprepade besök.

* **Holistisk bild**: Kombinera flera datapunkter i alla innehållsdistributörer för att få en fullständig bild av all medieaktivitet. Mät engagemanget och se/lyssna på alla möjliga kanaler.

  Med Streaming Media Collection kan ni spåra hela kundresan på hela webbplatsen och direktuppspelningsappar för att visualisera kundens väg och intressen och tillhandahålla förbättrade rekommendationer och personalisera kundupplevelser.  Med mediemätning kan ni kategorisera data i flera dimensioner och segment och samla in alla metadata ni behöver för att göra en fullständig och detaljerad analys. Sedan kan ni analysera data och attribuera framgångsmått för helt konsumerad media, genomsnittlig tid som tillbringats på platsen och slutförda annonser.

* **Vitala mått**: Mät vitala leveransvärden relaterade till Quality of Experience (QoE), t.ex. uteslutna bildrutor, använd buffringstid och genomsnittlig bithastighet.

* **Ökad granularitet**: Utvärdera visningsbeteendet på den mest detaljerade nivån, inklusive enskild besökartid på dagen, samtidiga visningsprogram eller avlyssnare per minut och den genomsnittliga tid som innehållet förbrukades.

* **Exakt mätning**: Mät på flera enheter som används för mediekonsumtion, inklusive OTT, smarttelefon, surfplatta, dator med mera, för att övervaka användarnas interaktionsmönster och vanor.

* **Segmentering**: Använd klassificeringar på spelare, enheter, genrer, kapitel och bildspel för att se hur de påverkar era övergripande vyer/avlyssningar och kundengagemang med innehåll, ljud, annonser och kombinationer.


## Så här fungerar det

Spårningsdata för direktuppspelande media samlas in från en spelare med Media for Edge Network SDK/Extension, Media Extension with Tags, Media SDKs, Media Edge API eller Media Collection API.

Alla detaljerade data (upp till 10 sekunder) skickas antingen till Media Analytics-tjänsten eller Experience Edge (beroende på vilken [implementeringsmetod](/help/implementation/overview.md) du väljer), som samlar in och bearbetar data för varje enskild uppspelningssession.

När uppspelningssessionen är slut skickas beräknade spårningsdata antingen till Adobe Analytics eller Customer Journey Analytics för lagring och rapportering.

>[!NOTE]
>
>Med Customer Journey Analytics-implementeringar kan data skickas till Customer Journey Analytics antingen med Experience Edge eller med Analytics Data Connector (ADC).


Mer information om de olika implementeringsmetoderna finns i [Implementera Streaming Media Collection för Adobe Analytics eller Customer Journey Analytics](/help/implementation/overview.md).

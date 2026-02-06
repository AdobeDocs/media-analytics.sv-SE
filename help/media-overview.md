---
title: Översikt över Adobe direktuppspelningsmedia
description: Använd Adobe Streaming Media-lösningar för att få kraftfulla insikter om innehåll, ljud och annonser.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 9%

---

# Översikt över Adobe direktuppspelade medietjänster

![Banderoll](./assets/media_analytics_banner.png)

Adobe direktuppspelade medietjänster innehåller kraftfulla verktyg för insamling, mätning och anpassning av direktuppspelat mediematerial, som ljud, video och reklam för leverantörer av direktuppspelade media. Ni kan kombinera data för direktuppspelande media med funktioner som Audience Analytics, Mobile eller Cross-Device Analytics.

Strömmande mediedata kan enkelt integreras i följande Adobe Experience Platform-produkter:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Plattform för kunddata i realtid

>[!IMPORTANT]
>
>Om du vill implementera streaming media-tjänsterna kontaktar du Adobe säljare eller Adobe Account Team och ser till att tillägget Customer Journey Analytics Streaming Media Collection eller Adobe Analytics for Streaming Media Add-on ingår i din produktportfölj.

## Viktiga funktioner

Fördelarna med direktuppspelande medietjänster är bland annat övervakning i realtid, detaljerad analys, användbara insikter, intäktsmöjligheter med mera.

* **Realtidsanalys**: Fatta konkreta, åtgärdbara beslut i realtid med hjälp av nyckeltal som mediefrekvenser som startar i flera kanaler.

  Med direktuppspelningstjänsterna får du nästan detaljrika detaljer om varaktighet, stopp och start i realtid så att du kan utvärdera och kombinera video- och ljudstatistik. Dessa insikter gör att ni kan förstå kundernas tittande och avlyssningsvanor och öka engagemanget med personaliserade rekommendationer.

* **Öka engagemanget**: Engagera användarna fullständigt genom färre buffringshändelser och förstå var och när annonser ska spelas upp i innehållet för att skapa en smidig, mindre påträngande upplevelse som levererar upprepade besök.

* **Holistisk bild**: Kombinera flera datapunkter i alla innehållsdistributörer för att få en fullständig bild av all medieaktivitet. Mät engagemanget och se/lyssna på alla möjliga kanaler.

  Med direktuppspelande medietjänster kan ni spåra hela kundresan på hela webbplatsen och direktuppspelande appar för att visualisera kundens kundväg och intressen och tillhandahålla förbättrade rekommendationer och personalisera kundupplevelser.  Med mediemätning kan ni kategorisera data i flera dimensioner och segment och samla in alla metadata ni behöver för att göra en fullständig och detaljerad analys. Sedan kan ni analysera data och attribuera framgångsmått för helt konsumerad media, genomsnittlig tid som tillbringats på platsen och slutförda annonser.

* **Vitala mått**: Mät vitala leveransvärden relaterade till Quality of Experience (QoE), t.ex. uteslutna bildrutor, använd buffringstid och genomsnittlig bithastighet.

* **Ökad granularitet**: Utvärdera visningsbeteendet på den mest detaljerade nivån, inklusive enskild besökartid på dagen, samtidiga visningsprogram eller avlyssnare per minut och den genomsnittliga tid som innehållet förbrukades.

* **Exakt mätning**: Mät på flera enheter som används för mediekonsumtion, inklusive OTT, smarttelefon, surfplatta, dator med mera, för att övervaka användarnas interaktionsmönster och vanor.

* **Segmentering**: Använd klassificeringar på spelare, enheter, genrer, kapitel och bildspel för att se hur de påverkar era övergripande vyer/avlyssningar och kundengagemang med innehåll, ljud, annonser och kombinationer.


## Så här fungerar det

Spårningsdata för direktuppspelande medietjänster samlas in från en spelare med Media for Edge Network SDK/Extension, Media Extension med taggar, Media SDK, Media Edge API eller Media Collection API.

Alla detaljerade data (upp till 10 sekunder) skickas antingen till Media Analytics-tjänsten eller Experience Edge (beroende på vilken [implementeringsmetod](/help/implementation/overview.md) du väljer), som samlar in och bearbetar data för varje enskild uppspelningssession.

När uppspelningssessionen är slut skickas beräknade spårningsdata antingen till Adobe Analytics eller Customer Journey Analytics för lagring och rapportering.

>[!NOTE]
>
>Med Customer Journey Analytics-implementeringar kan data skickas till Customer Journey Analytics antingen med Experience Edge eller med Analytics Data Connector (ADC).


Mer information om de olika implementeringsmetoderna finns i [Implementera direktuppspelningsmedietjänster för Adobe Analytics eller Customer Journey Analytics](/help/implementation/overview.md).

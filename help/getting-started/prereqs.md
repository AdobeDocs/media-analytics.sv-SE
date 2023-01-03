---
title: Lär dig om krav för direktuppspelande media
description: Kom igång med Adobe Analytics Streaming Media. Lär dig vad ni behöver för att implementera Adobe Analytics för direktuppspelande media.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b022bed6b7be0cc97caaaf6b7bbc42474a57b400
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Förutsättningar{#prerequisites}

Så här implementerar du Adobe Analytics för direktuppspelningsmedia:

1. **Bekräfta prismodellen för strömmande media**<br>
Den aktuella prismodellen bygger på videoströmmar. Kontakta vid behov din säljare eller kontoansvarige för att signera en ny försäljningsorder eftersom Streaming Media Analytics säljs separat från Adobe Analytics.

1. **Bekräfta att du implementerar Adobe Analytics**<br>
Streaming Media för Adobe Analytics kräver också en grundläggande Adobe Analytics-implementering. Se [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) för mer information.

1. **Hämta URL:en för mediespårningsservern**<br>
Be din Adobe Analytics-representant om URL:en för mediespårningsservern. Det här är 
`collection-api-server` URL för Mobile SDK, JavaScript SDK och spårningsservern utan samlings-api för Roku. Domännamn för API-implementering är: `[your_namespace].hb-api.omtrdc.net`.

1. **Hämta aktuell Media SDK eller implementera nödvändiga tillägg**<br>
Beroende på implementeringsvägen, [ladda ned aktuell SDK](download-sdks.md) för webb, mobiler och plattformar som ligger ovanpå varandra. De tillägg som krävs måste implementeras för att Adobe Analytics ska kunna aktiveras för sökvägar för medietillägg för direktuppspelning.

1. **Aktivera Adobe Analytics-rapporter**<br>
Om du vill aktivera rapporter i Analytics och visa innehåll och annonsuppgifter som du samlar in måste du aktivera rapporter i Analytics. Se [Aktivera medierapporter](/help/reporting/media-reports-enable.md).

1. **Aktivera Experience Cloud**<br>


## Implementera Adobe Experience Platform Identity Service. {#implement-id}

The **Identitetstjänst** används för att skapa ett gemensamt identifieringsramverk för bastjänsterna, lösningarna, kundattributen och målgrupperna i bastjänsten för Experience Cloud. Det fungerar genom att tilldela ett unikt, beständigt ID till en besökare. När din organisation implementerar ID-tjänsten kan du med detta ID identifiera samma besökare och deras data i olika Experience Cloud-lösningar.

![ID-tjänstgrafik](assets/mc_id_service_graphic.png)

ID-tjänsten kan även ersätta olika lösningsspecifika ID:n (till exempel Analytics AID). Via [Kund-ID och autentiseringstillstånd](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) kan du med ID-tjänsten skicka dina egna kund-ID:n till Experience Cloud. Tänk dock på att ID-tjänsten bara fungerar med de lösningar som du redan har prenumererat på. Om du inte är registrerad för åtkomst till andra produkter ger ID-tjänsten inte åtkomst.

ID-tjänsten är en integrerad komponent i många Experience Cloud-funktioner, förbättringar och tjänster. För närvarande stöder ID-tjänsten [Analyser,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) och [Mål.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

Om du inte har implementerat ID-tjänsten är det dags att börja fundera på en migreringsstrategi nu. Mer information om ID-tjänstens betydelse och roll finns i [Varför identitetstjänsten ska finnas på din radardator.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

Mer information om Experience Cloud-ID finns i [Experience Cloud ID - översikt](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) och [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html).

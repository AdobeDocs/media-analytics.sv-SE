---
title: Läs om förutsättningarna för Adobe direktuppspelningstjänster
description: Kom igång med direktuppspelande medietjänster. Lär dig vad du behöver för implementering.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Streaming Media, Workspace Basics"
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Förutsättningar {#prerequisites}

Innan du börjar implementera Adobe direktuppspelande medietjänster utför du följande uppgifter:

1. **Granska översikten över Adobe tjänster för direktuppspelning av media**<br>
Innan du börjar implementera direktuppspelande medietjänster ska du kontrollera att [Adobe översikt över direktuppspelande medietjänster](/help/media-overview.md) uppfyller dina behov.

1. **Bekräfta din prismodell**<br>
Den aktuella prismodellen för tillägget Customer Journey Analytics Streaming Media Collection och Adobe Analytics for Streaming Media Add-on baseras på videoströmmar. Kontakta vid behov din säljare eller Adobe Account Team eftersom tillägget säljs separat för Adobe Analytics och Adobe Experience Platform.

1. **Aktivera Adobe Analytics-rapporter**<br>
Om du vill aktivera rapporter i Analytics eller Customer Journey Analytics och visa innehåll och annonsuppgifter som du samlar in måste du aktivera rapporter. Se [Aktivera medierapporter](/help/reporting/media-reports-enable.md).

1. **Implementera Adobe Experience Platform Identity Service i Experience Cloud**

   **Identitetstjänsten** aktiverar det gemensamma identifieringsramverket för Experience Cloud Core Services, lösningar, kundattribut och målgrupper i People Core-tjänsten. Det fungerar genom att tilldela ett unikt, beständigt ID till en besökare. När din organisation implementerar ID-tjänsten kan du med detta ID identifiera samma besökare och deras data i olika Experience Cloud-lösningar.

   ![ID-tjänstgrafik](assets/mc_id_service_graphic.png)

   ID-tjänsten kan även ersätta olika lösningsspecifika ID:n (till exempel Analytics AID). Genom funktionen [Kund-ID:n och autentiseringstillstånd](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=sv-SE) kan du med ID-tjänsten skicka dina egna kund-ID:n till Experience Cloud. Tänk dock på att ID-tjänsten bara fungerar med de lösningar som du redan har prenumererat på. Om du inte är registrerad för åtkomst till andra produkter ger ID-tjänsten inte åtkomst.

   ID-tjänsten är en integrerad komponent i många av Experience Cloud funktioner, förbättringar och tjänster. För närvarande stöder ID-tjänsten [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) och [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   Om du inte har implementerat ID-tjänsten är det dags att börja fundera på en migreringsstrategi nu. Mer information om ID-tjänstens betydelse och roll finns i [Varför identitetstjänsten ska finnas på din radarr.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Mer information om Experience Cloud-id finns i [Översikt över Experience Cloud-id](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=sv-SE) och [Adobe Experience Platform-identitetstjänst](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=sv-SE).

1. **Visa ytterligare krav för din implementeringsmetod**

   Beroende på hur du planerar att implementera direktuppspelande medietjänster kan du se förutsättningarna för någon av följande implementeringsmetoder:

   * [Förutsättningar för implementering av endast Adobe Analytics](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Krav för Edge-implementeringar](/help/implementation/edge/prerequisites-edge.md)

   Använd [Implementeringsöversikten](/help/implementation/overview.md) för att avgöra vilken implementeringsmetod som är rätt för dig.

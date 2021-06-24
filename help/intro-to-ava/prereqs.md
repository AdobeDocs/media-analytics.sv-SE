---
title: Läs om krav för direktuppspelande media
description: Kom igång med Adobe Analytics Streaming Media. Lär dig vad du behöver för att implementera Adobe Analytics för direktuppspelningsmedia.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: '"Media Analytics, System Requirements"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Förutsättningar{#prerequisites}

## Beslut {#decision}

Innan du börjar spåra implementeringen har du några tidiga beslut att fatta om vilken implementering som passar bäst för din situation:

* **Media Analytics -** Använda de senaste Media SDK:erna (standard, rekommenderad implementering) och/eller Media Collection API (RESTful)
* **Milstolpe -** Den äldre Adobe-spårningsimplementeringen
* **API:er för datainfogning -** Implementera spårning utan att använda Media SDK:er

## Uppgifter {#prereq-tasks}

För en *Media Analytics*-implementering måste du utföra följande uppgifter innan du börjar:

1. **Aktivera Experience Cloud.**

   Du måste implementera Adobe Experience Platform Identity Service.

   Identitetstjänsten utgör det gemensamma ramverket för identifiering av bastjänsterna, lösningar, kundattribut och målgrupper i Experience Cloud bastjänsten. Det fungerar genom att tilldela ett unikt, beständigt ID till en besökare. När din organisation implementerar ID-tjänsten kan du med detta ID identifiera samma besökare och deras data i olika Experience Cloud-lösningar.

   ![](assets/mc_id_service_graphic.png)

   ID-tjänsten kan även ersätta olika lösningsspecifika ID:n (till exempel Analytics AID). Genom funktionen [Kund-ID:n och autentiseringstillstånd](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) kan ID-tjänsten skicka dina egna kund-ID:n till Experience Cloud. Tänk dock på att ID-tjänsten bara fungerar med de lösningar som du redan har prenumererat på. Om du inte är registrerad för åtkomst till andra produkter ger ID-tjänsten inte åtkomst.

   I framtiden är ID-tjänsten en integrerad komponent i många nuvarande och framtida funktioner, förbättringar och tjänster för Experience Cloud. För närvarande stöder ID-tjänsten [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) och [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >För att kunna delta i Adobe Experience Cloud Device Co-op krävs tjänsten Experience Cloud ID.

   Om du inte har implementerat ID-tjänsten är det dags att börja fundera på en migreringsstrategi nu. Mer information om ID-tjänstens betydelse och roll finns i [Varför identitetstjänsten ska finnas på din radarr.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Mer information om Experience Cloud ID finns i [Översikt över Experience Cloud ID,](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) och [Adobe Experience Platform identitetstjänst](https://experienceleague.adobe.com/docs/id-service/using/home.html).

1. **Aktivera Adobe Analytics-rapporter.**

   Information om hur du aktiverar rapporter i Analytics och ser innehåll och annonser som du samlar in finns i [Aktivera medierapporter.](/help/media-reports/media-reports-enable.md)

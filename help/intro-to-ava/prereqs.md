---
title: Förutsättningar
description: null
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Förutsättningar{#prerequisites}

## Beslut {#decision}

Innan du börjar spåra implementeringen har du några tidiga beslut att fatta om vilken implementering som passar bäst för din situation:

* **Media Analytics -** Använda de senaste SDK:erna (standard, rekommenderad implementering) och/eller API:t för Media Collection (RESTful)
* **Milstolpe -** Den äldre Adobe-spårningsimplementeringen
* **API:er för datainfogning -** Implementera spårning utan att använda Media SDK:er

## Uppgifter {#prereq-tasks}

För en implementering av *Media Analytics* måste du utföra följande uppgifter innan du börjar:

1. **Aktivera Experience Cloud.**

   Ni måste implementera Adobe Experience Platform Identity Service.

   Identitetstjänsten möjliggör det gemensamma identifieringsramverket för Experience Cloud-bastjänsterna, lösningar, kundattribut och målgrupper i bastjänsten för människor. Det fungerar genom att tilldela ett unikt, beständigt ID till en besökare. När din organisation implementerar ID-tjänsten kan du med det här ID:t identifiera samma webbplatsbesökare och deras data i olika Experience Cloud-lösningar.

   ![](assets/mc_id_service_graphic.png)

   ID-tjänsten kan även ersätta olika lösningsspecifika ID:n (till exempel Analytics AID). Genom funktionerna [Kund-ID:n och Autentiseringstillstånd](https://docs.adobe.com/content/help/en/id-service/using/reference/authenticated-state.html) kan du med ID-tjänsten skicka dina egna kund-ID:n till Experience Cloud. Tänk dock på att ID-tjänsten bara fungerar med de lösningar som du redan har prenumererat på. Om du inte är registrerad för åtkomst till andra produkter ger ID-tjänsten inte åtkomst.

   Framöver är ID-tjänsten en integrerad komponent i många aktuella och framtida Experience Cloud-funktioner, förbättringar och tjänster. För närvarande stöder ID-tjänsten [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager](https://www.adobe.com/marketing-cloud/data-management-platform.html) och [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >För att kunna delta i Adobe Experience Cloud Device Co-op krävs Experience Cloud ID-tjänsten.

   Om du inte har implementerat ID-tjänsten är det dags att börja fundera på en migreringsstrategi nu. Mer information om ID-tjänstens betydelse och roll finns i [Varför identitetstjänsten ska finnas på din radarr.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >Om det inte finns någon information om användar-ID för de mediespecifika anropen gäller standardmetoderna [för](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) Fallback-ID för analyser.

   Mer information om Experience Cloud ID finns i Översikt över [Experience Cloud ID,](https://docs.adobe.com/content/help/en/id-service/using/intro/overview.html) och [Adobe Experience Platform Identity Service.](https://docs.adobe.com/content/help/en/id-service/using/home.html)

1. **Aktivera Adobe Analytics-rapporter.**

   Information om hur du aktiverar rapporter i Analytics och ser innehållet och annonsen som du samlar in finns i Aktivera [medierapporter.](/help/media-reports/media-reports-enable.md)


---
title: Läs om kraven för Adobe Streaming Media Collection
description: Kom igång med Streaming Media Collection. Lär dig vad du behöver för implementering.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Förutsättningar {#prerequisites}

Innan du börjar implementera Adobe Streaming Media Collection utför du följande uppgifter:

1. **Granska översikten över den direktuppspelade mediesamlingen**<br>
Innan du börjar implementera Streaming Media Collection bör du kontrollera att [ Streaming Media Collection-översikten ](/help/media-overview.md) uppfyller dina behov.

1. **Bekräfta din prismodell**<br>
Den aktuella prismodellen för tillägget Adobe Streaming Media Collection baseras på videoströmmar. Kontakta vid behov din försäljningsrepresentant eller kontoteamet på Adobe eftersom tillägget säljs separat för Adobe Analytics och Adobe Experience Platform.

1. **Aktivera Adobe Analytics-rapporter**<br>
Om du vill aktivera rapporter i Analytics eller Customer Journey Analytics och visa innehåll och annonsuppgifter som du samlar in måste du aktivera rapporter. Se [Aktivera medierapporter](/help/reporting/media-reports-enable.md).

1. **Implementera Adobe Experience Platform Identity Service i Experience Cloud**

   **Identitetstjänsten** aktiverar det gemensamma identifieringsramverket för bastjänsterna, lösningarna, kundattributen och målgrupperna i huvudtjänsten Experience Cloud. Det fungerar genom att tilldela ett unikt, beständigt ID till en besökare. När din organisation implementerar ID-tjänsten kan du med detta ID identifiera samma besökare och deras data i olika Experience Cloud-lösningar.

   ![ID-tjänstgrafik](assets/mc_id_service_graphic.png)

   ID-tjänsten kan även ersätta olika lösningsspecifika ID:n (till exempel Analytics AID). Genom funktionen [Kund-ID:n och autentiseringstillstånd](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=sv-SE) kan du med ID-tjänsten skicka dina egna kund-ID:n till Experience Cloud. Tänk dock på att ID-tjänsten bara fungerar med de lösningar som du redan har prenumererat på. Om du inte är registrerad för åtkomst till andra produkter ger ID-tjänsten inte åtkomst.

   ID-tjänsten är en integrerad komponent i många Experience Cloud-funktioner, förbättringar och tjänster. För närvarande stöder ID-tjänsten [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) och [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   Om du inte har implementerat ID-tjänsten är det dags att börja fundera på en migreringsstrategi nu. Mer information om ID-tjänstens betydelse och roll finns i [Varför identitetstjänsten ska finnas på din radarr.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Mer information om Experience Cloud ID finns i [Översikt över Experience Cloud ID,](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=sv-SE) och [Adobe Experience Platform identitetstjänst](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=sv-SE).

1. **Visa ytterligare krav för din implementeringsmetod**

   Beroende på hur du tänker implementera Streaming Media Collection kan du se förutsättningarna för någon av följande implementeringsmetoder:

   * [Förutsättningar för implementering av endast Adobe Analytics](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Krav för Edge-implementeringar](/help/implementation/edge/prerequisites-edge.md)

   Använd [Implementeringsöversikten](/help/implementation/overview.md) för att avgöra vilken implementeringsmetod som är rätt för dig.

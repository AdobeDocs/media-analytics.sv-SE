---
title: Konfigurera en mobil SDK med taggar för direktuppspelningsmedia
description: Lär dig hur du implementerar Adobe Streaming Media för mobilappar.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Installera SDK för mobiler {#install-mobile-sdks}

Installera och konfigurera följande för att implementera direktuppspelningsmedia för mobilappar på Android eller iOS:

* **Adobe Experience Platform Mobile SDK**

   Om du vill samla in data använder du Taggar i Adobe Experience Platform. Taggar i Adobe Experience Platform är en tagghanteringslösning som gör att ni kan driftsätta Analytics-kod tillsammans med andra taggningskrav.

* **Media SDK för Android** eller **Media SDK för iOS**

* **Adobe Media Analytics för ljud- och videotillägg**

Information om hur du hämtar SDK:er och om du vill ha ytterligare dokumentationsresurser finns i [Hämta SDK:er för media, tillägg med hjälp av taggar och OTT SDK:er](/help/getting-started/download-sdks.md)

* **Hämta giltiga konfigurationsparametrar**

   Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.

* **Inkludera följande API:er i mediespelaren**

   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.

   * *Ett API som tillhandahåller spelarinformation* - Detta innehåller information om hur medienamnet spelas upp, spelhuvudet, annonser eller kapitel.

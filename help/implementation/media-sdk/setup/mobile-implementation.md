---
title: Konfigurera en mobil SDK med taggar för direktuppspelningsmedia
description: Lär dig hur du implementerar Adobe Streaming Media för mobilappar.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Installera SDK för mobiler {#install-mobile-sdks}

Installera och konfigurera följande för att implementera Streaming Media Collection-tillägget för mobilappar i Android eller iOS:

* **Adobe Experience Platform Mobile SDK**

  Använd något av följande för att samla in data:
   * Taggar i Adobe Experience Platform. Taggar i Adobe Experience Platform är en tagghanteringslösning som gör att ni kan driftsätta Analytics-kod tillsammans med andra taggningskrav.
   * Adobe Experience Platform Edge

* **Media SDK för Android** eller **Media SDK för iOS**

* **Adobe Media Analytics för ljud- och videotillägg**

Om du vill hämta SDK:er och om du vill ha mer dokumentation läser du [Hämta SDK:er för media, tillägg med hjälp av taggar och OTT SDK:er](/help/getting-started/download-sdks.md)

* **Hämta giltiga konfigurationsparametrar**

  Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.

* **Ta med följande API:er i mediespelaren**

   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.

   * *Ett API som innehåller spelarinformation* - Detta innehåller information om uppspelning, t.ex. medienamn, spelhuvudets position, annonser eller kapitel.

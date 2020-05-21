---
title: Mätningsalternativ
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 967a126723ebbbe02097bd07edc2ed967cd35f4c
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 3%

---


# Measurement options{#measurement-options}

Du kan aktivera ljud- och videospårning med Adobe Launch med Adobe Media Analytics-tillägget, Media SDK eller Media Collection API.

## Adobe Launch med Adobe Media Analytics-tillägget

Adobe Launch är nästa generations tagghanteringslösning från Adobe. Launch är ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser. Om du vill skapa och underhålla egna integreringar med Launch använder du tillägg. Ett tillägg är ett JavaScript-, HTML- och CSS-paket som utökar startgränssnittet och klientfunktionerna. Mer information finns i användarhandboken för [Experience Platform Launch](https://docs.adobe.com/content/help/en/launch/using/overview.html)

Adobe Media Analytics-tillägget (MA) lägger till JavaScript Media SDK (Media 2.x SDK) för ljud och video. Det här tillägget innehåller funktioner för att lägga till spårningsinstansen till en startwebbplats eller ett startprojekt. `MediaHeartbeat`

Adobe Launch med Media Analytics-tillägget kräver följande:
* Du måste vara en Adobe Experience Cloud-kund.
* Du måste distribuera Launch- eller DTM-inbäddningskoden på dina webbsidor.
* [Analystillägg](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID-tillägg](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Media SDK kan integreras med de vanligaste mediespelarna.

## Media Collection API (RESTful API)

Integreras med spelare utan SDK-stöd eller när SDK-integrering inte behövs.<br>Från och med version 2.2.0 har SDK:er för videomaterial (VHL) bytt namn till SDK:er för mediemäsning som stöder ljud- och videospårning. Media 2.2.0 SDK är helt bakåtkompatibelt med VHL 2.x SDK-serien. Namnändringen är bara en ändring av namnkonventionen och representerar inte funktionsändringar.

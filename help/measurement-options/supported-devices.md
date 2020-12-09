---
title: Enheter och plattformar som stöds
description: Adobe Analytics for Streaming Media ser till att alla medieströmmar samlas in och rapporteras på alla enheter.
translation-type: tm+mt
source-git-commit: dfffcf1e1d815ca178e0bdba881d973d60fe1631
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 19%

---


# Enheter och plattformar som stöds {#devices-supported}

>[!IMPORTANT]
>
>När stödet för version 4 Mobile SDK upphör den 31 augusti 2021 upphör även stödet för Media Analytics SDK för iOS och Android i Adobe.  Mer information finns i [Vanliga frågor och svar om Media Analytics SDK när support upphör](/help/sdk-implement/end-of-support-faqs.md).

Adobe Analytics for Streaming Media har stöd för alla större enheter:

* iOS- och Android-smartphones och surfplattor
* OTT-enheter för ROKU, AppleTV, FireTV och Android TV
* JavaScript-webbläsare för stationära och bärbara datorer

SDK:n för media uppdateras regelbundet när nya versioner av enheter släpps och du kan använda SDK för att integrera med de största mediespelarna idag, inklusive Brightcove och Oyala.

För enheter och plattformar som för närvarande inte har SDK-stöd eller i situationer där du inte vill använda en SDK kan du implementera API:t för Media Collection. Med Media Collection API kan du göra RESTful API-anrop direkt från en enhet eller plattform till Media Analytics-backend.

Tabellen nedan visar vilka enheter och plattformar som stöds. Information om hur du hämtar den senaste SDK-versionen finns i [Hämta SDK:er](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html). Om en enhet inte finns med i listan kontaktar du kundtjänst eller lösningskonsult för att få information om enhetens status.

| Strömmande plattformar och enheter |  | Media Launch Extension med AEP Mobile SDK | Media SDK | Media Collection API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Webb/mobil |  |  |  |  |
|  | JavaScript-webbläsare | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| Mobilapp |  |  |  |  |
|  | iOS-enheter | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>3</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android-enheter | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>3</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows-enheter |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV (tvOS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>3</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>(inbyggt) |
|  | Fire TV (Fire OS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>3</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>3</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | Spelkonsoler (t.ex. Xbox ONE, Sony PS3/PS4) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Ange övre rutor (t.ex. xfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Smarta TV-apparater (t.ex. Samsung, LG, Sony, Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(webbaserad)    | ![](/help/assets/icon-blue-check.png) |
| Övriga |  |  |  |  |
|  | Nya anslutna enheter |  |  | ![](/help/assets/icon-blue-check.png) |

1. Stödet för dessa SDK upphör den 31 augusti 2021. Mer information finns i [Vanliga frågor och svar om Media Analytics SDK när support upphör](/help/sdk-implement/end-of-support-faqs.md).

Mer information om vilka plattformsversioner som minst stöds för varje SDK finns i [Stöd för minimiplattformsversion](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/setup/setup-overview.html)

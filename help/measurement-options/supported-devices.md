---
title: Enheter som stöds
description: null
uuid: null
translation-type: tm+mt
source-git-commit: c86c7932f932af0a121e0b757921973d6f4084e8

---


# Enheter som stöds {#devices-supported}

Adobe Analytics för ljud och video ser till att alla medieströmmar samlas in och rapporteras på alla enheter.

Adobe Analytics for Audio and Video har stöd för alla större enheter:

* iOS- och Android-smartphones och surfplattor
* OTT-enheter för ROKU, AppleTV, FireTV och Android TV
* JavaScript-webbläsare för stationära och bärbara datorer

Media SDK uppdateras regelbundet när nya versioner av enheter släpps och du kan använda SDK för att integrera med de största mediespelarna idag, inklusive Brightcove och Ooyala.

För enheter och plattformar som för närvarande inte har SDK-stöd eller i situationer där du inte vill använda en SDK kan du implementera API:t för Media Collection. Med Media Collection API kan du göra RESTful API-anrop direkt från en enhet eller plattform till Media Analytics-backend.

Tabellen nedan visar de enheter som stöds för närvarande. Information om hur du hämtar den senaste SDK-versionen finns i [Hämta SDK:er](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html). Om en enhet inte finns med i listan kontaktar du kundtjänst eller lösningskonsult för att få information om enhetens status.


| Strömningsplattform/enhet |  | Media Launch Extension med AEP SDK | Media SDK | Media Collection API |
|---------------------------|-----------------------------------------------|:----------------------------:|:-------------------:|:--------------------:|
| Webb/mobil |  |  |  |  |
|  | JavaScript-webbläsare | X | X | X |
| Mobilapp |  |  |  |  |
|  | iOS-enheter | X | X | X |
|  | Android-enheter | X | X | X |
|  | Windows-enheter |  |  | X |
| OTT |  |  |  |  |
|  | Apple TV (Legacy, TVOS) |  | X | X |
|  | ROKU |  | X<br>(BrightScript) | X<br>(inbyggd) |
|  | Fire TV (Fire OS) |  | X | X |
|  | Android TV |  | X | X |
|  | Chromecast |  | X | X |
|  | Spelkonsoler (t.ex. Xbox ONE, Sony PS3/PS4) |  |  | X |
|  | Ange övre rutor (t.ex. xfinity X1) |  |  | X |
|  | Smarta TV-apparater (t.ex. Samsung, LG, Sony, Vizio) |  | X<br>(webbaserad) | X |
| Övriga |  |  |  |  |
|  | Nya anslutna enheter |  |  | X |


För Media SDK, se även [Stöd för lägsta plattformsversion](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

---
title: Nyheter i Media Analytics
description: Nyheter innehåller information om nya funktioner och meddelanden.
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 24%

---


# Nyheter i medieanalys{#whats-new}

![Banderoll](assets/media_analytics_banner.png)


Den här sidan beskriver nya funktioner, korrigeringar och viktiga meddelanden i Media Analytics. Här finns också ny dokumentation, kurser och videokurser som hjälper er att få ut mesta möjliga av Media Analytics.


## Versionsinformation

Versionsinformation om Adobe Experience Cloud

Versionsinformationen för Adobe Experience Cloud beskriver nya funktioner, korrigeringar och viktiga meddelanden i Adobe Experience Cloud. Detta inkluderar de senaste ändringarna av Media Analytics. Här finns också ny dokumentation, kurser och videokurser som hjälper dig att få ut mesta möjliga av Experience Cloud.

## Nya funktioner

| Funktion | [Allmän tillgänglighet](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html) – Måldatum | Beskrivning |
| ----------- | ---------- | ---------- |
| [Media Concurrent Viewer-panel](media-reports/media-workspace-panels/media-concurrent-viewers.md) | 17 september 2020 | På panelen Medievisningsprogram för samtidig användning i Workspace kan du förstå var maximal samtidighet inträffar eller var bortfall inträffar. Det ger värdefull insikt i innehållets kvalitet och tittarengagemanget och hjälper till med felsökning eller planering av volym/skala. |
| [Enheter och plattformar som stöds](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 18 juni 2020 | [!UICONTROL Media Launch Extension] med AEP Mobile SDK har nu stöd för följande OTT-enheter:<ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul> |
| [Spårning av spelarens tillstånd](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/player-state-overview.html) | 29 maj 2020 | [!UICONTROL Media Analytics]-kunder kan samla in tittarinteraktioner under uppspelning med en standarduppsättning lösningsvariabler för helskärmsvisning, undertexter, ljud av, bild-i-bild och i fokus. Du kan också skapa anpassade spelarlägen. [!UICONTROL Player State Tracking] variabler är nu tillgängliga för rapportering i [!UICONTROL Analysis Workspace]. Den här funktionen kräver något av följande: <ul><li>Media [!DNL JavaScript] SDK 3.0 eller senare</li><li>För användning med [!DNL Adobe Experience Platform] (AEP) SDK:</li><li>[!UICONTROL Media Analytics Extension] (för webb): [!UICONTROL Adobe Media Analytics] (3.x SDK) för ljud och video v1.0 eller senare</li><li>[!UICONTROL Media Analytics Extension] (för mobil): [!UICONTROL Adobe Media Analytics for Audio] och video v2.0 eller senare</li><li>[!UICONTROL Media Collection]</li></ul> |


## Viktiga meddelanden

| Funktion | [Allmän tillgänglighet](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html) – Måldatum | Beskrivning |
| ----------- | ---------- | ---------- |
| [Enheter och plattformar som stöds](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 31 augusti 2021 | När stödet för version 4 Mobile SDK upphör den 31 augusti 2021 upphör även stödet för Media Analytics SDK för iOS och Android i Adobe. Mer information finns i Vanliga frågor om supporten för Media Analytics SDK. |
| [Vanliga frågor om supporten för Media Analytics SDK](sdk-implement/end-of-support-faqs.md) | Hösten 2019 | Funktionsutvecklingen tog slut för Media Analytics SDK:er för iOS och Android.  Nya funktioner som introducerades från och med hösten 2019 aktiveras med Media Analytics-tilläggen och Media Collection API. |
| [Medieöversikt](media-overview.md) | 20 februari 2019 | Adobe har endast stöd för TLS 1.1 eller senare. Den här ändringen innebär att Adobe inte längre samlar in data från slutanvändare med äldre enheter eller webbläsare som distribuerar TLS 1.0. |
| [Enheter och plattformar som stöds](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 19 februari 2019 | De plattformsversioner som minst stöds för varje SDK anges nedan. <br>- iOS: iOS 6+  <br>- Android: Android 5.0+ - Lollipop  <br>- Chrome: v22+<br>- Mozilla: v27+<br>- Safari: v7+<br>- IE: v1+ |
| [Parametrar för ljud och video](metrics-and-metadata/audio-video-parameters.md) | 7 februari 2019 | Adobe Analytics for Video and Audio släppte en namnändring. <i>Medieinitierarna </i> kallas nu  <i>Media Starts</i>. Denna ändring gjordes för att återspegla branschstandarder i mätvärden och rapporter och för att göra mätvärdena lätt att identifiera vid rapportering. |
| [Parametrar för ljud och video](metrics-and-metadata/audio-video-parameters.md) | 13 september 2018 | Etiketterna för vissa dimensioner, mätvärden och rapporter har ändrats för att möjliggöra spårning av videoinnehåll och ljudanalys. Etiketterna som har ändrats är: *videon initierar* till *media initierar*, *videolängd* till *innehållslängd* och *videonamn* till *innehållsnamn*. Videorapporter i Reports and Analytics har uppdaterats för att använda namnet&quot;Media&quot; i stället för&quot;Video&quot;. Etikettändringarna ändrade inte datainsamling eller historikdata. Observera dessa ändringar om du använder dem i Report Builder eller i andra externa automatiserade datatunkter som kan påverkas av ändringen. |




<!-- | title | date | description | -->

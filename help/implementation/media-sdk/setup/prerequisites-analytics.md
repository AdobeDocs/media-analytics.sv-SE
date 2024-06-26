---
title: Förutsättningar för implementering av endast Adobe Analytics
description: Lär dig om förutsättningarna för att använda tillägget Streaming Media Collection med implementeringar som endast gäller för Adobe Analytics
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Förutsättningar för implementering av endast Adobe Analytics

De krav som beskrivs i det här avsnittet är specifika för implementering av tillägget Streaming Media Collection med enbart Adobe-Analytics (när inte Edge används).

1. **Slutför de allmänna kraven**<br>
Oavsett om du implementerar tillägget Streaming Media Collection för Adobe Analytics eller för Edge måste du se till att du uppfyller [allmänna krav](/help/getting-started/prereqs.md).

1. **Bekräfta att du har en Adobe Analytics-implementering**<br>
När du implementerar tillägget Streaming Media Collection med en implementering som bara innehåller analyser krävs även en grundläggande Adobe Analytics-implementering. Se [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) för mer information.

1. **Hämta URL:en för mediespårningsservern**<br>
Be din Adobe Analytics-representant om URL:en för mediespårningsservern. Det här är `collection-api-server` URL för Mobile SDK, JavaScript SDK och spårningsservern utan samling-api för Roku. Domännamn för API-implementering är: `[your_namespace].hb-api.omtrdc.net`.

1. **Hämta aktuell Media SDK eller implementera nödvändiga tillägg**<br>
Beroende på implementeringsvägen, [ladda ned aktuell SDK](/help/getting-started/download-sdks.md) för webb, mobiler och plattformar som ligger ovanpå varandra. De tillägg som krävs måste implementeras för att aktivera tilläggssökvägarna för Streaming Media Collection.

1. **Aktivera Adobe Analytics-rapporter**<br>
Om du vill aktivera rapporter i Analytics och visa innehåll och annonsuppgifter som du samlar in måste du aktivera rapporter i Analytics. Se [Aktivera medierapporter](/help/reporting/media-reports-enable.md).

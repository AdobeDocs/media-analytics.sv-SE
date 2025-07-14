---
title: Förutsättningar för implementering av endast Adobe Analytics
description: Lär dig om förutsättningarna för att använda Streaming Media Collection med Adobe Analytics-implementeringar
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0b0b4a373b15191dcb37dc436413f68cdc70768e
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Förutsättningar för implementering av endast Adobe Analytics

De krav som beskrivs i det här avsnittet är specifika för implementering av Streaming Media Collection med implementeringar som bara innehåller Adobe-Analytics (när Edge inte används).

1. **Slutför de allmänna kraven**<br>
Oavsett om du implementerar Streaming Media Collection för implementeringar av endast Adobe Analytics eller för Edge måste du se till att du uppfyller de [allmänna kraven ](/help/getting-started/prereqs.md) .

1. **Bekräfta att du har en Adobe Analytics-implementering**<br>
Vid implementering av Streaming Media Collection med en implementation med enbart Analytics krävs också en grundläggande Adobe Analytics-implementering. Mer information finns i [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

1. **Hämta URL:en för mediespårningsservern**<br>
Be din Adobe Analytics-representant om URL:en för mediespårningsservern. Det här är `collection-api-server`-URL:en för Mobile SDK, JavaScript SDK och den icke-samlings-API-spårningsservern för Roku. Domännamn för API-implementering är: `[your_namespace].hb-api.omtrdc.net`.

1. **Hämta det aktuella SDK-mediet eller implementera de nödvändiga tilläggen**<br>
Beroende på implementeringsvägen kan du [hämta den aktuella SDK ](/help/getting-started/download-sdks.md) för webben, mobiler eller toppmoderna plattformar. De tillägg som krävs måste implementeras för att aktivera sökvägarna för tilläggen för Streaming Media Collection.

1. **Aktivera Adobe Analytics-rapporter**<br>
Om du vill aktivera rapporter i Analytics och visa innehåll och annonsuppgifter som du samlar in måste du aktivera rapporter i Analytics. Se [Aktivera medierapporter](/help/reporting/media-reports-enable.md).

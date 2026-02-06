---
title: Förutsättningar för implementering av endast Adobe Analytics
description: Lär dig om förutsättningarna för att använda Adobe Analytics for Streaming Media Add-on för Adobe Analytics-implementeringar
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Förutsättningar för implementering av endast Adobe Analytics

De krav som beskrivs i det här avsnittet är specifika för implementering av Adobe Analytics for Streaming Media Add-on för Adobe-Analytics-implementeringar (när Edge inte används).

1. **Slutför de allmänna kraven**<br>
Oavsett om du implementerar direktuppspelningstjänster för implementeringar av endast Adobe Analytics eller för Edge måste du se till att du uppfyller de [allmänna kraven ](/help/getting-started/prereqs.md) .

1. **Bekräfta att du har en Adobe Analytics-implementering**<br>
När du implementerar Adobe Analytics for Streaming Media Add-on för en implementering som bara innehåller analyser krävs också en grundläggande Adobe Analytics-implementering. Mer information finns i [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

1. **Hämta URL:en för mediespårningsservern**<br>
Be din Adobe Analytics-representant om URL:en för mediespårningsservern. Det här är `collection-api-server`-URL:en för Mobile SDK, JavaScript SDK och den icke-samlings-API-spårningsservern för Roku. Domännamn för API-implementering är: `[your_namespace].hb-api.omtrdc.net`.

1. **Hämta det aktuella SDK-mediet eller implementera de nödvändiga tilläggen**<br>
Beroende på implementeringsvägen kan du [hämta den aktuella SDK ](/help/getting-started/download-sdks.md) för webben, mobiler eller toppmoderna plattformar. De tillägg som krävs måste implementeras för att Adobe Analytics for Streaming Media Add-on ska kunna aktiveras.

1. **Aktivera Adobe Analytics-rapporter**<br>
Om du vill aktivera rapporter i Analytics och visa innehåll och annonsuppgifter som du samlar in måste du aktivera rapporter i Analytics. Se [Aktivera medierapporter](/help/reporting/media-reports-enable.md).

---
title: Förutsättningar för implementering av endast Adobe Analytics
description: Lär dig om förutsättningarna för att använda direktuppspelningsmedia med implementeringar som endast är för Adobe Analytics
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: c4d058ee82f4995f42bfe21c0442004f1f7ea4af
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# Förutsättningar för implementering av endast Adobe Analytics

De krav som beskrivs i det här avsnittet är specifika för implementering av direktuppspelningsmedia med implementeringar enbart för Adobe-analys (när Edge inte används).

1. **Slutför de allmänna kraven**<br>
Oavsett om du implementerar Streaming Media för implementeringar av endast Adobe Analytics eller för Edge-implementeringar måste du se till att du uppfyller [allmänna krav](/help/getting-started/prereqs.md).

1. **Bekräfta att du har en Adobe Analytics-implementering**<br>
Vid implementering av Streaming Media med en implementation med enbart Analytics krävs också en grundläggande Adobe Analytics-implementering. Se [Implementera Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) för mer information.

1. **Hämta URL:en för mediespårningsservern**<br>
Be din Adobe Analytics-representant om URL:en för mediespårningsservern. Det här är `collection-api-server` URL för Mobile SDK, JavaScript SDK och spårningsservern utan samlings-api för Roku. Domännamn för API-implementering är: `[your_namespace].hb-api.omtrdc.net`.

1. **Hämta aktuell Media SDK eller implementera nödvändiga tillägg**<br>
Beroende på implementeringsvägen, [ladda ned aktuell SDK](/help/getting-started/download-sdks.md) för webb, mobiler och plattformar som ligger ovanpå varandra. De tillägg som krävs måste implementeras för att Adobe Analytics ska kunna aktiveras för sökvägar för medietillägg för direktuppspelning.

1. **Aktivera Adobe Analytics-rapporter**<br>
Om du vill aktivera rapporter i Analytics och visa innehåll och annonsuppgifter som du samlar in måste du aktivera rapporter i Analytics. Se [Aktivera medierapporter](/help/reporting/media-reports-enable.md).

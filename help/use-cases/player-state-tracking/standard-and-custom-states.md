---
title: Om standardlägen och anpassade lägen
description: Läs om funktionen för spårning av spelartillstånd, inklusive krav och riktlinjer för implementering och rapportering av standardlägen och anpassade spelarlägen.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Om standardlägen och anpassade lägen

Fem standardspelarlägen är tillgängliga och du kan lägga till egna anpassade lägen.

| Standardlägesnamn | Konstanten Media SDK | API-namn för mediesamling |
|-----------------------|------------------------------------------|-----------------------------|
| Helskärm | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Undertexter | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Ljud | `ADB.Media.PlayerState.Mute` | `mute` |
| Bild-i-bild | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| I fokus | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Data beräknas på samma sätt för standardtillstånd och anpassade tillstånd, men data lagras på olika sätt för Analytics-rapportering.

**För standardlägen** - När du aktiverar spårning av spelartillstånd från Media Management-konsolen i Analytics-rapporter (admin-sidan) är 15 lösningsvariabler tillgängliga för rapportering och dataexport.

**För anpassade lägen** - Du kan skapa egna bearbetningsregler för att lagra beräknade värden i anpassade händelser och sedan använda dessa regler för rapportering och dataexport.

## Riktlinjer

* En videosession är begränsad till tio spelarlägen.
* Alla kombinationer av lägen är tillåtna.
* Om flera spelarlägen godkänns, behålls endast de första 10 och vidarebefordras nedströms till VA-bearbetningskomponenten.
* Maximalt 10 lägen tillämpas för alla lägen, oavsett om de är stängda eller inte.
* Ett läge kan starta och avslutas flera gånger och räknas som ett enda läge. `closedCapationing` kan till exempel startas och stoppas fem gånger, men räknas som ett enskilt tillstånd.
* Alla lägen som överskrider maxgränsen på 10 tillåtna lägen ignoreras.

## Anpassade lägen

Med möjligheten att skapa anpassade lägen kan du hämta anpassade åtgärder och uppdatera anpassade metadata under en uppspelningssession.

Mer information om hur du skapar anpassade lägen finns i [Referenshandboken för Media API: `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)

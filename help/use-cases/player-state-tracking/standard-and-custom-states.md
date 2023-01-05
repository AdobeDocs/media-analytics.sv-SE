---
title: Om standardlägen och anpassade lägen
description: Läs om funktionen för spårning av spelartillstånd, inklusive krav och riktlinjer för implementering och rapportering av standardlägen och anpassade spelarlägen.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Om standardlägen och anpassade lägen

Fem standardspelarlägen är tillgängliga och du kan lägga till egna anpassade lägen.

| Standardlägesnamn | Media SDK-konstant | API-namn för mediesamling |
|-----------------------|------------------------------------------|-----------------------------|
| Helskärm | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Undertexter | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Ljud av | `ADB.Media.PlayerState.Mute` | `mute` |
| Bild-i-bild | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| I fokus | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Data beräknas på samma sätt för standardtillstånd och anpassade tillstånd, men data lagras på olika sätt för Analytics-rapportering.

**För standardlägen**- När du aktiverar spårning av spelartillstånd från Media Management Console i Analytics-rapporter (admin-sidan) är 15 lösningsvariabler tillgängliga för rapportering och dataexport.

**För anpassade lägen**- Du kan skapa egna bearbetningsregler för att lagra beräknade värden i anpassade händelser och sedan använda dessa regler för rapportering och dataexport.

## Riktlinjer

* En videosession är begränsad till 10 spelarlägen.
* Alla kombinationer av lägen är tillåtna.
* Om flera spelarlägen godkänns, behålls endast de första 10 och vidarebefordras nedströms till VA-bearbetningskomponenten.
* Maximalt 10 lägen tillämpas för alla lägen, oavsett om de är stängda eller inte.
* Ett läge kan starta och avslutas flera gånger och räknas som ett enda läge. Till exempel: `closedCapationing` kan startas och stoppas fem gånger, men räknas som ett enskilt tillstånd.
* Alla lägen som överskrider maxgränsen på 10 tillåtna lägen ignoreras.

## Anpassade lägen

Med möjligheten att skapa anpassade lägen kan du hämta anpassade åtgärder och uppdatera anpassade metadata under en uppspelningssession.

Mer information om hur du skapar anpassade lägen finns i [Referenshandbok för Media-API: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
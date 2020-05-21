---
title: Om standardlägen och anpassade lägen
description: I det här avsnittet beskrivs funktionen för spårning av spelartillstånd, inklusive krav och riktlinjer för implementering och rapportering av standardlägen och anpassade spelarlägen.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '251'
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

* En videosession är begränsad till 10 unika anpassade spelarlägen.
* Om flera spelarlägen skickas behålls endast de första 10 och vidarebefordras nedströms till bearbetningskomponenten för VA(?videoanalys).
* Maximalt 10 lägen tillämpas för alla lägen, oavsett om de är stängda eller inte.
* Samma läge kan startas och avslutas ett valfritt antal gånger och räknas som ett enda läge.
* Alla tillstånd som överskrider det högsta tillåtna anpassade värdet? lägen (10) tas bort.

## Anpassade lägen

Med möjligheten att skapa anpassade lägen kan du hämta anpassade åtgärder och uppdatera anpassade metadata under en uppspelningssession.

Behöver mer information om anpassade lägen

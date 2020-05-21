---
title: Om Spårning av spelartillstånd
description: I det här avsnittet beskrivs funktionen för spårning av spelartillstånd, inklusive krav och riktlinjer för implementering och rapportering av spelarlägen.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---


# Om Spårning av spelartillstånd

För att optimera produktupplevelsen och öka värdet för ert företag är det viktigt att förstå kundbeteendet när ni tittar på videor. Detta inkluderar tiden som tillbringats i olika spelarlägen.  Och för att optimera förståelsen behöver ni flexibiliteten att skapa och mäta nya spelarlägen och händelser efter behov.

Med Spårning av spelarstatus kan du fånga upp visningsprogrammets interaktion under uppspelning med en standarduppsättning av lösningsvariabler för helskärmsläge, undertexter, ljud av, bild-i-bild och i fokus.  Spårning av spelarstatus ger även flexibilitet att skapa anpassade spelarlägen.  Och det finns variabler för spårning av spelartillstånd tillgängliga för rapportering på arbetsytan för analyser.

Om du vill hämta ändringar av spelarläget uppdaterar Player State Tracking metadata för videomätningen. Om du till exempel vill fastställa videoengagemanget&quot;true&quot; mäter Flash Player State Tracking den tid som spenderas med ljudet i stället för med passiva eller icke-aktiva videobilder när ljudet är avstängt eller den tid som spenderas i läget Normal jämfört med helskärm.

Spårning av spelarstatus ger följande fördelar:

* Tillhandahåller standardvariabler som mäter vanliga lägen, till exempel helskärmsläge eller undertextning
* Tillhandahåller anpassningsbara variabler för mätning av anpassade lägen under en uppspelningssession
* Mäter tid i ett anpassat spelarläge
* Mäter flera lägen som kan vara samtidigt

![Spårning av spelartillstånd](assets/player_state_tracking.png)

## Krav

Spårning av spelartillstånd kräver följande för Media Analytics-tillägg för användning med Adobe Experience Platform (AEP SDK):
* Webb: Adobe Media Analytics (3.x SDK) för ljud och video v1.0+
* Mobil: Adobe Media Analytics for Audio and Video v2.0+

Om du bestämmer dig för att inte använda AEP SDK kan du använda följande när du spårar spelarstatus:
* Media JS SDK 3.0+
* Media Collection API version?

## Riktlinjer

Innan du implementerar spårning av spelartillstånd bör du tänka på följande riktlinjer.

* Spelarläget beräknas för alla uppspelningslägen - (ingen delning)
* Du kan mäta flera spelarlägen samtidigt
* Det högsta antalet spelarlägen som kan spåras under en uppspelning är 10 
* Mätvärden för spelarstatus skickas till Analytics för att enbart rapportera om stängningsanropet för media
* Spelartillstånd hämtas för varje enskild uppspelningssession - spelarläget beräknas inte för alla uppspelningar 

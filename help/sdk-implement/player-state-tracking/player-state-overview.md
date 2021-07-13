---
title: Om Spårning av spelartillstånd
description: Läs mer om funktionen för spårning av spelartillstånd, inklusive krav och riktlinjer för implementering och rapportering av spelarlägen.
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Om Spårning av spelartillstånd

För att optimera produktupplevelsen och öka värdet för ert företag är det viktigt att förstå kundbeteendet när ni tittar på videor. Detta inkluderar tiden som tillbringats i olika spelarlägen.  Det är också viktigt att ha flexibiliteten att skapa och mäta nya spelarlägen och händelser efter behov.

Med Spårning av spelarstatus kan du fånga upp visningsprogrammets interaktion under uppspelning med en standarduppsättning av lösningsvariabler för helskärmsläge, undertexter, ljud av, bild-i-bild och fokus.  Spårning av spelarstatus ger även flexibilitet att skapa anpassade spelarlägen. Du kan använda variabler för spårning av spelartillstånd för rapportering i Analysis Workspace.

Om du vill hämta ändringar av spelarläget uppdaterar Player State Tracking metadata för videomätningen. Om du till exempel vill fastställa videoengagemanget&quot;true&quot; mäter Flash Player State Tracking den tid som spenderas med ljudet i stället för med passiva eller icke-aktiva videobilder när ljudet är avstängt eller den tid som spenderas i läget Normal jämfört med helskärm.

Spårning av spelarstatus ger följande fördelar:

* Tillhandahåller standardvariabler som mäter vanliga lägen, till exempel helskärmsläge eller undertextning
* Tillhandahåller anpassningsbara variabler för mätning av anpassade lägen under en uppspelningssession
* Mäter tid i ett anpassat spelarläge
* Mäter flera lägen som kan vara samtidigt

![Spårning av spelartillstånd](assets/player_state_tracking.png)

## Krav

Spårning av spelartillstånd kräver något av följande för datainsamling:
* Media JS SDK 3.0+
* Chromecast 3.0 SDK for Adobe Marketing Cloud Solutions
* Media Analytics-tillägg (som används med Adobe Experience Platform (AEP) SDK)
   * Webb: Adobe Media Analytics (3.x SDK) för Audio och Video v1.0+
   * Mobil: Adobe Media Analytics for Audio and Video v2.0+
* Media Collection API

## Riktlinjer

Innan du implementerar spårning av spelartillstånd bör du tänka på följande riktlinjer.

* Spelarläget beräknas för alla uppspelningslägen (ingen delning).
* Du kan mäta flera spelarlägen samtidigt.
* Det högsta antalet spelarlägen som kan spåras under en uppspelning är 10.
* Statusvärden för spelarstatus skickas till Analytics för att enbart rapportera om Media Close-anropet.
* Kunskap om programstatus bevaras inte när ett läge har stoppats. När ett läge har avslutats måste läget startas igen för att spårningen ska kunna fortsätta. För varje nytt uppspelningsläge måste spelarens tillstånd startas igen.
* Spelartillstånd hämtas för varje enskild uppspelningssession - spelarläget beräknas inte för alla uppspelningar.

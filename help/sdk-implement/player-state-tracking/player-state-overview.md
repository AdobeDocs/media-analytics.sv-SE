---
title: Om spårning av spelarstatus
description: I det här avsnittet beskrivs spårningsfunktionen för spelarstatus, inklusive krav och riktlinjer för implementering och rapportering av spelartillstånd.
translation-type: tm+mt
source-git-commit: 4c11efd0b8bb457246c746621e7fbb9fbda621b2
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Om spårning av spelarstatus

För att optimera din produktupplevelse och ditt företags enhetsvärde är det viktigt att förstå kundbeteendet när du visar videor. Detta omfattar den tid som tillbringas inom olika spelarstater.  Det är också viktigt att ha flexibiliteten att skapa och mäta nya spelarstater och evenemang efter behov.

Spårning av spelarstatus ger möjlighet att fånga in visningsinteraktion under uppspelning med hjälp av en standarduppsättning lösningsvariabler för helskärm, sluten bildtext, tyst läge, bild i bild och fokus.  Spårning av spelarstatus ger även möjlighet att skapa anpassade spelarlägen. Du kan använda mellanlagsspårningsvariabler för rapportering i Analysis Workspace.

Om du vill spela in ändringar av spelartillståndet uppdaterar lägesspårning videomätningens metadata. Om du t.ex. vill bestämma &quot;sant&quot; videoengagemang mäter Spårning av spelarstatus den tid som läggs på ljudet jämfört med passiva eller icke-aktiva videovyer när ljudet är avstängt eller den tid som används i läget Normal kontra helskärm.

Spårning av spelarstatus ger följande fördelar:

* Tillhandahåller standardvariabler som mäter gemensamma lägen, t.ex. helskärm eller sluten bildtext
* Tillhandahåller anpassningsbara variabler för att mäta anpassade lägen under en uppspelningssession
* Måtttid inom ett anpassat spelartillstånd
* Mäter flera tillstånd som kan vara samtidiga

![Spårning av spelarstatus](assets/player_state_tracking.png)

## Krav

Spårning av spelarstatus kräver något av följande för datainsamling:
* Media JS SDK 3.0+
* Chromecast 3.0 SDK för Adobe Marketing Cloud Solutions
* Media Analytics Extension (används med Adobe Experience Platform (AEP) SDK)
   * Webbplats: Adobe Media Analytics (3.x SDK) för Audio and Video v1.0+
   * Mobil: Adobe Media Analytics för ljud och video v2.0+
* Media Collection API

## Riktlinjer

Innan du implementerar lägesspårning bör du tänka på följande riktlinjer.

* Spelartillståndet beräknas för alla uppspelningstillstånd (ingen uppdelning).
* Du kan mäta flera spelarlägen samtidigt.
* Det maximala antalet uppspelningstillstånd som kan spåras under en uppspelning är 10.
* Spelarstatusmått skickas till Analytics för att endast rapportera om Media Close-anropet.
* Kunskap om programstatus upprätthålls inte när ett tillstånd har stoppats. När ett läge har avslutats måste tillståndet startas igen för att fortsätta spåra. För varje nytt uppspelningstillstånd måste spelarens tillstånd startas igen.
* Spelarlägen hämtas för varje enskild uppspelningssession. Spelartillståndet beräknas inte över uppspelningar.

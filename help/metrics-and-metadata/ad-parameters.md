---
title: Annonsparametrar
description: '"Lär dig mer om annonsparametrar, inklusive implementering, nätverk och rapportvariabler för annonsvideodata."'
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '1850'
ht-degree: 3%

---

# Annonsparametrar{#ad-parameters}

I det här avsnittet presenteras en lista med videoannonsdata, inklusive kontextdatavärden, som Adobe samlar in via lösningsvariabler.

Beskrivning av tabelldata:

* **implementering:** information om implementeringsvärden och -krav
   * *Key*  - Variable, ange antingen manuellt i appen eller automatiskt med Adobe Media SDK.
   * *Obligatoriskt*  - Anger om parametern krävs för grundläggande videospårning.
   * *Typ*  - Anger vilken typ av variabel som ska anges, strängen eller talet.
   * *Skickat med*  - Anger när data skickas:  *Media* Startis the analytics call sent on media start,  *Ad* Startis, the analytics call sent on ad ad start osv. &quot; ** Closecalls&quot; är de kompilerade analysanrop som skickas direkt från hjärtslagservern till analysservern i slutet av mediesessionen, eller i slutet av annonsen, kapitlet osv. Stäng anrop är inte tillgängliga i nätverkspaketanrop.
   * *Min. SDK-version* - Anger vilken SDK-version du behöver för att komma åt parametern.
   * *Exempelvärde*  - innehåller exempel på vanlig variabelanvändning.
* **Nätverksparametrar:** Visar värden som skickas till Adobe Analytics- eller pulsslagservrar. I den här kolumnen visas namnen på de parametrar som visas i nätverksanrop som genereras av Adobe Media SDK:er.
* **Rapportering:** Information om hur du visar och analyserar videodata.
   * *Tillgängligt*  - Anger om data är tillgängliga i rapporter som standard (*Ja*) eller om det krävs anpassad konfiguration (*Anpassad*)
   * *Reserverad variabel*  - Anger om data har fångats in som en händelse, eVar, prop eller klassificering i en reserverad variabel.
   * *Rapportnamn*  - Namn på analysrapport för Adobe för variabel
   * *Kontextdata*  - Namn på Adobe Analytics-kontextdata som skickas till rapportservern och används i bearbetningsregler.
   * *Datafeed*  - kolumnnamn för variabel som hittas i Clickstream- eller Live Stream-dataflöden
   * *Audience Manager* - Trait name found in Adobe Audience Manager

>[!IMPORTANT]
>
>Ändra inte klassificeringsnamnen för de variabler som listas nedan
>beskrivs under Rapportering/Reserverad variabel som&quot;klassificering&quot;.
>Medieklassificeringarna definieras när en rapportserie aktiveras för media
>spårning. emellanåt lägger Adobe till nya egenskaper och när detta inträffar,
>kunderna måste återaktivera sina rapporteringsprogram för att få tillgång till nya medier
>egenskaper. Under uppdateringsprocessen avgör Adobe om
>klassificeringar aktiveras genom att namnen på variablerna kontrolleras. Om något av
>om de saknas lägger Adobe till de saknade igen.

## Lägg till videodata {#ad-video-data}

### Annons-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.id </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** Alla  </li> <li> **Exempelvärde:**<br/> &quot;2125&quot; </li><li> **Beskrivning:**<br/> ID för annonsen. (Valfritt heltal och/eller bokstavskombination)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **pulsslag:**<br/> (:asset:ledsen_id) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **förfallodatum:**<br/> Vid besök </li> <li> **rapportnamn:**<br/> annons </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>namn) </li> <li> **datafeed:**<br/> videoad </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### Lägg till i rutposition

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podPosition </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Platsen (index) för annonsen inuti den överordnade annonsbrytningen. Den första annonsen har index 0, den andra annonsen har index 1, osv.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **pulsslag:**<br/> (:asset:spod_position) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Lägg till i rutposition </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **datafeed:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Annonslängd

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.length </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** 1.5.1 </li> <li> **Exempelvärde:**<br/> &quot;15&quot;  </li><li> **Beskrivning:**<br/> Längd på videoannons i sekunder.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **pulsslag:**<br/> (:asset:load_length) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar och klassificering </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> annonslängd och annonslängd (variabel) </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>längd) </li> <li> **datafeed:**<br/> videolängd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### Namn på annonsspelare

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.playerName </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;Freewheel&quot; </li><li> **Beskrivning:**<br/> Namnet på spelaren som ansvarar för att återge annonsen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **pulsslag:**<br/> (:sp:splayer_name) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> annonsspelarens namn </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>playerName) </li> <li> **datafeed:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Namn på annonsbrytning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podFriendlyName </li> <li> **Obligatoriskt:**<br/> SDK: Ja, API: Nej. </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;pre-roll&quot; </li><li> **Beskrivning:**<br/> Ad Breaks egna namn.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **pulsslag:**<br/> (:asset:spod_name) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Podnamn </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Annonsbrytningsindex

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podPosition </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Indexvärdet för annonsbrytningen i innehållet med början vid 1. Den här egenskapen används **endast** av Media SDK för att generera Pod-ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Hjärtslag:**<br/> </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Nej </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Annonsbrytningsposition

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podSecond </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 90 </li><li> **Beskrivning:**<br/> Annonsbrytningens förskjutning inuti innehållet, i sekunder.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **pulsslag:**<br/> (:asset:lpod_offset) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **rapportnamn:**<br/> rutposition </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID för annonsbrytning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **pulsslag:**<br/> (:asset:spod_id) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> annonsruta </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>pod) </li> <li> **datafeed:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Annonsnamn

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.name </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** 1.5.1 </li> <li> **Exempelvärde:**<br/> &quot;Ford F-150&quot; </li><li> **Beskrivning:annonsens**<br/> eget namn.  I rapporter är&quot;annonsnamn&quot; klassificeringen och&quot;annonsnamn (variabel)&quot; eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **pulsslag:**<br/> (:asset:ledsen_namn) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar och klassificering </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> annonsnamn och annonsnamn (variabel) </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Standard-annonsmetadata {#standard-ad-metadata}

### Annonsör

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> ADVERTISER </li> <li> **API-nyckel:**<br/> media.ad.advertiser </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Företag/Varumärke vars produkt visas i annonsen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>annonsör) </li> <li> **pulsslag:**<br/> (:meta:<br/>sa.media.ad.advertiser) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> <i>Annonsör  </i> </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>annonsör) </li> <li> **datafeed:**<br/> videoannonsör </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### Kampanj-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> CAMPAIGN_ID </li> <li> **API-nyckel:**<br/> media.ad.campaignId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> heltal eller namn (sträng).  </li><li> **Beskrivning:**<br/> ID för annonskampanjen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>kampanj) </li> <li> **pulsslag:**<br/> (:meta:<br/>sa.media.ad.campaign) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> <i>Kampanj-ID </i> </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>kampanj) </li> <li> **datafeed:**<br/> videokamera </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.ca) </li> </ul> |



### Kreativt ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> CREATIVE_ID </li> <li> **API-nyckel:**<br/> media.ad.creativeId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> heltal eller namn (sträng).  </li><li> **Beskrivning:**<br/> ID för annonspersonalen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creative) </li> <li> **pulsslag:**<br/> (:meta:<br/>sa.media.ad.creative) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> <i>Kreativt ID  </i> </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>creative) </li> <li> **datafeed:**<br/> adklassifikationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### Plats-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> SITE_ID </li> <li> **API-nyckel:**<br/> media.ad.siteId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> ID för annonsplatsen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>plats) </li> <li> **pulsslag:**<br/> (:meta:<br/>sa.media.ad.site) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> <i>Använd anpassad bearbetningsregel  </i> </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>plats) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### Kreativ URL

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> CREATIVE_URL </li> <li> **API-nyckel:**<br/> media.ad.creativeURL </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> URL för annonspersonalen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **pulsslag:**<br/> (:meta:<br/>sa.media.ad.creativeURL) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> <i>Använd anpassad bearbetningsregel  </i> </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### Placement-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> PLACEMENT_ID </li> <li> **API-nyckel:**<br/> media.ad.placementId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Start, Ad Close </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:annons**<br/> placerings-ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>placering) </li> <li> **pulsslag:**<br/> (:meta:<br/>sa.media.ad.placement) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> <i>Använd anpassad bearbetningsregel  </i> </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>placering) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Annonsmått {#ad-metrics}

### Annonsstart

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> annonsstart </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antal videoannonser som startar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>vy) </li> <li> **pulsslag:**<br/>  (:event:stype=start)<br/> (:asset:stype=ad) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> annonsstart </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>vy) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.vi) </li> </ul> |



### Ad Complete

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Close </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antal videoannonser har slutförts.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>complete) </li> <li> **pulsslag:**<br/> (:event:stype=complete)<br/> (:asset:stype=ad)  </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Ad Complete </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.comcomplete) </li> </ul> |



### Annonstid

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Ad Close </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 15 </li><li> **Beskrivning:**<br/> Den totala tiden (i sekunder) som har ägnats åt att titta på annonsen (dvs. antalet sekunder som har spelats upp).  Värdet visas i tidsformatet (HH:MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder.  <br/>**Releasedatum: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlay) </li> <li> **Hjärtslag:**<br/> </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Lägg till tid </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>timePlay) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## Relaterade API:er {#section_Related_APIs}

### createAdObject API:er:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject API:er:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartbeatConfig-API:er:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

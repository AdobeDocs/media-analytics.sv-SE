---
title: Annonsparametrar
description: '"Lär dig mer om annonsparametrar, inklusive implementering, nätverk och rapportvariabler för annonsvideodata."'
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 771cffe923af41d10cb6589d85cf984c43480c29
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 3%

---

# Annonsparametrar{#ad-parameters}

I det här avsnittet presenteras en lista med videoannonsdata, inklusive kontextdatavärden, som Adobe samlar in via lösningsvariabler.

Beskrivning av tabelldata:

* **Implementering:** Information om genomförandevärden och krav
   * *Nyckel* - Variabel, ange antingen manuellt i appen eller automatiskt med Adobe Media SDK.
   * *Obligatoriskt* - Anger om parametern krävs för grundläggande videospårning.
   * *Typ* - Anger vilken typ av variabel som ska anges, strängen eller talet.
   * *Skickat med* - Anger när data skickas: *Mediestart* är det analysanrop som skickas vid mediestart, *Annonsstart* är det analysanrop som skickas vid annonsstart osv., den *Stäng* anrop är de kompilerade analysanrop som skickas direkt från hjärtslagservern till analysservern i slutet av mediesessionen eller slutet av annonsen, kapitlet osv. Stäng anrop är inte tillgängliga i nätverkspaketanrop.
   * *Min. SDK-version* - Anger vilken SDK-version du behöver för att komma åt parametern.
   * *Exempelvärde* - Visar exempel på vanlig variabelanvändning.
* **Nätverksparametrar:** Visar de värden som skickas till Adobe Analytics- eller pulsslagservrar. I den här kolumnen visas namnen på de parametrar som visas i nätverksanrop som genereras av Adobe Media SDK:er.
* **Rapportering:** Information om hur du visar och analyserar videodata.
   * *Tillgänglig* - Anger om data är tillgängliga i rapporter som standard (*Ja*), eller kräver anpassad installation (*Egen*)
   * *Reserverad variabel* - Anger om data fångas in som en händelse, eVar, prop eller klassificering i en reserverad variabel.
   * *Rapportnamn* - Namn på Adobe Analytics-rapport för variabel
   * *Kontextdata* - Namnet på de Adobe Analytics-kontextdata som skickas till rapportservern och som används i bearbetningsregler.
   * *Datafeed* - Kolumnnamn för variabeln som hittades i dataflödena Clickstream eller Live Stream
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
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.id </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** Alla  </li> <li> **Exempelvärde:**<br/> &quot;2125&quot; </li><li> **Beskrivning:**<br/> ID för annonsen. (Valfritt heltal och/eller bokstavskombination)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **Hjärtslag:**<br/> (s:asset:ad_id) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid besök </li> <li> **Rapportnamn:**<br/> Annons </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>namn) </li> <li> **Datafeed:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetReference.@id </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.ID </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.ID </li> </ul> |



### Lägg till i rutposition

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podPosition </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Platsen (index) för annonsen inuti den överordnade annonsbrytningen. Den första annonsen har index 0, den andra annonsen har index 1, osv.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Hjärtslag:**<br/> (s:asset:pod_position) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Lägg till i rutposition </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Datafeed:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetViewDetails.index </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.index </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.index </li> </ul> |



### Annonslängd

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.length </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** 1.5.1 </li> <li> **Exempelvärde:**<br/> &quot;15&quot;  </li><li> **Beskrivning:**<br/> Längd på videoannonsen i sekunder.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **Hjärtslag:**<br/> (l:asset:ad_length) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar och klassificering </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Annonslängd och annonslängd (variabel) </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>längd) </li> <li> **Datafeed:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetReference.xmpDM:duration </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.length </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.length </li> </ul> |



### Namn på annonsspelare

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.playerName </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;Freewheel&quot; </li><li> **Beskrivning:**<br/> Namnet på spelaren som ansvarar för att återge annonsen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Hjärtslag:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Namn på annonsspelare </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Datafeed:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetViewDetails.playerName </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.playerName </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.playerName </li> </ul> |



### Namn på annonsbrytning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podFriendlyName </li> <li> **Obligatoriskt:**<br/> SDK: Ja, API: Nej. </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;pre-roll&quot; </li><li> **Beskrivning:**<br/> Ad Breaks egna namn.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Hjärtslag:**<br/> (s:asset:pod_name) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Pod Name </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetViewDetails.adBreak.dc:title </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingPodDetails.friendlyName </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingPodDetails.friendlyName </li> </ul> |



### Annonsbrytningsindex

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podPosition </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Indexvärdet för annonsbrytningen inuti innehållet med början på 1. Den här egenskapen används **endast** av Media SDK för att generera Pod ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Hjärtslag:**<br/> </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Nej </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetViewDetails.index </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingPodDetails.index </li> </ul> |



### Annonsbrytningsposition

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podSecond </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 90 </li><li> **Beskrivning:**<br/> Annonsens förskjutning i innehållet, i sekunder.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Hjärtslag:**<br/> (l:asset:pod_offset) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Pod Position </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetViewDetails.adBreak.offset </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingPodDetails.second </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingPodDetails.second </li> </ul> |



### ID för annonsbrytning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **Hjärtslag:**<br/> (s:asset:pod_id) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Annonsruta </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>pod) </li> <li> **Datafeed:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetViewDetails.adBreak.@id </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingPodDetails.adBreakID </li> </ul> |



### Annonsnamn

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.name </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** 1.5.1 </li> <li> **Exempelvärde:**<br/> &quot;Ford F-150&quot; </li><li> **Beskrivning:**<br/> Annonsens namn.  I rapporter är&quot;annonsnamn&quot; klassificeringen och&quot;annonsnamn (variabel)&quot; eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Hjärtslag:**<br/> (s:asset:ad_name) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar och klassificering </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Annonsnamn och annonsnamn (variabel) </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetReference.dc:title </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.name </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.name </li> </ul> |



## Standard-annonsmetadata {#standard-ad-metadata}

### Annonsör

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> ADVERTISER </li> <li> **API-nyckel:**<br/> media.ad.advertiser </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Företag/varumärke vars produkt visas i annonsen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>annonsör) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> <i>Annonsör </i> </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>annonsör) </li> <li> **Datafeed:**<br/> videoannonser </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetReference.publish </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.publish </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.publish </li> </ul> |



### Kampanj-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> CAMPAIGN_ID </li> <li> **API-nyckel:**<br/> media.ad.campaignId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> Heltal eller namn (sträng).  </li><li> **Beskrivning:**<br/> ID för annonskampanjen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>kampanj) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.ad.ca) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> <i>Kampanj-ID </i> </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>kampanj) </li> <li> **Datafeed:**<br/> videokampanj </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.ca) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetReference.campaign </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.campaignID </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.campaignID </li> </ul> |



### Kreativt ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> CREATIVE_ID </li> <li> **API-nyckel:**<br/> media.ad.creativeId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> Heltal eller namn (sträng).  </li><li> **Beskrivning:**<br/> ID för annonsens kreatör.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creative) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> <i>Kreativt ID </i> </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>creative) </li> <li> **Datafeed:**<br/> adklassificationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetReference.creativeID </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.creativeID </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.creativeID </li> </ul> |



### Plats-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> SITE_ID </li> <li> **API-nyckel:**<br/> media.ad.siteId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> ID för annonsplatsen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>plats) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> <i>Använd anpassad bearbetningsregel </i> </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Egen </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>plats) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetReference.siteID </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.siteID </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.siteID </li> </ul> |



### Kreativ URL

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> CREATIVE_URL </li> <li> **API-nyckel:**<br/> media.ad.creativeURL </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Webbadress till reklamkreatören.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> <i>Använd anpassad bearbetningsregel </i> </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Egen </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetReference.creativeURL </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.creativeURL </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.creativeURL </li> </ul> |



### Placement-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> PLACEMENT_ID </li> <li> **API-nyckel:**<br/> media.ad.placementId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart, annonsstängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Annonsens placerings-ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>placering) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> <i>Använd anpassad bearbetningsregel </i> </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Egen </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>placering) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.adAssetReference.placementID </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.placementID </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.placementID </li> </ul> |




## Annonsmått {#ad-metrics}

### Annonsstart

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Annonsstart </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antal videoannonser som startar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>vy) </li> <li> **Hjärtslag:**<br/>  (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Annonsöppningar </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>vy) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.vi) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.starting.value > 0 => &quot;TRUE&quot; </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.isStarted </li> </ul> |



### Ad Complete

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stäng annons </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antal slutförda videoannonser.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>complete) </li> <li> **Hjärtslag:**<br/> (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Ad Completes </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.comcomplete) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.complete.value > 0 => &quot;TRUE&quot; </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.isCompleted </li> </ul> |



### Annonstid

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stäng annons </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 15 </li><li> **Beskrivning:**<br/> Den totala tiden (i sekunder) som har ägnats åt att titta på annonsen (dvs. antalet sekunder som har spelats upp).  Värdet visas i tidsformat (HH):MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder.  <br/>**Releasedatum: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlay) </li> <li> **Hjärtslag:**<br/> </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Annonstid </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.ad.<br/>timePlay) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> <li> **Sökväg till XDM-fält:**<br/> advertising.timePlayed.value </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.advertisingDetails.timePlayed </li> </ul> |



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

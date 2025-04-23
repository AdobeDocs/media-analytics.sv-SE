---
title: Annonsparametrar
description: Lär dig mer om annonsparametrar, inklusive implementering, nätverk och rapportvariabler för annonsvideodata.
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ebabbe52fe673e3fb6f13da40bbc3c87aef1c7bd
workflow-type: tm+mt
source-wordcount: '2038'
ht-degree: 0%

---

# Annonsparametrar{#ad-parameters}

I det här avsnittet finns en lista med videoannonsdata, inklusive kontextdatavärden, som Adobe samlar in via lösningsvariabler.

Beskrivning av tabelldata:

* **Implementering:** Information om implementeringsvärden och krav
   * *Nyckel* - Variabel, antingen manuellt i appen eller automatiskt av Adobe Media SDK.
   * *Obligatorisk* - Anger om parametern krävs för grundläggande videospårning.
   * *Typ* - Anger typen för variabeln som ska anges, strängen eller talet.
   * *Skickat med* - Anger när data skickas: *Mediestart* är det analysanrop som skickas vid mediestart, *Ad Start* är det analysanrop som skickas vid annonsstart och så vidare. *Close* -anropen är de kompilerade analysanrop som skickas direkt från hjärtslagsservern till analysservern i slutet av mediesessionen eller i slutet annons, kapitel osv. Stäng anrop är inte tillgängliga i nätverkspaketanrop.
   * *Min. SDK Version* - Anger vilken SDK-version du behöver för att komma åt parametern.
   * *Exempelvärde* - Visar exempel på vanlig variabelanvändning.
* **Nätverksparametrar:** Visar de värden som skickas till Adobe Analytics- eller pulsslagservrar. I den här kolumnen visas namnen på de parametrar som visas i nätverksanrop som genereras av Adobe Media SDK:er.
* **Rapportering:** Information om hur du visar och analyserar videodata.
   * *Tillgänglig* - Anger om data är tillgängliga i rapporter som standard (*Ja*) eller om det krävs en anpassad konfiguration (*Anpassad*)
   * *Reserverad variabel* - Anger om data hämtas som en händelse, eVar, prop eller klassificering i en reserverad variabel.
   * *Rapportnamn* - Namn på Adobe Analytics-rapport för variabel
   * *Kontextdata* - Namnet på de Adobe Analytics-kontextdata som skickas till rapportservern och används i bearbetningsregler.
   * *Datafeed* - kolumnnamn för variabel som hittas i dataflöden från Clickstream eller Live Stream
   * *Audience Manager* - Trait name found in Adobe Audience Manager

>[!IMPORTANT]
>
>Ändra inte klassificeringsnamnen för de variabler som listas nedan
>beskrivs under Rapportering/Reserverad variabel som&quot;klassificering&quot;.
>Medieklassificeringarna definieras när en rapportserie aktiveras för media
>spårning. Då och då lägger Adobe till nya egenskaper och när detta inträffar,
>kunderna måste återaktivera sina rapporteringsprogram för att få tillgång till nya medier
>egenskaper. Under uppdateringsprocessen avgör Adobe om
>klassificeringar aktiveras genom att namnen på variablerna kontrolleras. Om något av
>om de saknas lägger Adobe till de saknade.

## Lägg till videodata {#ad-video-data}

### Annons-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.id </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** Alla  </li> <li> **Exempelvärde:**<br/> &quot;2125&quot; </li><li> **Beskrivning:**<br/> ID för annonsen. (Valfritt heltal och/eller bokstavskombination)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>namn) </li> <li> **pulsslag:**<br/> (<code>s:asset:ad_id}</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid BESÖK </li> <li> **Rapportnamn:**<br/> Annons </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>namn) </li> <li> **Datafeed:**<br/> videoad </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.adAssetReference._id </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.name </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.name </li> </ul> |



### Lägg till i rutposition

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podPosition </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Positionen (indexvärdet) för annonsen inuti den överordnade annonsbrytningen. Den första annonsen har index 0, den andra annonsen har index 1, osv.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>podPosition) </li> <li> **pulsslag:**<br/> (<code>s:asset:pod_position)</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Lägg till i rutposition </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>podPosition) </li> <li> **Datafeed:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **XDM-fältsökväg:** (inaktuell)<br/> advertising.adAssetViewDetails.index </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.podPosition </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.podPosition </li> </ul> |



### Annonslängd

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.length </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** 1.5.1 </li> <li> **Exempelvärde:**<br/> &quot;15&quot;  </li><li> **Beskrivning:**<br/> Längd på videoannons i sekunder.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>längd) </li> <li> **pulsslag:**<br/> (<code>l:asset:ad_length</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar och klassificering </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Lägg till längd och annonslängd (variabel) </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>längd) </li> <li> **Datafeed:**<br/> videolängd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.adAssetReference.<br/>_xmpDM.duration </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.length </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.length </li> </ul> |



### Namn på annonsspelaren

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.playerName </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;Freewheel&quot; </li><li> **Beskrivning:**<br/> Namnet på spelaren som ansvarar för att återge annonsen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>playerName) </li> <li> **pulsslag:**<br/> (<code>s:sp:player_name)</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Ad Player-namn </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>playerName) </li> <li> **Datafeed:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> <li> **XDM-fältsökväg:** (inaktuell)<br/> advertising.adAssetViewDetails.playerName </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.<br/>playerName </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.<br/>playerName </li> </ul> |



### Namn på annonsbrytning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [namn](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podFriendlyName </li> <li> **Obligatoriskt:**<br/> SDK: Ja; API: Nej. </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;pre-roll&quot; </li><li> **Beskrivning:**<br/> Ad Breaks egna namn.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>podFriendlyName) </li> <li> **pulsslag:**<br/> (<code>s:asset:pod_name)</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Podnamn </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>podFriendlyName) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.adAssetViewDetails.<br/>adBreak._dc.title </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingPodDetails.<br/>friendlyName </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingPodDetails.<br/>friendlyName </li> </ul> |



### Annonsbrytningsindex

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podIndex </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Indexvärdet för annonsbrytningen i innehållet med början vid 1. Den här egenskapen används **endast** av Media SDK för att generera Pod ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **pulsslag:**<br/> </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Nej </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> </li> <li> **XDM-fältsökväg:** (inaktuell)<br/> advertising.adAssetViewDetails.index </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingPodDetails.index </li> </ul> |



### Annonsbrytningsposition

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.podSecond </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 90 </li><li> **Beskrivning:**<br/> Annonsbrytningens förskjutning inuti innehållet, i sekunder.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>podSecond) </li> <li> **pulsslag:**<br/> (<code>l:asset:pod_offset)</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Pod Position </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>podSecond) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.adAssetViewDetails.adBreak.<br/>förskjutning </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingPodDetails.<br/>förskjutning </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingPodDetails.<br/>förskjutning </li> </ul> |



### ID för annonsbrytning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ange automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>pod) </li> <li> **pulsslag:**<br/> (<code>s:asset:pod_id)</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Annonspod </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>pod) </li> <li> **Datafeed:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.adAssetViewDetails.adBreak._id </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingPodDetails.<br/>ID </li> </ul> |



### Annonsnamn

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [namn](./ad-parameters.md#section_Related_APIs) </li> <li> **API-nyckel:**<br/> media.ad.name </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** 1.5.1 </li> <li> **Exempelvärde:**<br/> &quot;Ford F-150&quot; </li><li> **Beskrivning:**<br/> Annonsens eget namn.  I rapporter är&quot;annonsnamn&quot; klassificeringen och&quot;annonsnamn (variabel)&quot; eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>friendlyName) </li> <li> **pulsslag:**<br/> (<code>s:asset:ad_name)</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar och klassificering </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Annonsnamn och annonsnamn (variabel) </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>friendlyName) </li> <li> **Datafeed:**<br/> videoadname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.adAssetReference._dc.title </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.friendlyName </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.friendlyName </li> </ul> |



## Standard-annonsmetadata {#standard-ad-metadata}

### Annonsör

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK Key:**<br/> ADVERTISER </li> <li> **API-nyckel:**<br/> media.ad.advertiser </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Företag/varumärke vars produkt visas i annonsen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>annonser) </li> <li> **pulsslag:**<br/> (<code>s:meta:)</code><br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> <i>Advertiser </i> </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>annonser) </li> <li> **Datafeed:**<br/> videoannonsör </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> <li> **XDM-fältsökväg:** (inaktuell)<br/> advertising.adAssetReference.publish </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.publishser </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.publish </li> </ul> |



### Kampanj-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> CAMPAIGN_ID </li> <li> **API-nyckel:**<br/> media.ad.campaignId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> Heltal eller namn (sträng).  </li><li> **Beskrivning:**<br/> ID för annonskampanjen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>kampanj) </li> <li> **pulsslag:**<br/> (<code>s:meta:)</code><br/>a.media.ad.caämta) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> <i>Kampanj-ID </i> </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>kampanj) </li> <li> **Datafeed:**<br/> videokampanj </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.caämta) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.adAssetReference.campaign </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.<br/>campaignID </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.<br/>campaignID </li> </ul> |



### CREATIVE ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> CREATIVE_ID </li> <li> **API-nyckel:**<br/> media.ad.creativeId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> Heltal eller namn (sträng).  </li><li> **Beskrivning:**<br/> ID för annonsskaparen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>kreativ) </li> <li> **pulsslag:**<br/> (<code>s:meta:)</code><br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> <i>Creative-ID </i> </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>kreativ) </li> <li> **Datafeed:**<br/> adklassifikationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.adAssetReference.creativeID </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.creativeID </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.creativeID </li> </ul> |



### Plats-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> SITE_ID </li> <li> **API-nyckel:**<br/> media.ad.siteId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> ID för annonsplatsen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>plats) </li> <li> **pulsslag:**<br/> (<code>s:meta:)</code><br/>a.media.ad.site) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> <i>Använd anpassad bearbetningsregel </i> </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Anpassat </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>plats) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.adAssetReference.siteID </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.siteID </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.siteID </li> </ul> |



### CREATIVE URL

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> CREATIVE_URL </li> <li> **API-nyckel:**<br/> media.ad.creativeURL </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> URL för annonsskaparen.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>creativeURL) </li> <li> **pulsslag:**<br/> (<code>s:meta:&lt;c/ode><br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> <i>Använd anpassad bearbetningsregel </i> </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Anpassat </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>creativeURL) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> <li> **XDM-fältsökväg:** (inaktuell)<br/> advertising.adAssetReference.creativeURL </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.<br/>creativeURL </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.<br/>creativeURL </li> </ul> |



### Placement-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> PLACEMENT_ID </li> <li> **API-nyckel:**<br/> media.ad.placementId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Lägg till, Lägg till och stäng </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Annonsens placerings-ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>placering) </li> <li> **pulsslag:**<br/> (<code>s:meta:)</code><br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> <i>Använd anpassad bearbetningsregel </i> </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Anpassat </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>placering) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.adAssetReference.placementID </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.advertisingDetails.<br/>placementID </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.<br/>placementID </li> </ul> |




## Annonsmått {#ad-metrics}

### Annonsstart

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ange automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> annonsstart </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antal videoannonser som startar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>vy) </li> <li> **pulsslag:**<br/> (<code>s:event:type=start</code>)<br/> (<code>s:asset:type=ad<code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Ad Starts </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>vy) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.viytt) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.starting.value > 0 => &quot;TRUE&quot; </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.isStarted </li> </ul> |



### Ad Complete

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ange automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> och stäng </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antal videoannonser har slutförts.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>slutförd) </li> <li> **pulsslag:**<br/> (<code>s:event:type=complete</code>)<br/> (<code>s:asset:type=ad</code>)  </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Annonsen är klar </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>slutförd) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.comcomplete) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.complete.value > 0 => &quot;TRUE&quot; </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.<br/>isCompleted </li> </ul> |



### Annonstid

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ange automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> och stäng </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 15 </li><li> **Beskrivning:**<br/> Den totala tiden (i sekunder) som har ägnats åt att titta på annonsen (dvs. antalet sekunder som har spelats upp).  Värdet visas i tidsformat (<code>HH:MM:SS)</code>) i Analysis Workspace och Reports &amp; Analytics. I Data Feeds, Data Warehouse och Reporting API:er visas värdena på några sekunder.  <br/>**Releasedatum: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad).<br/>timePlayed) </li> <li> **pulsslag:**<br/> </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Annonstid </li> <li> **Datafeed:**<br/> videoadtime </li> <li> **Kontextdata:**<br/> (a.media.ad).<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlay) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/> advertising.timePlayed.value </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.advertisingDetails.<br/>timePlay </li> </ul> |



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

---
title: Kvalitetsparametrar
description: Läs mer om kvalitetsparametrarna (QoE) som används för att hämta kvalitetsmetadata.
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
exl-id: aac178dc-5a46-4ce3-80e9-ec82cbfbfff5
feature: Media Analytics, Variables
role: User, Admin, Data Engineer
source-git-commit: 6e01f55ac498d69a6f7eac4ac0086e276cc0dd8a
workflow-type: tm+mt
source-wordcount: '3106'
ht-degree: 2%

---

# Kvalitetsparametrar{#quality-parameters}

I det här avsnittet presenteras en lista över upplevelsekvalitet (QoE/QoS), inklusive kontextdatavärden, som Adobe samlar in via lösningsvariabler.

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

## Metadata för kvalitet {#quality-metadata}

### Genomsnittlig bithastighet

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [bithastighet](./quality-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.qoe.bitrate </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 800-899 </li><li> **Beskrivning:**<br/> Genomsnittlig bithastighet (i kbit/s). Värdet är fördefinierat inom intervall om 100 kbit/s. Den genomsnittliga bithastigheten beräknas som ett vägt genomsnitt av alla bithastighetsvärden som relateras till uppspelningens varaktighet som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>bitrateAverageBucket) </li> <li> **Hjärtslag:**<br/> (l:stream:bithastighet) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Genomsnittlig bithastighet </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bitrateAverageBucket) </li> <li> **Datafeed:**<br/> videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverageBucket </li> </ul> |


### Starttid

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.qoe.timeToStart </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Mediestart, stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 30 000 </li><li> **Beskrivning:**<br/> Standardvärdet är noll om du inte anger det via QoSObject. Du anger det här värdet i millisekunder. Värdet visas i tidsformat (HH):MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>timeToStart) </li> <li> **Hjärtslag:**<br/> (l:stream:startup_time) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Starttid </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>timeToStart) </li> <li> **Datafeed:**<br/> videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value </li> </ul> |


### Bildrutor per sekund

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.qoe.framesPerSecond </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Mediestart, stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 24 </li><li> **Beskrivning:**<br/> Det aktuella värdet för direktuppspelningens bildrutehastighet (i bildrutor per sekund). Fältet mappas till fps-fältet i stängningsanropet och kan nås via bearbetningsregler.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Hjärtslag:**<br/> (l:stream:fps) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Nej </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> </li> <li> **Sökväg till XDM-fält:**<br/>  </li> </ul> |



### Släppta bildrutor

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> droppedFrames </li> <li> **API-nyckel:**<br/> media.qoe.droppedFrames </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 3 </li><li> **Beskrivning:**<br/> Antalet uteslutna bildrutor (Int). Detta värde beräknas som summan av alla bildrutor som släpps under en uppspelningssession. Det här värdet hämtas från det sista värdet av (l):stream:drop_frames).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>dropFrameCount) </li> <li> **Hjärtslag:**<br/> (l:stream:<br/>drop_frames) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Släppta bildrutor </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>dropFrameCount) </li> <li> **Datafeed:**<br/> videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount) </li> <li> **Sökväg till XDM-fält:**<br/>  media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value </li> </ul> |



### Bufferthändelser

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 2 </li><li> **Beskrivning:**<br/> Antalet bufferthändelser. Detta mått beräknas som antalet olika buffertlägen som inträffade under en uppspelningssession. Detta är antalet gånger spelaren försätts i ett buffertläge från andra lägen, t.ex. uppspelning eller pausning.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>bufferCount) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Bufferthändelser </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bufferCount) </li> <li> **Datafeed:**<br/> videoqoebuffcountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> <li> **Sökväg till XDM-fält:**<br/>  media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value </li> </ul> |



### Buffertvaraktighet totalt

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** </li> <li> **Exempelvärde:**<br/> 30 </li><li> **Beskrivning:**<br/> Den totala tiden, i sekunder, för buffring. Det här värdet beräknas som summan av alla bufferthändelsevaraktigheter som inträffade under en uppspelningssession. Värdet visas i tidsformat (HH):MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder. <br/>**Releasedatum: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>bufferTime) </li> <li> **Hjärtslag:**<br/> (l:event:längd) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Buffertvaraktighet totalt </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bufferTime) </li> <li> **Datafeed:**<br/> videoqoebuffer timeevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value </li> </ul> |



### Bithastighetsändringar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.qoe.bitrateChange </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 3 </li><li> **Beskrivning:**<br/> Antalet bithastighetsändringar (heltal). Detta värde beräknas som summan av alla bithastighetsändringshändelser som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>bitrateChangeCount) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Bithastighetsändringar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bitrateChangeCount) </li> <li> **Datafeed:**<br/> videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value </li> </ul> |



### Fel-/felhändelser

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Antalet fel (heltal). Detta värde beräknas som summan av alla felhändelser som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>errorCount) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Fel </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>errorCount) </li> <li> **Datafeed:**<br/> videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.errors.value </li> </ul> |



### Fel-ID för Player SDK

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Unika fel-ID:n som genereras av spelarens SDK. Kunderna måste ange felkoder/ID:n vid implementeringen via de felprogrammeringsgränssnitt som tillhandahålls.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>playerSdkErrors) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Fel-ID för Player SDK </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>playerSdkErrors) </li> <li> **Datafeed:**<br/> videoinspelaredkerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors </li> </ul> |



### Externa fel-ID:n

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Unika fel-ID:n från externa källor, t.ex. CDN-fel. Kunderna måste ange felkoder/ID:n vid implementeringen via de felprogrammeringsgränssnitt som tillhandahålls.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>externalErrors) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Externa fel-ID:n </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>externalErrors) </li> <li> **Datafeed:**<br/> videoqoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors </li> </ul> |



### Fel-ID för Media SDK

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Unika fel-ID:n som genereras av Media SDK under uppspelning.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>mediaSdkErrors) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Egen </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>mediaSdkErrors) </li> <li> **Datafeed:**<br/> mediaqoeexternalfel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.mediaSdkErrors </li> </ul><br/> |




### Sessionsslut {#session-end}

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** 2.1 </li> <li> **Exempelvärde:**<br/> end </li><li> **Beskrivning:**<br/> Sluthändelsen betyder att SDK skickar ett nära anrop till backend-objektet. När den här händelsen tas emot stänger backend sessionen för videon och ingen ytterligare bearbetning görs. <br/>Om mediet är klart till 100 % ska det skickas efter `s:event:type=complete.` Se [Innehållet har slutförts](audio-video-parameters.md#content-complete) för relaterad information. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> (s:event:type=end) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> </li> <li> **Sökväg till XDM-fält:**<br/>  </li> </ul> |



## Kvalitetsmått {#quality-metrics}

### Starttid

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 30 000 </li><li> **Beskrivning:**<br/> Standardvärdet är noll om du inte anger det via QoSObject. Du anger det här värdet i millisekunder. Värdet visas i tidsformat (HH):MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder. <br/>**Releasedatum: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>timeToStart) </li> <li> **Hjärtslag:**<br/> (l:stream:startup_time) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Starttid </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>timeToStart) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value </li> </ul> |



### Bufferthändelser

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 2 </li><li> **Beskrivning:**<br/> Antalet bufferthändelser (heltal). Det här måttet beräknas som antalet bufferthändelser som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>bufferCount) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Bufferthändelser </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bufferCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value </li> </ul> |



### Buffertvaraktighet totalt

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 15 </li><li> **Beskrivning:**<br/> Den totala buffringstiden (sekunder). heltal). Det här värdet beräknas som summan av alla bufferthändelsevaraktigheter som inträffade under en uppspelningssession. Värdet visas i tidsformat (HH):MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder. <br/>**Releasedatum: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>bufferTime) </li> <li> **Hjärtslag:**<br/> (l:event:längd) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Buffertvaraktighet totalt </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bufferTime) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value </li> </ul> |



### Bithastighetsändringar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> Händelse </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;3&quot; </li><li> **Beskrivning:**<br/> Antalet bithastighetsändringar. Detta värde beräknas som summan av alla bithastighetsändringshändelser som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>bitrateChangeCount) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Bithastighetsändringar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bitrateChangeCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value </li> </ul> |



### Fel

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Antalet fel som uppstod (heltal). Detta värde beräknas som summan av alla felhändelser som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>errorCount) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Felhändelser </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>errorCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.errors.value </li> </ul> |



### Släppta bildrutor

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Antalet uteslutna bildrutor (heltal). Detta värde beräknas som summan av alla bildrutor som släpps under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>dropFrameCount) </li> <li> **Hjärtslag:**<br/> (l:stream:<br/>drop_frames) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Släppta bildrutor </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>dropFrameCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount) </li> <li> **Sökväg till XDM-fält:**<br/>  media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value </li> </ul> |



### Droppar före start

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet gånger som en användare avslutar videon innan den börjar. Det här måttet är bara 1 om inget innehåll återges, oavsett annonser.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>dropBeforeStart) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Släpper före start </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>dropBeforeStart) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> <li> **Sökväg till XDM-fält:**<br/>  media.mediaTimed.primaryAssetViewDetails.qoe.dropBeforeStarts.value >= 1 => &quot;TRUE&quot; </li> </ul> |



>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Buffertpåverkade strömmar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet strömmar som påverkas av buffring. Det här måttet är bara 1 om minst en bufferthändelse inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>buffert) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Buffertpåverkade strömmar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>buffert) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>buffert) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bufferImpachedStreams.value >= 1 => &quot;TRUE&quot; </li> </ul> |



>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Ändrade bithastighetsströmmar som påverkas

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet strömmar i vilka bithastighetsändringar inträffade. Det här måttet anges till 1 endast om minst en bithastighetsändringshändelse inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>bitrateChange) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Ändrade bithastighetsströmmar som påverkas </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bitrateChange) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChangeImpachedStreams.value >= 1 => &quot;TRUE&quot; </li> </ul> |



>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Genomsnittlig bithastighet

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 3200 </li><li> **Beskrivning:**<br/> Genomsnittlig bithastighet (i kbit/s, heltal). Det här måttet beräknas som ett vägt genomsnitt av alla bithastighetsvärden som är relaterade till uppspelningens varaktighet som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>bitrateAverage) </li> <li> **Hjärtslag:**<br/> (l:stream:bithastighet) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Genomsnittlig bithastighet </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bitrateAverage) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value </li> </ul> |



### Felpåverkade strömmar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet strömmar i vilka en felhändelse inträffade (dvs. `trackError` anropades under uppspelningssessionen, och `type=error` hjärtslagsanrop genererades). </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>fel) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Felpåverkade strömmar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>fel) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>fel) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.errorImpachedStreams.value > 0 => &quot;TRUE&quot; </li> </ul> |



>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Ignorerade bildrutepåverkade strömmar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet strömmar i vilka bildrutor släpptes. Det här måttet är bara 1 om minst en bildruta har tagits bort under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>droppedFrames) </li> <li> **Hjärtslag:**<br/> (l:stream:<br/>drop_frames) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Ignorerade bildrutepåverkade strömmar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>droppedFrames) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrames) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.dropFrameImpachedStreams.value >= 1 => &quot;TRUE&quot; </li> </ul> |



>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Strömmar som påverkas

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** 1,5+ </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet strömmar i vilka en händelse som avstannat inträffade. Det här måttet är bara 1 om minst en hög inträffade under uppspelningen. Kunderna måste skapa egna bearbetningsregler för att kunna rapportera värdet.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>stall) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Egen</li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>stall) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stall) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.stallingImpachedStreams.value >= 1 => &quot;TRUE&quot; </li> </ul><br/> |

>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Fallande händelser

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** 1,5+ </li> <li> **Exempelvärde:**<br/> &quot;3&quot; </li><li> **Beskrivning:**<br/> Antalet gånger som uppspelningen stoppades under en uppspelningssession. Kunderna måste skapa egna bearbetningsregler för att kunna rapportera värdet.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>stallCount) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Egen</li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>stallCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.stalls.value </li> </ul><br/> |



### Total varaktighet

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng media </li> <li> **Min. SDK-version:** 1,5+ </li> <li> **Exempelvärde:**<br/> 12 </li><li> **Beskrivning:**<br/> Total tid (sekunder). heltal) spelningen stoppades under en uppspelningssession. Kunderna måste skapa egna bearbetningsregler för att kunna rapportera värdet.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe)<br/>stallTime) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Egen</li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>stallTime) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.stallTime.value </li> </ul> <br/> |



## Relaterade API:er {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

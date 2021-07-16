---
title: Kvalitetsparametrar
description: Läs mer om kvalitetsparametrarna (QoE) som används för att hämta kvalitetsmetadata.
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
exl-id: aac178dc-5a46-4ce3-80e9-ec82cbfbfff5
feature: '"Media Analytics, Variables"'
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '2997'
ht-degree: 2%

---

# Kvalitetsparametrar{#quality-parameters}

I det här avsnittet presenteras en lista över upplevelsekvalitet (QoE/QoS), inklusive kontextdatavärden, som Adobe samlar in via lösningsvariabler.

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

## Metadata för kvalitet {#quality-metadata}

### Genomsnittlig bithastighet

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [bithastighet](./quality-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.qoe.bitrate </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Stäng </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 800-899 </li><li> **Beskrivning:**<br/> Genomsnittlig bithastighet (i kbit/s). Värdet är fördefinierat inom intervall om 100 kbit/s. Den genomsnittliga bithastigheten beräknas som ett vägt genomsnitt av alla bithastighetsvärden som relateras till uppspelningens varaktighet som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **pulsslag:**<br/> (:stream:bithastighet) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> genomsnittlig bithastighet </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bitrateAverageBucket) </li> <li> **datafeed:**<br/> videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> </ul> |


### Starttid

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.qoe.timeToStart </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 30 000 </li><li> **Beskrivning:**<br/> Det här värdet är som standard noll om du inte anger det via QoSObject. Du anger det här värdet i millisekunder. Värdet visas i tidsformatet (HH:MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **pulsslag:**<br/> (:stream:lstartup_time) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> tid att starta </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>timeToStart) </li> <li> **datafeed:**<br/> videoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |


### Bildrutor per sekund

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.qoe.framesPerSecond </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 24 </li><li> **Beskrivning:**<br/> Strömmens aktuella bildrutehastighet (i bildrutor per sekund). Fältet mappas till fps-fältet i stängningsanropet och kan nås via bearbetningsregler.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **pulsslag:**<br/> (:stream:lfps) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Nej </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Släppta bildrutor

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> dropFrames </li> <li> **API-nyckel:**<br/> media.qoe.droppedFrames </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 3 </li><li> **Beskrivning:**<br/> Antalet uteslutna bildrutor (Int). Detta värde beräknas som summan av alla bildrutor som släpps under en uppspelningssession. Det här värdet hämtas från det sista värdet för (l:stream:dropped_frames).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>dropFrameCount) </li> <li> **pulsslag:**<br/> (:stream:<br/>ldropped_frames) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> uteslutna bildrutor </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>dropFrameCount) </li> <li> **datafeed:**<br/> videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount) </li> </ul> |



### Bufferthändelser

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 2 </li><li> **Beskrivning:**<br/> Antalet bufferthändelser. Detta mått beräknas som antalet olika buffertlägen som inträffade under en uppspelningssession. Detta är antalet gånger spelaren försätts i ett buffertläge från andra lägen, t.ex. uppspelning eller pausning.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=buffer) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> bufferthändelser </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bufferCount) </li> <li> **datafeed:**<br/> videoqoebuffer countevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Buffertvaraktighet totalt

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** </li> <li> **Exempelvärde:**<br/> 30 </li><li> **Beskrivning:**<br/> Den totala tiden, i sekunder, för buffring. Det här värdet beräknas som summan av alla bufferthändelsevaraktigheter som inträffade under en uppspelningssession. Värdet visas i tidsformatet (HH:MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder. <br/>**Releasedatum: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **pulsslag:**<br/> (:event:lduration) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Total buffertvaraktighet </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bufferTime) </li> <li> **Datafeed:**<br/> videoqoebuffer timeevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Bithastighetsändringar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.qoe.bitrateChange </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 3 </li><li> **Beskrivning:**<br/> Antalet bithastighetsändringar (heltal). Detta värde beräknas som summan av alla bithastighetsändringshändelser som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=bitrate_change) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> bithastighetsändringar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bitrateChangeCount) </li> <li> **datafeed:**<br/> videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Fel-/felhändelser

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Antalet fel (heltal). Detta värde beräknas som summan av alla felhändelser som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> fel </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>errorCount) </li> <li> **datafeed:**<br/> videoquoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### Fel-ID för Player SDK

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> De unika fel-ID:n som genereras av spelarens SDK. Kunderna måste ange felkoder/ID:n vid implementeringen via de felprogrammeringsgränssnitt som tillhandahålls.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>playerSdkErrors) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Player SDK-fel-ID </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>playerSdkErrors) </li> <li> **datafeed:**<br/> videoqoeplayerdkerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> </ul> |



### Externa fel-ID:n

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Unika fel-ID:n från externa källor, t.ex. CDN-fel. Kunderna måste ange felkoder/ID:n vid implementeringen via de felprogrammeringsgränssnitt som tillhandahålls.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>externalErrors) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> externt fel-ID </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>externalErrors) </li> <li> **datafeed:**<br/> videoquoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> </ul> |



### Fel-ID för Media SDK

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> De unika fel-ID:n som genereras av Media SDK under uppspelning.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>mediaSdkErrors) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>mediaSdkErrors) </li> <li> **datafeed:**<br/> mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> </ul><br/> |




### Sessionsslut {#session-end}

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** 2.1 </li> <li> **Exempelvärde:**<br/> end </li><li> **Beskrivning:**<br/> Sluthändelsen betyder att SDK skickar ett nära anrop till backend-objektet. När den här händelsen tas emot stänger backend sessionen för videon och ingen ytterligare bearbetning görs. <br/>Om mediet har slutförts till 100 % ska det skickas efter  `s:event:type=complete.` Se  [innehållsslutförande ](audio-video-parameters.md#content-complete) för relaterad information. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> (:event:stype=end) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> </li> </ul> |



## Kvalitetsmått {#quality-metrics}

### Starttid

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 30 000 </li><li> **Beskrivning:**<br/> Det här värdet är som standard noll om du inte anger det via QoSObject. Du anger det här värdet i millisekunder. Värdet visas i tidsformatet (HH:MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder. <br/>**Releasedatum: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **pulsslag:**<br/> (:stream:lstartup_time) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> tid att starta </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>timeToStart) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### Bufferthändelser

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 2 </li><li> **Beskrivning:**<br/> Antalet bufferthändelser (heltal). Det här måttet beräknas som antalet bufferthändelser som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=buffer) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> bufferthändelser </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bufferCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Buffertvaraktighet totalt

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 15 </li><li> **Beskrivning:**<br/> Den totala buffringstiden (sekunder). heltal). Det här värdet beräknas som summan av alla bufferthändelsevaraktigheter som inträffade under en uppspelningssession. Värdet visas i tidsformatet (HH:MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder. <br/>**Releasedatum: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **pulsslag:**<br/> (:event:lduration) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Total buffertvaraktighet </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bufferTime) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Bithastighetsändringar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> händelse </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;3&quot; </li><li> **Beskrivning:**<br/> Antalet bithastighetsändringar. Detta värde beräknas som summan av alla bithastighetsändringshändelser som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=bitrate_change) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> bithastighetsändringar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bitrateChangeCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Fel

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Antal fel som inträffat (heltal). Detta värde beräknas som summan av alla felhändelser som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> felhändelser </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>errorCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### Släppta bildrutor

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 </li><li> **Beskrivning:**<br/> Antalet uteslutna bildrutor (heltal). Detta värde beräknas som summan av alla bildrutor som släpps under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>dropFrameCount) </li> <li> **pulsslag:**<br/> (:stream:<br/>ldropped_frames) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> uteslutna bildrutor </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>dropFrameCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount) </li> </ul> |



### Droppar före start

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet gånger som en användare avslutar videon innan den startas. Det här måttet är bara 1 om inget innehåll återges, oavsett annonser.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>dropBeforeStart) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=aa_start) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> släpp före start </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>dropBeforeStart) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Buffertpåverkade strömmar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet strömmar som påverkas av buffring. Det här måttet är bara 1 om minst en bufferthändelse inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>buffert) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=buffer) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Buffertpåverkade strömmar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>buffert) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>buffert) </li> </ul> |



>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Ändrade bithastighetsströmmar som påverkas

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet strömmar där bithastighetsändringar inträffade. Det här måttet anges till 1 endast om minst en bithastighetsändringshändelse inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChange) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=bitrate_change) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Bithastighetsändring, påverkade strömmar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bitrateChange) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Genomsnittlig bithastighet

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 3200 </li><li> **Beskrivning:**<br/> Genomsnittlig bithastighet (i kbit/s, heltal). Det här måttet beräknas som ett vägt genomsnitt av alla bithastighetsvärden som är relaterade till uppspelningens varaktighet som inträffade under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateAverage) </li> <li> **pulsslag:**<br/> (:stream:bithastighet) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> genomsnittlig bithastighet </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>bitrateAverage) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> </ul> |



### Felpåverkade strömmar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet strömmar där en felhändelse inträffade (d.v.s.  `trackError` anropades under uppspelningssessionen och ett  `type=error` pulsslagsanrop genererades). </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>fel) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Felpåverkade strömmar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>fel) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>fel) </li> </ul> |



>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Ignorerade bildrutepåverkade strömmar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet strömmar i vilka bildrutor släpptes. Det här måttet är bara 1 om minst en bildruta har tagits bort under en uppspelningssession.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>droppedFrames) </li> <li> **pulsslag:**<br/> (:stream:<br/>ldropped_frames) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Ignorerade bildrutepåverkade strömmar </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>droppedFrames) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Strömmar som påverkas

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** 1.5+ </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet strömmar där en fast händelse inträffade. Det här måttet är bara 1 om minst en hög inträffade under uppspelningen. Kunderna måste skapa egna bearbetningsregler för att kunna rapportera värdet.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stall) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=stall) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Eget</li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>stall) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stall) </li> </ul><br/> |

>[!IMPORTANT]
>
>Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.

### Fallande händelser

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** 1.5+ </li> <li> **Exempelvärde:**<br/> &quot;3&quot; </li><li> **Beskrivning:**<br/> Antalet gånger som uppspelningen stoppades under en uppspelningssession. Kunderna måste skapa egna bearbetningsregler för att kunna rapportera värdet.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stallCount) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=stall) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Eget</li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>stallCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> </ul><br/> |



### Total varaktighet

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** 1.5+ </li> <li> **Exempelvärde:**<br/> 12 </li><li> **Beskrivning:**<br/> Total tid (sekunder; heltal) spelningen stoppades under en uppspelningssession. Kunderna måste skapa egna bearbetningsregler för att kunna rapportera värdet.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stallTime) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=stall) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Eget</li> <li> **Kontextdata:**<br/> (a.media.qoe)<br/>stallTime) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> </ul> <br/> |



## Relaterade API:er {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

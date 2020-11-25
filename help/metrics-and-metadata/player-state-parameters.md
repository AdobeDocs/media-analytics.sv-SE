---
title: Parametrar för spelartillstånd
description: I det här avsnittet beskrivs parametrar för spårning av spelartillstånd.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 1cf631d7f3d5365a02be99af78655ac3b53fb3cb
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 1%

---


# Parametrar för spelartillstånd{#player-state-parameters}

I det här avsnittet visas en lista med data om spelartillstånd som Adobe samlar in via lösningsvariabler.

Beskrivning av tabelldata:

* **implementering:** information om implementeringsvärden och -krav
   * *Key*  - Variable, ange antingen manuellt i appen eller automatiskt av Adobe Media SDK.
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
>Ändra inte klassificeringsnamnen för de variabler som listas nedan och som beskrivs under Rapportera/Reserverad variabel som &quot;klassificering&quot;.\
>Medieklassificeringarna definieras när en rapportsserie aktiveras för mediespårning. Ibland lägger Adobe till nya egenskaper och när detta inträffar måste kunderna återaktivera sina rapporteringsprogram för att få tillgång till de nya medieegenskaperna. Under uppdateringsprocessen avgör Adobe om klassificeringarna är aktiverade genom att kontrollera namnen på variablerna. Om någon av dem saknas lägger Adobe till de saknade igen.

## Egenskaper för spelartillstånd {#player-state-properties}

Spårningsfunktionerna för spelartillstånd kan kopplas till ett ljud- eller videoflöde. Standardiserade spårningsvärden för spelartillstånd lagras som lösningsvariabler. Standardlägena är: fullScreen, mute, closeCaption, pictureInPicture och inFocus.

### Egenskaper för helskärm

#### Strömmar som påverkas av helskärm

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Antalet strömmar som påverkas av helskärmsläge. Det här måttet är bara 1 om minst ett helskärmsläge inträffade under en uppspelningssession. <br/> **Viktigt** <br/> Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.fullscreen.set<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Rapportera**<br/> NameStreams som påverkas av helskärm </li> <li> **Context**<br/> Data.media.states.fullscreen.set<br/> </li> <li> **Data**<br/> FeedvideoStatusScreen </li> <li> **Audience**<br/> Manager_contextdata.a.media.states.fullscreen.set </li> </ul> |

#### Antal helskärmar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> ****<br/> Beskrivning Det antal gånger som en helskärm visades. Det här måttet är bara 1 om minst ett helskärmsläge inträffade under en uppspelningssession. <br/> **Viktigt**<br/> Om den här händelsen anges är antalet lika med det antal gånger videon var i helskärmsläge. Om den här händelsen inte anges skickas inget värde.</li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.fullscreen.count<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Rapportera**<br/> namnAntal helskärmar </li> <li> **Context**<br/> Data.media.states.fullscreen.count<br/> </li> <li> **Data**<br/> Feedvideostatefullscreencount </li> <li> **Audience**<br/> Manager_contextdata.media.states.fullscreen.count </li> </ul> |



#### Total längd för helskärm

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Den tid som en helskärm visades. Det här måttet är bara 1 om minst ett helskärmsläge inträffade under en uppspelningssession. <br/> ****<br/>  ViktigtOm den här händelsen anges motsvarar tiden hur länge videon var i helskärmsläge. Om den här händelsen inte anges skickas inget värde.  </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.fullscreen.time<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **RapportnamnTotal**<br/> varaktighet för helskärm </li> <li> **Context**<br/> Data.media.states.fullscreen.time<br/> </li> <li> **Data**<br/> Feedvideostatefullscreentime </li> <li> **Audience**<br/> Manager_contextdata.media.states.fullscreen.time </li> </ul> |


### Stäng bildtextegenskaper

#### Strömmar som påverkas av undertextning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Antalet strömmar som påverkas av undertextning. Det här måttet är bara 1 om minst ett textningstillstånd inträffade under en uppspelningssession. <br/> **Viktigt** <br/>  Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.closedcaptioning.set<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Rapportera**<br/> NameStreams som påverkas av dold textning </li> <li> **Context**<br/> Data.media.states.closedcaptioning.set<br/> </li> <li> **Data**<br/> Feedvideostateclosedcaptioning </li> <li> **Audience**<br/> Manager_contextdata.a.media.states.closedcaptioning.set </li> </ul> |


#### Antal textning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Antalet gånger som textning visas. Det här måttet är bara 1 om minst ett textningstillstånd inträffade under en uppspelningssession. <br/> **Viktigt**<br/>  Om den här händelsen anges är antalet lika med det antal gånger videon var i läget Undertexter. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.closedcaptioning.count<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Rapportera**<br/> namnAntal textning </li> <li> **Context**<br/> Data.media.states.closedcaptioning.count<br/> </li> <li> **Data**<br/> Feedvideostatecolescaptioncount </li> <li> **Audience**<br/> Manager_contextdata.media.states.closedcaptioning.count </li> </ul> |


#### Total varaktighet för undertextning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Den tid som textning visades. Det här måttet är bara 1 om minst ett helskärmsläge inträffade under en uppspelningssession. <br/> ****<br/>  ViktigtOm den här händelsen anges motsvarar tiden hur länge videon var i läget för undertextning. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.closedcaptioning.time<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Total varaktighet för**<br/> rapportnamnTextning </li> <li> **Context**<br/> Data.media.states.closedcaptioning.time<br/> </li> <li> **Data**<br/> Feedvideostatecolescaptioningtime </li> <li> **Audience**<br/> Manager_contextdata.media.states.closedcaptioning.time </li> </ul> |


### Stäng av egenskaper

#### Strömmar som påverkas av ljud av

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Antalet strömmar som påverkas av Mute. Det här måttet anges till 1 endast om minst ett Mute-läge inträffade under en uppspelningssession. <br/> **Viktigt** <br/> Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.mute.set<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Rapportera**<br/> NameStreams som påverkas av Mute </li> <li> **Context**<br/> Data.media.states.mute.set<br/> </li> <li> **Data**<br/> FeedvideoStatement </li> <li> **Audience**<br/> Manager_contextdata.a.media.states.mute.set </li> </ul> |

#### Antal avstängningar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> ****<br/> BeskrivningAntalet gånger som ljud av visades. Det här måttet anges till 1 endast om minst ett Mute-läge inträffade under en uppspelningssession. <br/> ****<br/>  ViktigtOm den här händelsen anges är antalet lika med det antal gånger videon var i läget Ljud av. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.mute.count<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Rapport**<br/> NameMute Count </li> <li> **Context**<br/> Data.media.states.mute.count<br/> </li> <li> **Data**<br/> FeedVideoCount </li> <li> **Audience**<br/> Manager_contextdata.media.states.mute.count </li> </ul> |

#### Total varaktighet för tyst

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> ****<br/> BeskrivningLängden på tiden Mute visades. Det här måttet anges till 1 endast om minst ett Mute-läge inträffade under en uppspelningssession. <br/> ****<br/> ViktigtOm den här händelsen anges motsvarar tiden hur länge videon var i läget Ljud av. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.mute.time<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Total varaktighet**<br/> för rapportnamnMute </li> <li> **Context**<br/> Data.media.states.mute.time<br/> </li> <li> **Data**<br/> FeedVideoStatusTime </li> <li> **Audience**<br/> Manager_contextdata.media.states.mute.time </li> </ul> |


### Bild-i-bildegenskaper


#### Strömmar som påverkas av bild-i-bild

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Antalet strömmar som påverkas av bild-i-bild. Det här måttet är bara 1 om minst ett bild-i-bildläge inträffade under en uppspelningssession. <br/> **Viktigt** <br/> Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.picturepicture.set<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Rapportera**<br/> namnströmmar som påverkas av bild-i-bild </li> <li> **Context**<br/> Data.media.states.picturepicture.set<br/> </li> <li> **Data**<br/> Feedvideostatepturepicture </li> <li> **Audience**<br/> Manager_contextdata.a.media.states.picturepicture.set </li> </ul> |


#### Bild-i-bildantal

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Antalet gånger som bild-i-bild visades. Det här måttet är bara 1 om minst ett bild-i-bildläge inträffade under en uppspelningssession. <br/> **** <br/> ViktigtOm den här händelsen anges är antalet lika med det antal gånger som videon var i läget Bild-i-bild. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.picturepicture.count<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Rapportera**<br/> namnBild-i-bildantal </li> <li> **Context**<br/> Data.media.states.picturepicture.count<br/> </li> <li> **Data**<br/> Feedvideostateptuåterpicturecount </li> <li> **Audience**<br/> Manager_contextdata.media.states.picturepicture.count </li> </ul> |


#### Total längd för bild-i-bild

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Tidslängden för bild-i-bild visades. Det här måttet är bara 1 om minst ett bild-i-bildläge inträffade under en uppspelningssession. <br/> **** <br/> ViktigtOm den här händelsen anges motsvarar tiden hur länge videon var i läget Bild i bild. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.picturepicture.time<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Total längd för**<br/> rapportnamnBild-i-bild </li> <li> **Context**<br/> Data.media.states.picturepicture.time<br/> </li> <li> **Data**<br/> Feedvideostateptuåterpicturetime </li> <li> **Audience**<br/> Manager_contextdata.media.states.picturepicture.time </li> </ul> |


### Egenskaper för fokus

#### Strömmar som påverkas av InFocus

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Antalet strömmar som påverkas av InFocus. Det här måttet anges till 1 endast om minst ett I fokus-läge inträffade under en uppspelningssession. <br/> **Viktigt** <br/> Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.infocus.set<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Rapportera**<br/> NameStreams som påverkas av InFocus </li> <li> **Context**<br/> Data.media.states.infocus.set<br/> </li> <li> **Data**<br/> Feedvideostateinfocus </li> <li> **Audience**<br/> Manager_contextdata.a.media.states.infocus.set </li> </ul> |


#### I fokus

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Antalet gånger som fokus visades. Det här måttet anges till 1 endast om minst ett I fokus-läge inträffade under en uppspelningssession. <br/> ****<br/>  ViktigtOm den här händelsen anges är antalet lika med det antal gånger som videon var i fokus-läge. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.infocus.count<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Rapportnamn**<br/> i fokus </li> <li> **Context**<br/> Data.media.states.infocus.count<br/> </li> <li> **Data**<br/> FeedVideoStatusInfoCount </li> <li> **Audience**<br/> Manager_contextdata.media.states.infocus.count </li> </ul> |


#### Total längd för fokus

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeyAutomatically set  </li> <li> **API**<br/> KeyN/A </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Skickat**<br/> med stängt media </li> <li> **Min. SDK-version**<br/> 3.0</li> <li> **Exempel**<br/> ValueTRUE </li><li> **Beskrivning**<br/> Tidslängden i fokus visades. Det här måttet anges till 1 endast om minst ett I fokus-läge inträffade under en uppspelningssession. <br/> **** <br/> ViktigtOm den här händelsen anges motsvarar tiden hur länge videon var i fokus. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.infocus.time<br/></li> <li> ****<br/> HeartbeatN/A </li> </ul> | <ul> <li> ****<br/> TillgängligtJa </li> <li> **Reserverad**<br/> variabelhändelse </li> <li> **Total längd**<br/> för rapportnamn i fokus </li> <li> **Context**<br/> Data.media.states.infocus.time<br/> </li> <li> **Data**<br/> Feedvideostateinfocustime </li> <li> **Audience**<br/> Manager_contextdata.media.states.infocus.time </li> </ul> |

## Egenskapslista för XDM-identiteter

Data som lagras i Analytics kan användas i alla syften och Player State-mätvärdena kan importeras till Adobe Experience Platform med hjälp av XDM och användas med Customer Journey Analytics.

| Egenskapen Spelartillstånd | Mappning |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## Relaterade API:er {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

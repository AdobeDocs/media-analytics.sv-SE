---
title: Parametrar för spelartillstånd
description: I det här avsnittet beskrivs parametrar för spårning av spelartillstånd.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 3c24b69265287084393be830193da14ae85cc5ba
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 0%

---


# Parametrar för spelartillstånd{#player-state-parameters}

I det här avsnittet finns en lista med data om spelartillstånd som Adobe samlar in via lösningsvariabler.

Beskrivning av tabelldata:

* **Implementering:** Information om genomförandevärden och krav
   * *Nyckel* - Variabel, antingen manuellt i appen eller automatiskt i Adobe Media SDK.
   * *Obligatoriskt* - Anger om parametern krävs för grundläggande videospårning.
   * *Typ* - Anger vilken typ av variabel som ska anges, strängen eller talet.
   * *Skickat med* - Anger när data skickas: *Media Start* är det analysanrop som skickas vid mediestart, *Ad Start* är det analysanrop som skickas vid annonsstart och så vidare. anropet *Close* är de kompilerade analysanrop som skickas direkt från hjärtslagservern till analysservern i slutet av mediesessionen eller slutet av annonsen, kapitlet osv. Stäng anrop är inte tillgängliga i nätverkspaketanrop.
   * *Min. SDK-version* - Anger vilken SDK-version du behöver för att komma åt parametern.
   * *Exempelvärde* - innehåller exempel på vanlig variabelanvändning.
* **Nätverksparametrar:** Visar värdena som skickas till Adobe Analytics- eller Heartbeat-servrar. I den här kolumnen visas namnen på de parametrar som visas i nätverksanrop som genereras av Adobe Media SDK:er.
* **Rapportering:** Information om hur du visar och analyserar videodata.
   * *Tillgänglig* - Anger om data är tillgängliga i rapporter som standard (*Ja*) eller om det krävs anpassad konfiguration (*Anpassad*)
   * *Reserverad variabel* - Anger om data hämtas som en händelse, eVar, prop eller klassificering i en reserverad variabel.
   * *Rapportnamn* - namn på Adobe Analytics-rapport för variabel
   * *Kontextdata* - Namnet på de Adobe Analytics-kontextdata som skickas till rapportservern och som används i bearbetningsregler.
   * *Datafeed* - kolumnnamn för variabel som hittas i dataflöden från Clickstream eller Live Stream
   * *Audience Manager* - Trait name found in Adobe Audience Manager

>[!IMPORTANT]
>
>Ändra inte klassificeringsnamnen för de variabler som listas nedan och som beskrivs under Rapportera/Reserverad variabel som &quot;klassificering&quot;.\
>Medieklassificeringarna definieras när en rapportsserie aktiveras för mediespårning. Då och då lägger Adobe till nya egenskaper och när detta inträffar måste kunderna aktivera sina rapporteringsprogram på nytt för att få tillgång till de nya medieegenskaperna. Under uppdateringsprocessen avgör Adobe om klassificeringarna är aktiverade genom att kontrollera namnen på variablerna. Om någon av dem saknas lägger Adobe till de som saknas igen.



## Egenskaper för spelartillstånd {#player-state-properties}

Tabellerna för spårningsegenskaper för spelarstatus är ordnade i följande fem avsnitt:

* Helskärm
   * Strömmar som påverkas av helskärm
   * Antal helskärmar
   * Total längd för helskärm
* Stäng bildtext
   * Strömmar som påverkas av undertextning
   * Antal textning
   * Total varaktighet för undertextning
* Ljud av
   * Strömmar som påverkas av ljud av
   * Antal avstängningar
   * Total varaktighet för tyst
* Bild-i-bild
   * Direktuppspelning som påverkas av bild-i-bild
   * Bild-i-bildantal
   * Total längd för bild-i-bild
* I fokus
   * Strömmar som påverkas av InFocus
   * I fokus
   * Total längd för fokus

### Egenskaper för helskärm

#### Strömmar som påverkas av helskärm

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Antalet strömmar som påverkas av helskärmsläge. Det här måttet är bara 1 om minst ett helskärmsläge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamnsströmmar **<br/>som påverkas av helskärm</li> <li> **Context Data **<br/>(a.media.states.fullscreen.set)<br/> </li> <li> **Videostatefärg för **<br/>datafeed</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.fullscreen.set)</li> </ul> |

#### Antal helskärmar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> ****<br/>Beskrivning Det antal gånger som en helskärm visades. Det här måttet är bara 1 om minst ett helskärmsläge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreencount)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamn **<br/>, helskärmsläge</li> <li> **Kontextdata **<br/>(videostatefullscreencount)<br/> </li> <li> **Data Feed **<br/>videostatefullscreencount</li> <li> **Audience Manager **<br/>(c_contextdata.videostatefullscreencount)</li> </ul> |



#### Total längd för helskärm

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Den tid som en helskärm visades. Det här måttet är bara 1 om minst ett helskärmsläge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreentime)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamn **<br/>, helskärmsvaraktighet</li> <li> **Kontextdata **<br/>(videostatefullscreentime)<br/> </li> <li> **Datautmatning **<br/>videostatefullscreentime</li> <li> **Audience Manager **<br/>(c_contextdata.videostatefullscreentime)</li> </ul> |


### Stäng bildtextegenskaper

#### Strömmar som påverkas av undertextning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Antalet strömmar som påverkas av undertextning. Det här måttet är bara 1 om minst ett textningstillstånd inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.closedcaptioning.set)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamnsströmmar **<br/>som påverkas av undertextning</li> <li> **Context Data **<br/>(a.media.states.closedcaptioning.set)<br/> </li> <li> **Datautmatningsvideostatelänkarbildtext **<br/></li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.closedcaptioning.set)</li> </ul> |


#### Antal textning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Antalet gånger som undertextning har valts. Det här måttet är bara 1 om minst ett textningstillstånd inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningcount)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Antal undertexter för rapportnamn **<br/></li> <li> **Kontextdata **<br/>(videostateclosedcaptioningcount)<br/> </li> <li> **videostatecolescaptionantal för **<br/>datafeed</li> <li> **Audience Manager **<br/>(c_contextdata.videostateclosedcaptioningcount)</li> </ul> |


#### Total varaktighet för undertextning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Den tid som textning för undertexter valdes. Det här måttet är bara 1 om minst ett textningstillstånd inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningtime)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamn **<br/>, varaktighet för undertextning</li> <li> **Kontextdata **<br/>(videostateclosedcaptioningtime)<br/> </li> <li> **Datafeed **<br/>videostatecolescaptioningtime</li> <li> **Audience Manager **<br/>(c_contextdata.videostateclosedcaptioningtime)</li> </ul> |


### Stäng av egenskaper

#### Strömmar som påverkas av ljud av

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Antalet strömmar som påverkas av Mute. Det här måttet anges till 1 endast om minst ett Mute-läge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamnsströmmar **<br/>som påverkas av ljud av</li> <li> **Context Data **<br/>(a.media.states.mute.set)<br/> </li> <li> **Videouttryck för **<br/>datafeed</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.mute.set)</li> </ul> |

#### Antal avstängningar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Antalet gånger som Ljud av har valts. Det här måttet anges till 1 endast om minst ett Mute-läge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutecount)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Antal avstängningar **<br/>av rapportnamn</li> <li> **Kontextdata **<br/>(videostatemutecount)<br/> </li> <li> **Datautflöde **<br/>videostatuutecount</li> <li> **Audience Manager **<br/>(c_contextdata.videostatemutecount)</li> </ul> |

#### Total varaktighet för tyst

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> ****<br/>BeskrivningLängden på den tid Mute valdes. Det här måttet anges till 1 endast om minst ett Mute-läge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutetime)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamn **<br/>, varaktighet av tyst</li> <li> **Kontextdata **<br/>(videoStatusTime)<br/> </li> <li> **Datautmatningsvideomeddelandetid **<br/></li> <li> **Audience Manager **<br/>(c_contextdata.videostatemutetime)</li> </ul> |


### Bild-i-bildegenskaper


#### Strömmar som påverkas av bild-i-bild

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Antalet strömmar som påverkas av bild-i-bild. Det här måttet är bara 1 om minst ett bild-i-bildläge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.picturepicture.set)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamnsströmmar **<br/>som påverkas av bild-i-bild</li> <li> **Kontextdata **<br/>(a.media.states.picturepicture.set)<br/> </li> <li> **Datafeed **<br/>videostateptuåtervisningsbild</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.picturepicture.set)</li> </ul> |


#### Bild-i-bildantal

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Antalet gånger som bild-i-bild visades. Det här måttet är bara 1 om minst ett bild-i-bildläge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictuåterpicturecount)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamn **<br/>bild-i-bildantal</li> <li> **Kontextdata **<br/>(videostatepicturempicturecount)<br/> </li> <li> **videostatepictuåterpicturecount för **<br/>datafeed</li> <li> **Audience Manager **<br/>(c_contextdata.videostatepicturepicturecount)</li> </ul> |


#### Total längd för bild-i-bild

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Tidslängden för bild-i-bild visades. Det här måttet är bara 1 om minst ett bild-i-bildläge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictuåterpicturetime)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamn **<br/>bild-i-bildvaraktighet</li> <li> **Kontextdata **<br/>(videostatepictuåterpicturetime)<br/> </li> <li> **Datautmatningsvideostatepuåterpicturetime **<br/></li> <li> **Audience Manager **<br/>(c_contextdata.videostatepicturepicturetime)</li> </ul> |


### Egenskaper för fokus

#### Strömmar som påverkas av InFocus

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Antalet strömmar som påverkas av InFocus. Det här måttet anges till 1 endast om minst ett I fokus-läge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamnsströmmar **<br/>som påverkas av fokus</li> <li> **Kontextdata **<br/>(a.media.states.infocus.set)<br/> </li> <li> **Datautflöde **<br/>videostateinfocus</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.states.infocus.set)</li> </ul> |


#### I fokus

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Antalet gånger som fokus visades. Det här måttet anges till 1 endast om minst ett I fokus-läge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocuscount)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamn **<br/>i fokusantal</li> <li> **Kontextdata **<br/>(videostateinfocuscount)<br/> </li> <li> **Data Feed **<br/>videostateinfocuscount</li> <li> **Audience Manager **<br/>(c_contextdata.videostateinfocuscount)</li> </ul> |


#### Total längd för fokus

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel **<br/>anges automatiskt</li> <li> **API-nyckel **<br/>saknas</li> <li> **Obligatoriskt **<br/>nr</li> <li> **Ange **<br/>nummer</li> <li> **Skickat med **<br/>mediestängning</li> <li> **Min. SDK version **<br/>3.0</li> <li> **Exempelvärde **<br/>TRUE</li><li> **Beskrivning **<br/>Tidslängden i fokus visades. Det här måttet anges till 1 endast om minst ett I fokus-läge inträffade under en uppspelningssession.<br/> **Viktigt** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocustime)<br/></li> <li> **Hjärtslag **<br/>N/A</li> </ul> | <ul> <li> **Tillgängligt **<br/>Ja</li> <li> **Reserverad variabelhändelse **<br/></li> <li> **Rapportnamn **<br/>i fokus</li> <li> **Kontextdata **<br/>(videostateinfocustime)<br/> </li> <li> **Videostateinfocustime för **<br/>datafeed</li> <li> **Audience Manager **<br/>(c_contextdata.videostateinfocustime)</li> </ul> |



## Relaterade API:er {#related_apis_section}

BEHOV: Lägg till API-länkar i dokument:
* Android - [createStateObject](https://need)
* iOS - [createStateObjectWithName](https://need)
* Javascript - [createStateObject](https://need)

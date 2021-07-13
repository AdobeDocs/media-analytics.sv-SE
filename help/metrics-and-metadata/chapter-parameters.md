---
title: Kapitelparametrar
description: '"Läs mer om kapitelparametrar för implementering, nätverk och rapportering."'
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 2%

---

# Kapitelparametrar{#chapter-parameters}

I det här avsnittet finns en lista med kapitel- och/eller segmentdata, inklusive kontextdatavärden, som Adobe samlar in via lösningsvariabler.

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
>Ändra inte klassificeringsnamnen för de variabler som listas nedan och som beskrivs under Rapportera/Reserverad variabel som &quot;klassificering&quot;.\
>Medieklassificeringarna definieras när en rapportsserie aktiveras för mediespårning. Ibland lägger Adobe till nya egenskaper och när detta inträffar måste kunderna återaktivera sina rapporteringsprogram för att få tillgång till de nya medieegenskaperna. Under uppdateringsprocessen avgör Adobe om klassificeringarna är aktiverade genom att kontrollera namnen på variablerna. Om någon av dem saknas lägger Adobe till de saknade igen.

## Kapitelmetadata {#chapter-metadata}

### Kapitelnamn

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.chapter.friendlyName </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Kapitelstart, Kapitelstängning </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> &quot;The Big Bang Chapter 2 - Dating&quot; </li><li> **Beskrivning:**<br/> Namnet på kapitlet och/eller segmentet.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **pulsslag:**<br/> (:stream:schapter_name) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Skapad som standard..  </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **rapportnamn:**<br/> kapitelnamn </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> </ul> |

### Kapitelposition

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.chapter.index </li> <li> **Obligatoriskt:**<br/> SDK: Nej. API: Ja. </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Kapitelstängning </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> 2 </li><li> **Beskrivning:**<br/> Placeringen (index, heltal) av kapitlet i innehållet.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>position) </li> <li> **pulsslag:**<br/> (:stream:lchapter_pos) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **rapportnamn:**<br/> kapitelposition </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>position) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>position) </li> </ul> |

### Kapitelförskjutning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.chapter.offset </li> <li> **Obligatoriskt:**<br/> SDK: Nej. API: Ja. </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Kapitelstängning </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> 58 </li><li> **Beskrivning:**<br/> Kapitelns förskjutning i innehållet (i sekunder) från början.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>förskjutning) </li> <li> **pulsslag:**<br/> (:stream:lchapter_offset) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **rapportnamn:**<br/> kapitelförskjutning </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>förskjutning) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>förskjutning) </li> </ul> |

### Kapitellängd

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.chapter.length </li> <li> **Obligatoriskt:**<br/> SDK: Nej. API: Ja. </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Kapitelstängning </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> 486 </li><li> **Beskrivning:**<br/> Kapitelns längd i sekunder.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>length) </li> <li> **pulsslag:**<br/> (:stream:lchapter_length) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **rapportnamn:**<br/> kapitellängd </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>längd) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>längd) </li> </ul> |

### Kapitel

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Kapitelstängning </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Kapitelets automatiskt genererade ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>name) </li> <li> **pulsslag:**<br/> (:stream:schapter_id) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> kapitel </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>namn) </li> <li> **datafeed:**<br/> videokort </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>namn) </li> </ul> |

## Kapitelmått {#chapter-Metrics}

### Kapitelstart

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven  </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Kapitelstart </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet kapitel börjar.  **Viktigt:**  Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>vy) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=chapter_start) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> kapitelstart</li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>vy) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>vy) </li> </ul> |

### Kapitel slutfört

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven  </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Kapitelstängning </li> <li> **Min. SDK-version:** 1.3</li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet kapitel slutförs.  **Viktigt:**  Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>complete) </li> <li> **pulsslag:**<br/> (:event:<br/>stype=chapter_complete) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> kapitelslutföranden</li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> </ul> |

### Kapiteltid spenderad

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven  </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Kapitelstängning </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Den tid som har ägnats åt kapitlet.  Värdet visas i tidsformatet (HH:MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder. <br/>**Releasedatum: 09/13/18**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>timePlay) </li> <li> **Hjärtslag:**<br/> </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Kapiteltid använt</li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>timePlay) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlay) </li> </ul> |

## Relaterade API:er {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)

---
title: Kapitelparametrar
description: "Läs mer om kapitelparametrar för implementering, nätverk och rapportering."
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 2%

---

# Kapitelparametrar{#chapter-parameters}

I det här avsnittet finns en lista med kapitel- och/eller segmentdata, inklusive kontextdatavärden, som Adobe samlar in via lösningsvariabler.

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
>Ändra inte klassificeringsnamnen för de variabler som listas nedan och som beskrivs under Rapportera/Reserverad variabel som &quot;klassificering&quot;.\
>Medieklassificeringarna definieras när en rapportsserie aktiveras för mediespårning. Ibland lägger Adobe till nya egenskaper och när detta inträffar måste kunderna återaktivera sina rapporteringsprogram för att få tillgång till de nya medieegenskaperna. Under uppdateringsprocessen avgör Adobe om klassificeringarna är aktiverade genom att kontrollera namnen på variablerna. Om någon av dem saknas lägger Adobe till de saknade igen.

## Kapitelmetadata {#chapter-metadata}

### Kapitelnamn

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.chapter.friendlyName </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Kapitelstart, kapitelstängning </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> &quot;The Big Bang Chapter 2 - Dating&quot; </li><li> **Beskrivning:**<br/> Namnet på kapitlet och/eller segmentet.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Hjärtslag:**<br/> (s:stream:kapitel_namn) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Skapad som standard...  </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Kapitelnamn </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.dc:title </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.chapterDetails.friendlyName </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.chapterDetails.friendlyName </li> </ul> |

### Kapitelposition

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.chapter.index </li> <li> **Obligatoriskt:**<br/> SDK: Nej. API: Ja. </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stängd kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> 2 </li><li> **Beskrivning:**<br/> Placeringen (index, heltal) av kapitlet inuti innehållet.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>position) </li> <li> **Hjärtslag:**<br/> (l:stream:kapitel_pos) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Kapitelposition </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>position) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>position) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.index </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.chapterDetails.index </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.chapterDetails.index </li> </ul> |

### Kapitelförskjutning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.chapter.offset </li> <li> **Obligatoriskt:**<br/> SDK: Nej. API: Ja. </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stängd kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> 58 </li><li> **Beskrivning:**<br/> Kapitelns förskjutning i innehållet (i sekunder) från början.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>förskjutning) </li> <li> **Hjärtslag:**<br/> (l:stream:kapitel_förskjutning) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Kapitelförskjutning </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>förskjutning) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>förskjutning) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.offset </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.chapterDetails.offset </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.chapterDetails.offset </li> </ul> |

### Kapitellängd

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.chapter.length </li> <li> **Obligatoriskt:**<br/> SDK: Nej. API: Ja. </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stängd kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> 486 </li><li> **Beskrivning:**<br/> Kapitelns längd i sekunder.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>length) </li> <li> **Hjärtslag:**<br/> (l:stream:kapitel_längd) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Kapitellängd </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>längd) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>längd) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.xmpDM:duration </li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.chapterDetails.length </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.chapterDetails.length </li> </ul> |

### Kapitel

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stängd kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Kapitelets automatiskt genererade ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>name) </li> <li> **Hjärtslag:**<br/> (s:stream:kapitel_id) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallodatum:**<br/> Vid TRIT </li> <li> **Rapportnamn:**<br/> Kapitel </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>namn) </li> <li> **Datafeed:**<br/> videokort </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>namn) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.@id </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.chapterDetails.ID </li> </ul> |

## Kapitelmått {#chapter-Metrics}

### Kapitelstart

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt  </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Kapitelstart </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet kapitel börjar.  **Viktigt:**  Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>vy) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Kapitelstart</li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>vy) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>vy) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.chapterCount.<br/>värde > 0 => &quot;TRUE&quot; </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.chapterDetails.isStarted </li> </ul> |

### Kapitel slutfört

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt  </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> string </li> <li> **Skickat med:**<br/> Stängd kapitel </li> <li> **Min. SDK-version:** 1.3</li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet kapitel slutförs.  **Viktigt:**  Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Hjärtslag:**<br/> (s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Kapitel slutförs</li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.mediaChapter.<br/>complete.value </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.chapterDetails.isCompleted </li> </ul> |

### Kapiteltid spenderad

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ställ in automatiskt  </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stängd kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Den tid som har ägnats åt kapitlet.  Värdet visas i tidsformat (HH):MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder. <br/>**Releasedatum: 09/13/18**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>timePlay) </li> <li> **Hjärtslag:**<br/> </li> </ul> | <ul> <li> **Tillgängligt:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> event </li> <li> **Rapportnamn:**<br/> Kapiteltid spenderad</li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>timePlay) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlay) </li> <li> **Sökväg till XDM-fält:**<br/> media.mediaTimed.mediaChapter.<br/>timePlayed.value </li> <li> **Sökväg till Reporting XDM-fält:**<br/> mediaReporting.chapterDetails.timePlay </li> </ul> |

## Relaterade API:er {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)

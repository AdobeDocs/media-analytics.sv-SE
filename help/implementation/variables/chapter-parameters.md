---
title: Kapitelparametrar
description: Lär dig mer om kapitelparametrar för implementering, nätverk och rapportering.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 6e8334098e5db63ac5b108b7d3986b2fe9c8c91f
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# Kapitelparametrar{#chapter-parameters}

I det här avsnittet finns en lista med kapitel- och/eller segmentdata, inklusive kontextdatavärden, som Adobe samlar in via lösningsvariabler.

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
>Ändra inte klassificeringsnamnen för de variabler som listas nedan och som beskrivs under Rapportera/Reserverad variabel som &quot;klassificering&quot;.\
>Medieklassificeringarna definieras när en rapportsserie aktiveras för mediespårning. Ibland lägger Adobe till nya egenskaper och när detta inträffar måste kunderna aktivera sina rapporteringsprogram på nytt för att få tillgång till de nya medieegenskaperna. Under uppdateringsprocessen avgör Adobe om klassificeringarna är aktiverade genom att kontrollera namnen på variablerna. Om någon av dem saknas lägger Adobe till de saknade igen.

## Kapitelmetadata {#chapter-metadata}

### Kapitelnamn

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [namn](./chapter-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.chapter.friendlyName </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Stänga kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> &quot;The Big Bang Chapter 2 - Dating&quot; </li><li> **Beskrivning:**<br/> Namnet på kapitlet och/eller segmentet.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **pulsslag:**<br/> (<code>s:stream:kapitel_name)</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Skapad som standard..  </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Kapitelnamn </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/>media.mediaTimed.mediaChapter.<br/>chapterAssetReference.dc:title</li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.chapterDetails.friendlyName </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.chapterDetails.friendlyName </li> </ul> |

### Kapitelposition

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.chapter.index </li> <li> **Obligatoriskt:**<br/> SDK: Nej; API: Ja. </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stänga kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> 2 </li><li> **Beskrivning:**<br/> Placeringen (index, heltal) av kapitlet i innehållet.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>position) </li> <li> **pulsslag:**<br/> (<code>l:stream:kapitel_pos)</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Kapitelposition </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>position) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>position) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/>media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.index</li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.chapterDetails.index </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.chapterDetails.index </li> </ul> |

### Kapitelavstånd

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API-nyckel:**<br/> media.chapter.offset </li> <li> **Obligatoriskt:**<br/> SDK: Nej; API: Ja. </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stänga kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> 58 </li><li> **Beskrivning:**<br/> Kapitlets förskjutning i innehållet (i sekunder) från början.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>förskjutning) </li> <li> **pulsslag:**<br/> (<code>l:stream:kapitel_offset)</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Kapitelförskjutning </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>förskjutning) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>förskjutning) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/>media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.offset</li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.chapterDetails.offset </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.chapterDetails.offset </li> </ul> |

### Kapitellängd

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.chapter.length </li> <li> **Obligatoriskt:**<br/> SDK: Nej; API: Ja. </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stänga kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> 486 </li><li> **Beskrivning:**<br/> Kapitelns längd i sekunder.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>längd) </li> <li> **pulsslag:**<br/> (<code>l:stream:kapitel_length</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Kapitellängd </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>längd) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>längd) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/>media.mediaTimed.mediaChapter.<br/>chapterAssetReference.xmpDM:duration</li> <li> **Sökväg till XDM-samlingsfält:**<br/> mediaCollection.chapterDetails.length </li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.chapterDetails.length </li> </ul> |

### Kapitel

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ange automatiskt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Stänga kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Kapitelets autogenererade ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>namn) </li> <li> **pulsslag:**<br/> (<code>s:stream:kapitel_id)</code>) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfaller:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Kapitel </li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>namn) </li> <li> **Datafeed:**<br/> videokort </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>namn) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/>media.mediaTimed.mediaChapter.<br/>chapterAssetReference.@id</li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.chapterDetails.ID </li> </ul> |

## Kapitelmått {#chapter-Metrics}

### Kapitelstart

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ange automatiskt  </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Stänga kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet kapitel startar.  **Viktigt!** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>vy) </li> <li> **pulsslag:**<br/> (<code>s:event:)</code><br/>type=kapitel_start) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Kapitel börjar</li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>vy) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>vy) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/>media.mediaTimed.chapterCount.<br/>värde > 0 => &quot;TRUE&quot;</li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.chapterDetails.isStarted </li> </ul> |

### Kapitel slutfört

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ange automatiskt  </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Stänga kapitel </li> <li> **Min. SDK-version:** 1.3</li> <li> **Exempelvärde:**<br/> TRUE </li><li> **Beskrivning:**<br/> Antalet kapitel har slutförts.  **Viktigt!** Om den här händelsen anges är det enda möjliga värdet SANT. Om den här händelsen inte anges skickas inget värde.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>slutförd) </li> <li> **pulsslag:**<br/> (<code>s:event:)</code><br/>type=kapitel_complete) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Kapitel slutförs</li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>slutförd) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>slutförd) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/>media.mediaTimed.mediaChapter.<br/>complete.value</li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.chapterDetails.isCompleted </li> </ul> |

### Kapiteltid spenderad

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK-nyckel:**<br/> Ange automatiskt  </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> tal </li> <li> **Skickat med:**<br/> Stänga kapitel </li> <li> **Min. SDK-version:** 1.3 </li> <li> **Exempelvärde:**<br/> </li><li> **Beskrivning:**<br/> Den tid som har ägnats åt kapitlet.  Värdet visas i tidsformat (<code>HH:MM:SS)</code>) i Analysis Workspace. I Data Feeds, Data Warehouse och Reporting API:er visas värdena på några sekunder.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **pulsslag:**<br/> </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Kapiteltid tillagd</li> <li> **Kontextdata:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> <li> **Sökväg till XDM-fält:** (inaktuellt)<br/>media.mediaTimed.mediaChapter.<br/>timePlayed.value</li> <li> **Rapporterar XDM-fältsökväg:**<br/> mediaReporting.chapterDetails.timePlayed </li> </ul> |

## Relaterade API:er {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* JavaScript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)

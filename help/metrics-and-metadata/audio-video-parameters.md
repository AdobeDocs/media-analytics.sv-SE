---
title: Parametrar för ljud och video
description: Lär dig mer om ljud- och videoinnehållsdata och kontextdatavärden.
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
exl-id: 9dc84377-6eca-482f-89e7-c4008d1c0f07
source-git-commit: 6b3a77d470605047d0d118de379801a3ed645800
workflow-type: tm+mt
source-wordcount: '6229'
ht-degree: 2%

---

# Parametrar för ljud och video{#audio-and-video-parameters}

I det här avsnittet finns en lista med ljud- och videoinnehållsdata, inklusive kontextdatavärden, som Adobe samlar in via lösningsvariabler.

>[!IMPORTANT]
>
>Den 7 februari 2019 släppte Adobe Analytics for Video and Audio en namnändring. <i>Medieinitierarna </i> kallas nu  <i>Media Starts</i>. Denna ändring gjordes för att återspegla branschstandarder i mätvärden och rapporter och för att göra mätvärdena lätt att identifiera vid rapportering.

>[!NOTE]
>
>Från och med den 13 september 2018 ändrades etiketterna för vissa dimensioner, mätvärden och rapporter så att det gick att spåra video- och ljudanalyser i olika innehåll. Etiketterna som har ändrats är: *videon initierar* till *media initierar*, *videolängd* till *innehållslängd* och *videonamn* till *innehållsnamn*. Videorapporter i Reports and Analytics har uppdaterats för att använda namnet&quot;Media&quot; i stället för&quot;Video&quot;. Etikettändringarna ändrade inte datainsamling eller historikdata. Observera dessa ändringar om du använder dem i Report Builder eller i andra externa automatiserade datatunkter som kan påverkas av ändringen.

Beskrivning av tabelldata:

* **implementering:** information om implementeringsvärden och -krav
   * *Key*  - Variable, ange antingen manuellt i appen eller automatiskt med Adobe Media SDK.
   * *Obligatoriskt*  - Anger om parametern krävs för grundläggande ljud- och videospårning.
   * *Typ*  - Anger vilken typ av variabel som ska anges, strängen eller talet.
   * *Skickat med*  - Anger när data skickas:  *Media* Startis the analytics call sent on media start,  *Ad* Startis, the analytics call sent on ad ad start osv. &quot; ** Closecalls&quot; är de kompilerade analysanrop som skickas direkt från hjärtslagservern till analysservern i slutet av mediesessionen, eller i slutet av annonsen, kapitlet osv. Stäng anrop är inte tillgängliga i nätverkspaketanrop.
   * *Min. SDK-version* - Anger vilken SDK-version du behöver för att komma åt parametern.
   * *Exempelvärde*  - innehåller exempel på vanlig variabelanvändning.
* **Nätverksparametrar:** Visar värden som skickas till Adobe Analytics- eller pulsslagservrar. I den här kolumnen visas namnen på de parametrar som visas i nätverksanrop som genereras av Adobe Media SDK:er.
* **Rapportering:** Information om hur du visar och analyserar ljud- och videodata.
   * *Tillgängligt*  - Anger om data är tillgängliga i rapporter som standard (*Ja*) eller om det krävs anpassad konfiguration (*Anpassad*)
   * *Reserverad variabel*  - Anger om data har fångats in som en händelse, eVar, prop eller klassificering i en reserverad variabel.
   * *Förfallotid*  - Anger om data förfaller efter varje träff eller efter varje besök.
   * *Rapportnamn*  - Namn på analysrapport för Adobe för variabel
   * *Kontextdata*  - Namn på Adobe Analytics-kontextdata som skickas till rapportservern och används i bearbetningsregler.
   * *Datafeed*  - kolumnnamn för variabel som hittas i Clickstream- eller Live Stream-dataflöden
   * *Audience Manager* - Trait name found in Adobe Audience Manager

>[!IMPORTANT]
>
>Ändra inte klassificeringsnamnen för de variabler som listas nedan och som beskrivs under Rapportera/Reserverad variabel som &quot;klassificering&quot;.\
>Medieklassificeringarna definieras när en rapportsserie aktiveras för mediespårning. Ibland lägger Adobe till nya egenskaper och när detta inträffar måste kunderna återaktivera sina rapporteringsprogram för att få tillgång till de nya medieegenskaperna. Under uppdateringsprocessen avgör Adobe om klassificeringarna är aktiverade genom att kontrollera namnen på variablerna. Om någon av dem saknas lägger Adobe till de saknade igen.

## Kärnströmningsmediedata {#core-audio-and-video-data}

### Strömtyp {#stream-type}

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> [mediaType](./audio-video-parameters.md#create-media-object) </li> <li> **API-nyckel:**<br/> media.streamType </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 2.2 <br/><br/>Finns i [Översikt över API:t för mediainsamling](/help/media-collection-api/mc-api-overview.md) eller [Hämta SDK:er - Version 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Exempelvärde:**<br/> &quot;video&quot; </li> <li> **Beskrivning:**<br/> Identifierar strömtypen. Giltiga värden är &quot;audio&quot;, &quot;video&quot; och &quot; &quot;.  <br/><br/>[Rapporteringssegment](/help/metrics-and-metadata/segments.md):  <br/><br/>Medieströmtyp: Alla -  <br/>Segmentera alla medieströmdata. Regel: Innehållet (ID) finns  <br/><br/>i medieströmstypen: Ljud -  <br/>Segmentera alla ljudströmsdata; Regel: Innehåll (ID) finns OCH Medieströmtyp = typ av  <br/><br/>ljudmedieström: &quot;Video&quot; -  <br/>Segmentera alla videoströmsdata. Regel: Innehåll (ID) finns OCH medieströmtyp != ljud <br/><br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.streamType) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Strömtyp </li> <li> **Kontextdata:**<br/> (a.media.streamType) </li> <li> **datafeed:**<br/> videoströmtyp </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### Innehålls-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API-nyckel:**<br/> media.id </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;4586695ABC&quot; </li> <li>**Beskrivning:Innehållets**<br/> innehålls-ID, som kan användas för att knyta tillbaka till andra bransch-/CMS-ID:n, som är lika med det sista värdet av  `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **pulsslag:**<br/> (er:resurs:video_id) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **förfallodatum:**<br/> Vid besök </li> <li> **rapportnamn:**<br/> innehåll </li> <li> **Kontextdata:**<br/> (a.media.name) </li> <li> **datafeed:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Innehållslängd (variabel)

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-nyckel:**<br/> media.length </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> VOD: 128; Live: 86400, Linjär: 1800. </li><li> **Beskrivning:**<br/> Klipplängd/körningsmiljö - Detta är den maximala längden (eller längden) för det innehåll som används (i sekunder). Det är lika med det sista värdet på `l:asset:length` från händelser av typen Main. <br/>Om  `l:asset:length` inte anges  `l:asset:duration` används det sista värdet för. <br/>I rapporter är Videolängd klassificeringen och Innehållslängd (variabel) är eVar.   <br/> **Viktigt:** Den här egenskapen används för att beräkna flera mätvärden, till exempel förloppsspårningsvärden och medelvärdespublik. Om detta inte anges, eller inte är större än noll, är dessa värden inte tillgängliga.  För Live-media med okänd längd är värdet 86400 standardvärdet. <br/>Före version 1.5.1 var detta  `l:asset:duration`; efter 1.5.1,  `l:asset:length.` <br/> **Releasedatum: 09/13/18** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Hjärtslag:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> innehållslängd (variabel) </li> <li> **Kontextdata:**<br/> (a.media.length) </li> <li> **datafeed:**<br/> videolängd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Videolängd

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API-nyckel:**<br/> media.length </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> VOD: 128; Live: 86400, Linjär: 1800. </li> <li> **Beskrivning:**<br/> Klipplängd/körningsmiljö - Detta är den maximala längden (eller längden) för det innehåll som används (i sekunder). Det är lika med det sista värdet på `l:asset:length` från händelser av typen Main. Om `l:asset:length` inte är inställt används det sista värdet på `l:asset:duration`. I rapporter är Videolängd klassificeringen och Innehållslängd (variabel) är eVar.  <br/> **Viktigt:** Den här egenskapen används för att beräkna flera mätvärden, till exempel förloppsspårningsvärden och medelvärdespublik. Om detta inte anges, eller inte är större än noll, är dessa värden inte tillgängliga.  För Live-media med okänd längd är värdet 86400 standardvärdet. Före version 1.5.1 var detta `l:asset:duration`; efter 1.5.1 är detta `l:asset:length.`<br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Hjärtslag:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> videolängd </li> <li> **Kontextdata:**<br/> (a.media.length) </li> <li> **datafeed:**<br/> video.videoClassificationLength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Innehållstyp

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API-nyckel:**<br/> media.contentType </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> begränsad sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;vod&quot; </li> <li> **Beskrivning:**<br/> Tillgängliga värden per  **strömtyp**:  <br/> _Ljud:_ &quot;låt&quot;,&quot;poddsändning&quot;,&quot;ljudbok&quot;,&quot;radio&quot;  <br/> _Video:_ &quot;VoD&quot;,&quot;Live&quot;,&quot;Linear&quot;,&quot;UGC&quot;,&quot;DVoD&quot;- <br/> kunder kan ange anpassade värden för den här parametern. Detta är lika med `s:stream:type.` Om detta inte anges är det lika med `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.contentType) </li> <li> **Hjärtslag:**<br/> (s:stream:type) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> innehållstyp </li> <li> **Kontextdata:**<br/> (a.contentType) </li> <li> **datafeed:**<br/> videoinnehålltyp </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID för mediesession

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> hämtad från serverdel </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **text:**<br/> tal </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.8 </li> <li> **Exempelvärde:**<br/> 1482236761294786918253 </li> <li> **Beskrivning:**<br/> Detta identifierar en instans av en innehållsström som är unik för en enskild uppspelning.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.vsid) </li> <li> **pulsslag:**<br/> (s:event:sid) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd bearbetningsregel </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.vsid) </li> <li> **datafeed:**<br/> videosessionid </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### Flagga för hämtning av media

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> `config.downloadedcontent` </li> <li> **API-nyckel:**<br/> hämtad från serverdel </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> boolesk </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** <br/>Starta Android- och iOS-tillägg v1.1.0 </li> <li> **Exempelvärde:**<br/> true </li> <li> **Beskrivning:**<br/> Ange som true när träffen genereras på grund av uppspelning av en hämtad mediesession. Finns inte när det hämtade innehållet inte spelas upp.<br/><br/>[Starta](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.downloaded) </li> <li> **pulsslag:**<br/> (s:meta:a.media.downloaded) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.downloaded) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.downloaded) </li> </ul> |

### Innehållsspelarens namn

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API-nyckel:**<br/> media.playerName </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;Brightcove&quot; </li> <li> **Beskrivning:**<br/> Spelarens namn.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>playerName) </li> <li> **Hjärtslag:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Innehållsspelarens namn </li> <li> **Kontextdata:**<br/> (a.media.playerName) </li> <li> **datafeed:**<br/> videouppspelningsnamn </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Innehållskanal

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [kanal](./audio-video-parameters.md#config-media-object) </li> <li> **API-nyckel:**<br/> media.channel </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;Idrott&quot; </li> <li> **Beskrivning:**<br/> Distributionsstation/kanaler eller var innehållet spelas upp. Alla strängvärden accepteras här.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.channel) </li> <li> **Hjärtslag:**<br/> (s:sp:channel) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> innehållskanal </li> <li> **Kontextdata:**<br/> (a.media.channel) </li> <li> **datafeed:**<br/> videochchannel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Innehållssegment

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Ja </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;0-10&quot; </li> <li> **Beskrivning:**<br/> Intervallet som beskriver den del av innehållet som har visats (i minuter). Segmentet beräknas som min och max för spelhuvudets värden under en uppspelningssession.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> innehållssegment </li> <li> **Kontextdata:**<br/> (a.media.segment) </li> <li> **datafeed:**<br/> videosegment </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segment) </li> </ul> |

### Innehållsnamn (variabel)

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API-nyckel:**<br/> media.name </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.1 </li> <li> **Exempelvärde:**<br/> &quot;The Big Bang Theory&quot; </li> <li> **Beskrivning:**<br/> Det här är det&quot;läsbara&quot; (läsbara) namnet på innehållet, som är lika med det sista värdet i  `s:asset:name.`<br/>I-rapportering, videonamnet är klassificeringen och innehållsnamnet (variabel) är eVar.  <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **Hjärtslag:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Innehållsnamn (variabel) </li> <li> **Kontextdata:**<br/> (a.media.friendlyName) </li> <li> **datafeed:**<br/> videonamn </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Videonamn

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API-nyckel:**<br/> media.name </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.1 </li> <li> **Exempelvärde:**<br/> &quot;The Big Bang Theory&quot; </li> <li> **Beskrivning:**<br/> Det här är det&quot;läsbara&quot; (läsbara) namnet på innehållet, som är lika med det sista värdet i  `s:asset:name.` <br/>I-rapportering, videonamnet är klassificeringen och innehållsnamnet (variabel) är eVar.   <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **Hjärtslag:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> videonamn </li> <li> **Kontextdata:**<br/> (a.media.friendlyName) </li> <li> **datafeed:**<br/> video.videoClassificationName </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Videosökväg

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> &quot;4586695ABC&quot; </li> <li> **Beskrivning:**<br/> Gör det möjligt att spåra sökvägen till ett visningsprogram på en webbplats och/eller i en app för att se sökvägen som de valde för att visa en viss video. Valfri kombination av heltal och/eller bokstav.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **pulsslag:**<br/> (er:resurs:video_id) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> prop </li> <li> **rapportnamn:**<br/> videosökväg </li> <li> **Kontextdata:**<br/> (a.media.name) </li> <li> **datafeed:**<br/> videosökväg </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

### SDK-version

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API-nyckel:**<br/> media.sdkVersion </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;2.62.0_release&quot; </li> <li> **Beskrivning:SDK-**<br/> versionen som används av spelaren. Detta kan ha vilket värde som helst som passar din spelare. <br/><br/>Kunderna måste skapa egna bearbetningsregler för att kunna rapportera värdet.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>sdkVersion) </li> <li> **Hjärtslag:**<br/> (s:sp:sdk) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.sdkVersion) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL-version

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;js-2.0.1.88-c8c0b1&quot; </li> <li> **Beskrivning:**<br/> Den Media SDK-version som används för spårningssessionen. <br/><br/>Kunderna måste skapa egna bearbetningsregler för att kunna rapportera värdet.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vhlVersion) </li> <li> **Hjärtslag:**<br/> (s:sp:hb_version) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.vhlVersion) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Standard Streaming Media-metadata {#standard-audio-and-video-metadata}

### Visa

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> VISA </li> <li> **API-nyckel:**<br/> media.show </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;Modern Family&quot; &quot;The Last Dance&quot; &quot;New Girl&quot; </li> <li> **Beskrivning:**<br/> Program-/ <br/>serienamn krävs bara om programmet ingår i en serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.show) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> Visa </li> <li> **Kontextdata:**<br/> (a.media.show) </li> <li> **datafeed:**<br/> videoshow </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.show) </li> </ul> |

### Strömformat

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> STREAM_FORMAT </li> <li> **API-nyckel:**<br/> media.streamFormat </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;HD&quot; </li> <li> **Beskrivning:Strömmens**<br/> format (HD, SD)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.format) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.format) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.format) </li> </ul> |

### Säsong

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> SEASON </li> <li> **API-nyckel:**<br/> media.säsong </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;2&quot; </li> <li> **Beskrivning:**<br/> Det årstid som programmet tillhör.  Säsongsserie krävs bara om programmet ingår i en serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.säsong) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.säsong) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Säsong </li> <li> **Kontextdata:**<br/> (a.media.säsong) </li> <li> **datafeed:**<br/> videosäsong </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.säsong) </li> </ul> |

### Episod

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> EPISODE </li> <li> **API-nyckel:**<br/> media.episode </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;13&quot; </li> <li> **Beskrivning:**<br/> Antal avsnitt.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.episode) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> avsnitt </li> <li> **Kontextdata:**<br/> (a.media.episode) </li> <li> **datafeed:**<br/> videoavsnitt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.episode) </li> </ul> |

### Tillgångs-ID

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> ASSET_ID </li> <li> **API-nyckel:**<br/> media.assetId </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;89745363&quot; </li> <li> **Beskrivning:**<br/> Det här är den unika identifieraren för mediematerialet, till exempel TV-seriens avsnittsidentifierare, filmresursidentifierare eller live-händelseidentifierare. Vanligtvis härleds dessa ID:n från metadatautfärdare som EIDR, TMS/Gracenote eller Rovi. Dessa identifierare kan också komma från andra egenutvecklade eller interna system.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.asset) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **rapportnamn:**<br/> resurs-ID </li> <li> **Kontextdata:**<br/> (a.media.asset) </li> <li> **datafeed:**<br/> video.videoklassificeringassetid </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Genre

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> GENRE </li> <li> **API-nyckel:**<br/> media.genre </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;Drama&quot;,&quot;Comedy&quot; </li> <li> **Beskrivning:**<br/> Typ eller gruppering av innehåll enligt definition av innehållsproducent. Värdena ska vara kommaavgränsade i variabel implementering. Vid rapportering delas listvärdet upp i en radpost, där varje radartikel får samma eVar.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.genre) </li> <li> **hjärtsslag:**<br/> (s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:eVar**<br/> Lista </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Genre </li> <li> **Kontextdata:**<br/> (a.media.genre) </li> <li> **datafeed:**<br/> videogener </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Första AIR-datum

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> FIRST_AIR_DATE </li> <li> **API-nyckel:**<br/> media.firstAirDate </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;2016-01-25&quot; </li> <li> **Beskrivning:**<br/> Det datum då innehållet först skrevs på tv. Alla datumformat kan accepteras, men Adobe rekommenderar: YYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.airDate) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> första AIR-datum </li> <li> **Kontextdata:**<br/> (a.media.airDate) </li> <li> **datafeed:**<br/> video.videoClassificationDate </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Första digitala datum

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> FIRST_DIGITAL_DATE </li> <li> **API-nyckel:**<br/> media.firstDigitalDate </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;2016-01-25&quot; </li> <li> **Beskrivning:**<br/> Det datum då innehållet först skrevs på en digital kanal eller plattform. Alla datumformat kan accepteras, men Adobe rekommenderar: YYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.digitalDate) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> första digitalt datum </li> <li> **Kontextdata:**<br/> (a.media.digitalDate) </li> <li> **datafeed:**<br/> video.videoclassificationdigitaldate </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Innehållsklassificering

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> KLASSIFICERING </li> <li> **API-nyckel:**<br/> media.rating </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> TVY, TVG, TVPG, TVMA </li> <li> **Beskrivning:**<br/> Klassificering enligt definition i TV:s föräldrariktlinjer.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.rating) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **rapportnamn:**<br/> innehållsklassificering </li> <li> **Kontextdata:**<br/> (a.media.rating) </li> <li> **datafeed:**<br/> video.videoClassification </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Originator

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> ORIGINATOR </li> <li> **API-nyckel:**<br/> media.originator </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;Warner Brothers&quot;,&quot;Sony&quot;,&quot;Disney&quot; </li> <li> **Beskrivning:Innehållets**<br/> skapare.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.originator) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> Klassificering </li> <li> **Rapportnamn:**<br/> Originator </li> <li> **Kontextdata:**<br/> (a.media.originator) </li> <li> **Datafeed:**<br/> video.videoClassificationOriginator </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Nätverk

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> NÄTVERK </li> <li> **API-nyckel:**<br/> media.network </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;Fox&quot;,&quot;Bravo&quot;,&quot;ESPN&quot; </li> <li> **Beskrivning:**<br/> Namnet på nätverket/kanalen.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.network) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> nätverk </li> <li> **Kontextdata:**<br/> (a.media.network) </li> <li> **dataflöde:**<br/> videonätverk </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.network) </li> </ul> |

### Visa typ

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> SHOW_TYPE </li> <li> **API-nyckel:**<br/> media.showType </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;0&quot; = Hela avsnittet; &quot;1&quot; = Preview/trailer; &quot;2&quot; = Clip; &quot;3&quot; = Annat. </li> <li> **Beskrivning:**<br/> Innehållstyp, uttryckt som ett heltal mellan 0 och 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.type) </li> <li> **hjärtsslag:**<br/> (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> Visa typ </li> <li> **Kontextdata:**<br/> (a.media.type) </li> <li> **datafeed:**<br/> videoshowtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> MVPD </li> <li> **API-nyckel:**<br/> media.pass.mvpd </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;Comcast&quot;, &quot;DirecTV&quot;, &quot;Dish&quot; </li> <li> **Beskrivning:**<br/> MVPD tillhandahålls via autentisering via Adobe.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.mvpd) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> MVPD </li> <li> **Kontextdata:**<br/> (a.media.pass.mvpd) </li> <li> **datafeed:**<br/> videomvpd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Auktoriserad

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> AUKTORISERAD </li> <li> **API-nyckel:**<br/> media.pass.auth </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;TRUE&quot; </li> <li> **Beskrivning:**<br/> Användaren har autentiserats via Adobe.  <br/>**Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.auth) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> auktoriserat </li> <li> **Kontextdata:**<br/> (a.media.pass.auth) </li> <li> **datafeed:**<br/> videoauktoriserad </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Dag - del

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> DAY_PART </li> <li> **API-nyckel:**<br/> media.dayPart </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> </li> <li> **Beskrivning:**<br/> En egenskap som definierar tiden på dagen då innehållet sändes eller spelades upp. Detta kan ha vilket värde som helst som kunderna behöver.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.dayPart) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> dagdel </li> <li> **Kontextdata:**<br/> (a.media.dayPart) </li> <li> **datafeed:**<br/> videodaypart </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Medieflödestyp

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> FEED </li> <li> **API-nyckel:**<br/> media.feed </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 </li> <li> **Exempelvärde:**<br/> &quot;East-HD&quot;,&quot;West-HD&quot;,&quot;East-SD&quot; </li> <li> **Beskrivning:**<br/> Typ av feed.   <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.feed) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> medieflödstyp </li> <li> **Kontextdata:**<br/> (a.media.feed) </li> <li> **datafeed:**<br/> videofeedtyp </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Konstnär

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.artist </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 <br/>Finns i [Översikt över mediesamling](/help/media-collection-api/mc-api-overview.md) eller [Hämta SDK:er - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exempelvärde:**<br/> &quot;The Beatles&quot; </li> <li> **Beskrivning:artistens**<br/> namn.   <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.artist) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.artist) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> artist</li> <li> **Kontextdata:**<br/> (a.media.artist) </li> <li> **datafeed:**<br/> videoartist </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.artist) </li> </ul> |

### Album

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.album </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 <br/>Finns i [Översikt över mediesamling](/help/media-collection-api/mc-api-overview.md) eller [Hämta SDK:er - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exempelvärde:**<br/> &quot;Kretslopp&quot; </li> <li> **Beskrivning:**<br/> Albumets namn.   <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.album) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> album </li> <li> **Kontextdata:**<br/> (a.media.album) </li> <li> **datafeed:**<br/> videoalbum </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.album) </li> </ul> |

### Etikett

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.label </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 <br/>Finns i [Översikt över mediesamling](/help/media-collection-api/mc-api-overview.md) eller [Hämta SDK:er - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exempelvärde:**<br/> &quot;Kretslopp&quot; </li> <li> **Beskrivning:**<br/> Namn på postetiketten.   <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.label) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> etikett</li> <li> **Kontextdata:**<br/> (a.media.label) </li> <li> **datafeed:**<br/> videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.label) </li> </ul> |

### Upphovsman

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.author </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 <br/>Finns i [Översikt över mediesamling](/help/media-collection-api/mc-api-overview.md) eller [Hämta SDK:er - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exempelvärde:**<br/> &quot;John Kennedy Toole&quot; </li> <li> **Beskrivning:Författarens**<br/> namn (i en ljudbok).   <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.author) </li> <li> **Hjärtslag:**<br/> (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> författare </li> <li> **Kontextdata:**<br/> (a.media.author) </li> <li> **datafeed:**<br/> videoförfattare </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.author) </li> </ul> |

### Station

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.station </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 <br/>Finns i [Översikt över mediesamling](/help/media-collection-api/mc-api-overview.md) eller [Hämta SDK:er - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exempelvärde:**<br/> &quot;NPR&quot; </li> <li> **Beskrivning:**<br/> Namn/ID för radiostationen.   <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.station) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **rapportnamn:**<br/> station </li> <li> **Kontextdata:**<br/> (a.media.station) </li> <li> **datafeed:**<br/> videostation </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.station) </li> </ul> |

### Utgivare

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> </li> <li> **API-nyckel:**<br/> media.publisher </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:**<br/> Mediestart, mediestängning </li> <li> **Min. SDK-version:** 1.5.7 <br/>Finns i [Översikt över mediesamling](/help/media-collection-api/mc-api-overview.md) eller [Hämta SDK:er - Version 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exempelvärde:**<br/> &quot;Random Bauhaus&quot; </li> <li> **Beskrivning:**<br/> Namnet på ljudinnehållsutgivaren.   <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.publisher) </li> <li> **pulsslag:**<br/> (s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **Förfallotid:**<br/> vid HIT </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.publisher) </li> <li> **datafeed:**<br/> videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.publisher) </li>  </ul> |

## Streaming Media Metrics {#audio-and-video-metrics}

### Media börjar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven</li> <li> **API-nyckel:**<br/> Ej tillämpligt</li> <li> **Typ:**<br/> sträng</li> <li> **Skickat med:**<br/> Mediestart</li> <li> **Min. SDK-version:** Alla</li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:händelsen**<br/> Load för mediet. (Detta inträffar när användaren klickar på knappen _Spela upp_). Detta skulle räknas även om det finns annonser före rullning, buffring, fel och så vidare.  <br/>**Viktigt:**  Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.view) </li> <li> **pulsslag:**<br/> (s:event:<br/>type=start) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Media börjar </li> <li> **Kontextdata:**<br/> (a.media.view) </li> <li> **datafeed:**<br/> videostart </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.view) </li> </ul> |

### Innehållet börjar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:Den**<br/> första bildrutan med media används. Om användaren hoppar under annons, buffring osv. så finns det ingen händelse av&quot;Innehållsstart&quot;.  <br/> **Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> innehållet börjar </li> <li> **Kontextdata:**<br/> (a.media.play) </li> <li> **datafeed:**<br/> videouppspelning </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.play) </li> </ul> |

### Innehållet är klart {#content-complete}

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:**<br/> En direktuppspelning som bevakades tills den slutfördes. Detta innebär inte nödvändigtvis att användaren tittade på eller lyssnade på hela strömmen. de kunde ha hoppat över i förväg. Detta innebär bara att användaren har nått slutet av strömmen, 100 %. <br/>Se även  [Sessionsslut](quality-parameters.md#session-end) <br/> **Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **pulsslag:**<br/> (s:event:<br/>type=complete) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> innehållet har slutförts </li> <li> **Kontextdata:**<br/> (a.media.complete) </li> <li> **datafeed:**<br/> videocomplete   </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.complete) </li> </ul> |

### Innehållstid

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 105 </li> <li> **Beskrivning:**<br/> Summerar händelsens varaktighet (i sekunder) för alla händelser av typen PLAY i huvudinnehållet.  Värdet visas i tidsformat (HH:MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder.  <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> använd innehållstid </li> <li> **Kontextdata:**<br/> (a.media.timePlay) </li> <li> **datafeed:**<br/> videotid </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.timePlay) </li> </ul> |

### Medietid tillagd

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 120 </li> <li> **Beskrivning:**<br/> Summerar händelsens varaktighet (i sekunder) för alla händelser av typen PLAY, både huvud- och annonsinnehåll.  Värdet visas i tidsformat (HH:MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder.  <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> medietid </li> <li> **Kontextdata:**<br/> (a.media.totalTimePlayed) </li> <li> **datafeed:**<br/> videosumtid </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Unik speltid

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 94 </li> <li> **Beskrivning:**<br/> Värdet i sekunder för de unika innehållssegmenten som spelas upp under en session. Undvik den tid som spelas upp vid sökningsscenarier där ett visningsprogram ser samma segment av innehållet flera gånger.  Värdet visas i tidsformat (HH:MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder.  <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> unik uppspelningstid </li> <li> **Kontextdata:**<br/> (a.media.uniqueTimePlayed) </li> <li> **datafeed:**<br/> videoredigering </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### Tio % statusmarkör

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:**<br/> Spelhuvudet skickar 10 %-markören med innehåll baserat på längd. Markören räknas bara en gång, även om du söker bakåt. Om du söker framåt räknas inte markörer som hoppas över.  <br/> **Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> 10 % förloppsmärke </li> <li> **Kontextdata:**<br/> (a.media.progress10) </li> <li> **datafeed:**<br/> videoprogress10 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### Förloppsmärke på 25 %

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:**<br/> Spelhuvudet skickar 25 %-markören med innehåll baserat på innehållets längd. Markören räknades bara en gång, även om den söker bakåt. Om du söker framåt räknas inte markörer som hoppas över.  <br/> **Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> 25 % förloppsmärke </li> <li> **Kontextdata:**<br/> (a.media.progress25) </li> <li> **datafeed:**<br/> videoprogress25 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### Förloppsmärke på 5 %

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:**<br/> Spelhuvudet skickar en 50-procentig markör med innehåll baserat på innehållets längd. Markören räknades bara en gång, även om den söker bakåt. Om du söker framåt räknas inte markörer som hoppas över.  <br/> **Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> 50 % förloppsmärke </li> <li> **Kontextdata:**<br/> (a.media.progress50) </li> <li> **datafeed:**<br/> videoprogress50 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### Sjuttiofem % Progress Marker

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> **Ej tillämpligt** </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:**<br/> Spelhuvudet skickar en 75 %-markör med innehåll baserat på innehållets längd. Markören räknades bara en gång, även om den söker bakåt. Om du söker framåt räknas inte markörer som hoppas över.  <br/> **Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> 75 % förloppsmärke </li> <li> **Kontextdata:**<br/> (a.media.progress75) </li> <li> **datafeed:**<br/> videoprogress75 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### 95 % förloppsmärke

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:**<br/> Spelhuvudet skickar 95 %-markeringen av innehållet baserat på innehållets längd. Markören räknades bara en gång, även om den söker bakåt. Om du söker framåt räknas inte markörer som hoppas över.  <br/> **Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> 95 % förloppsmärke </li> <li> **Kontextdata:**<br/> (a.media.progress95) </li> <li> **datafeed:**<br/> videoprogress95 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Genomsnittlig målgrupp i minuter

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> större än eller lika med 1 </li> <li> **Beskrivning:**<br/> Mått för genomsnittlig minutpublik beräknas som Total Content Time Spent, för ett visst medieobjekt, dividerat med längden för alla uppspelningssessioner:  <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> genomsnittlig minutpublik </li> <li> **Kontextdata:**<br/> (a.media.AverageMinuteAudience) </li> <li> **datafeed:**<br/> videoaverageminutepublik </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.AverageMinuteAudience) </li> </ul> |

### Sekunder sedan senaste samtal

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 600</li> <li> **Beskrivning:**<br/> Sekunder sedan senaste anropsmåttet är 0 om strömmen stängdes med en complete-händelse eller med en end-händelse och är vanligtvis 600 om den stängdes på grund av timeout. Det här måttet har ingen lösningsvariabel och regler för automatisk bearbetning, så du måste skapa en anpassad bearbetningsregel för att kunna spara den.</li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Eget</li> <li> **Kontextdata:**<br/> (a.media.secondsSinceLastCall) </li> <li> **dataflöde:**<br/> videosekundssincelastcall </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.secondsSinceLastCall) </li> </ul> |

### Federerade data

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> boolesk </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> true  </li> <li> **Beskrivning:**<br/> Ange som true när träffen är federerad (d.v.s. tas emot av kunden som en del av en federerad datadelning, i stället för som en egen implementering). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Ej tillämpligt </li> <li> **Kontextdata:**<br/> (a.media.federated) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.federated) </li> </ul> |

### Uppskattade strömmar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 1 - för 19 minuters uppspelning;  <br/>2 - För 31 minuters uppspelning.  <br/>3 - För en uppspelning på 78 minuter. </li> <li> **Beskrivning:**<br/> Det uppskattade antalet video- eller ljudströmmar per enskilt innehåll. Det här värdet ökas för varje 30 minuters uppspelningstid (innehåll + annonser). Kunderna måste skapa egna bearbetningsregler för att kunna rapportera värdet. <br/><br/>En ström räknas var 30:e minut baserat på  `ms_s` (eller totalTimePlayed = Total tid för video), ungefär som:  <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.stimams) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.stimams) </li> </ul> |

### Pausade påverkade strömmar

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** 1.5.6 </li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:**<br/> Värdet är antingen true eller false. Det är sant om en eller flera pauser inträffar under uppspelning av ett enda medieobjekt.  <br/> **Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **pulsslag:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> pausad påverkad ström </li> <li> **Kontextdata:**<br/> (a.media.pause) </li> <li> **datafeed:**<br/> videopaus </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pause) </li> </ul> |

### Pausa händelser

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** 1.5.6 </li> <li> **Exempelvärde:**<br/> 2 </li> <li> **Beskrivning:**<br/> Det här måttet beräknas som antalet pausperioder som inträffade under en uppspelningssession.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **pulsslag:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> paushändelser </li> <li> **Kontextdata:**<br/> (a.media.pauseCount) </li> <li> **datafeed:**<br/> videomängd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Total pausvaraktighet

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** 1.5.6 </li> <li> **Exempelvärde:**<br/> 190 </li> <li> **Beskrivning:**<br/> Summerar längden (i sekunder) för alla händelser av typen PAUSE. Värdet visas i tidsformat (HH:MM:SS) i Analysis Workspace och Rapporter och analyser. I Data Feeds, Data warehouse och Reporting API:er visas värdena på några sekunder. <br/> **Releasedatum: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **Rapportnamn:**<br/> Total pausvaraktighet </li> <li> **Kontextdata:**<br/> (a.media.pauseTime) </li> <li> **Datafeed:**<br/> (videoOperationTime) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Återuppta innehåll

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> **media.resume** </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** 1.5.6 </li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:**<br/> En Återuppta räknas för varje uppspelning som återupptas efter mer än 30 minuters buffring, paus eller uppehållsperiod ELLER om det här värdet anges av spelaren i VideoInfo trackPlay.  <br/> **Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **pulsslag:**<br/> (s:event:<br/>type=resume) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> Återuppta innehåll </li> <li> **Kontextdata:**<br/> (a.media.resume) </li> <li> **datafeed:**<br/> videoresume </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.resume) </li> </ul> |

### Vyer för innehållssegment

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Automatiskt angiven </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **Typ:**<br/> sträng </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> TRUE </li> <li> **Beskrivning:**<br/> Antalet vyer av huvudinnehållet. En vy för innehållssegment räknas när minst en ram visas.  <br/> **Viktigt:** Detta kan bara vara sant om det är inställt. Om den inte anges returneras inget värde. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> händelse </li> <li> **rapportnamn:**<br/> innehållssegmentvyer </li> <li> **Kontextdata:**<br/> (a.media.segmentView) </li> <li> **datafeed:**<br/> videosegmentvy </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segmentView) </li> </ul> |


### Antal annonser

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ej tillämpligt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 2 </li> <li> **Beskrivning:**<br/> Antalet annonser som startades under mediesessionen.    <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.adCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Antal kapitel

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ej tillämpligt </li> <li> **API-nyckel:**<br/> Ej tillämpligt </li> <li> **text:**<br/> tal </li> <li> **Skickat med:Stäng**<br/> media </li> <li> **Min. SDK-version:** Alla </li> <li> **Exempelvärde:**<br/> 2 </li> <li> **Beskrivning:**<br/> Antalet kapitel som startades under mediesessionen.    <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> Ej tillämpligt </li> <li> **Hjärtslag:**<br/> Ej tillämpligt </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Använd anpassad bearbetningsregel </li> <li> **Reserverad variabel:**<br/> Ej tillämpligt </li> <li> **Rapportnamn:**<br/> Eget </li> <li> **Kontextdata:**<br/> (a.media.chapterCount) </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |


## California Consumer Privacy Act (CCPA) Parametrar {#ccpa-params}

### Avanmäl vidarebefordran på serversidan

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ej tillämpligt </li> <li> **API-nyckel:**<br/> analytics.optOutServerSideForwarding </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> boolesk </li> <li> **Skickat med:**<br/> Mediestart </li> <li> **Min. SDK-version:** Ej tillämpligt </li> <li> **Exempelvärde:**<br/> true </li> <li>**Beskrivning:**<br/> Ange som true när slutanvändaren har valt att inte dela data mellan Adobe Analytics och andra Experience Cloud-lösningar (t.ex. Audience Manager). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.dmp) </li> <li> **pulsslag:**<br/> (s:meta:cm.ssf) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **förfallodatum:**<br/> Vid besök </li> <li> **Rapportnamn:**<br/> Ej tillämpligt </li> <li> **kontextdata:**<br/> Ej tillämpligt </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> Ej tillämpligt </li> </ul> |

### Avanmäl dig från delning

|   Implementering   | Nätverksparametrar | Rapportering |
| --- | --- | --- |
| <ul> <li> **SDK-nyckel:**<br/> Ej tillämpligt </li> <li> **API-nyckel:**<br/> analytics.optOutShare </li> <li> **Obligatoriskt:**<br/> Nej </li> <li> **text:**<br/> boolesk </li> <li> **Skickat med:**<br/> Mediestart </li> <li> **Min. SDK-version:** Ej tillämpligt </li> <li> **Exempelvärde:**<br/> true </li> <li>**Beskrivning:**<br/> Ange som true när slutanvändaren har valt att inte använda data som federeras (t.ex. till andra Adobe Analytics-klienter). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.oos) </li> <li> **pulsslag:**<br/> (s:meta:cm.oos) </li> </ul> | <ul> <li> **Tillgänglig:**<br/> Ja </li> <li> **Reserverad variabel:**<br/> eVar </li> <li> **förfallodatum:**<br/> Vid besök </li> <li> **Rapportnamn:**<br/> Ej tillämpligt </li> <li> **kontextdata:**<br/> Ej tillämpligt </li> <li> **Datafeed:**<br/> Ej tillämpligt </li> <li> **Audience Manager:**<br/> Ej tillämpligt </li> </ul> |

## Relaterade API:er {#section_Related_APIs}

### createMediaObject API:er {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig API:er {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

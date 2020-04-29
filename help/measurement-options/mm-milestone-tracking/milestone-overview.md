---
title: Översikt över milstolpar
description: null
uuid: 2f9ec6bb-8860-4863-98bc-5cffb356ccc5
translation-type: tm+mt
source-git-commit: 5a4f15616712ee91bc028258991fc4e7359698a5

---


# Översikt över milstolpar{#milestone-overview}

>[!CAUTION]
>
>Det här måttalternativet har tagits bort.

[Dokumentation för äldre milstolpe](milestone_analytics_video.pdf)

## Konfiguration {#configuration}

### Videokonfiguration för milstolpe

Om du vill spåra video anger du en uppsättning *anpassade konverteringsvariabler* (eVars) och *anpassade händelser* som ska användas för spårning och rapportering. En *Custom Insight* -variabel ( `s.prop` ) används också för målning.

Variablerna som du väljer för varje mätvärde läggs till på videokonfigurationssidan. På så sätt kan systemet automatiskt generera och formatera standardvideorapporter. Både *videonamnet* eVar och *videovisningsräknaren* krävs. Andra variabler är valfria men rekommenderas för fullständig mätning. När videospårning är aktiverat kan du visa rapporter som genererats från videodata som du har rapporterat med hjälp av videospårning.

Du kan också spåra valfritt antal ytterligare mätvärden för video. Om du till exempel använder flera videospelare på webbplatsen kan du fylla i en eVar med spelarnamnet. Vissa av de variabler du väljer kan också användas i andra delar av webbplatsen. Om den används på hela webbplatsen kan du med variabeln *innehållstyp* mäta vilken procentandel av sidvyerna som kommer från video och låta dig relatera konverteringshändelser till video.

### Konfiguration för milstolprapportering

Om du vill konfigurera videorapportering för en milstolpe-implementering går du till **[!UICONTROL Admin > Report Suite Manager].**Markera rapportsviten och välj sedan**[!UICONTROL Video Management > Video Reporting]:**

<!--
![](assets/0clip_image002_1537416456.png){width="248"}
-->

![](assets/rs1.png)

På den första skärmen fungerar bara Video Core med milstolpe-data. Markera **[!UICONTROL Video Core]** och klicka **[!UICONTROL Save].**

![](assets/video-core-check.png)

På nästa skärm väljer du **[!UICONTROL Use Custom Variables].**

<!--
![](assets/0clip_image006_-1561510960.png){width="470"}
-->

![](assets/rs2.png)

På den sista skärmen väljer du de två eVars och tre händelser som ska användas för videomätningen:

<!--
![](assets/0clip_image008_-92166399.png)
-->

![](assets/rs3.png)

## Variabelreferens för video {#video-variable-reference}

Följande tabell innehåller ytterligare information om e-handelsvariabler och anpassade händelser för video:

| Videomått | Variabeltyp | Beskrivning |
| --- | --- | --- |
| Innehåll | eVar- <br/>standardförfallodatum: Besök | (Obligatoriskt) Samlar in namnet på videon enligt implementeringen. |
| Innehållstyp | eVar- <br/>standardförfallodatum: Sidvy | Samlar in data om den typ av innehåll som visas av en besökare. Träffar som skickas via videomätning tilldelas en innehållstyp för `video.` den <br/>här variabeln och behöver inte reserveras exklusivt för videospårning. Genom att använda samma variabel för andra innehållstyper för innehållsrapporter kan du analysera hur besökarna distribueras över olika typer av innehåll. Du kan till exempel tagga andra innehållstyper med värden som `article` eller `product page` med den här variabeln. <br/>Från ett videomätningsperspektiv kan du med *Content Type* identifiera videobesökare och därmed beräkna videokonverteringsgraden. |
| Innehållstid | Händelsetyp <br/>: Räknare | Räknar den tid (i sekunder) som har ägnats åt att titta på en video sedan den senaste datainsamlingsprocessen (bildbegäran). |
| Videostart | Händelsetyp <br/>: Räknare | Anger att en besökare har visat en del av en video. Den ger dock ingen information om hur mycket, eller vilken del, av en video som besökaren visade. |
| Videon slutförs | Händelsetyp <br/>: Räknare | Anger att en användare har visat en komplett video. Som standard mäts complete-händelsen en sekund före videons slut.  <br/>Under implementeringen kan du ange hur många sekunder från slutet av videon som du vill att en vy ska vara slutförd. För livevideo och andra strömmar som inte har någon definierad ände kan du ange en anpassad punkt för att mäta slutförda data. Till exempel efter en viss tidpunkt. |

## Mediemodvariabler {#media-module-variables}

Med följande variabler kan du konfigurera videomätning. Du måste definiera värden för variablerna i tabellen Obligatoriska variabler. Om du vill spåra händelser i videospelaren måste du aktivera autoTrack (för spelare som stöds) eller implementera anpassad spårning av spelarhändelser med metoderna open, play, stop och close.

| Variabel | Beskrivning |
| --- | --- |
| `Media.trackUsingContextData` | **Syntax:** <br/><br/> `s.Media.trackUsingContextData = true;` Med <br/>det här alternativet aktiveras integrerad videospårning. När värdet är true genererar mediemodulen kontextdata för mediespårning i stället för äldre `pev3`. <br/>Används `Media.contextDataMapping` för att mappa kontextdata till de markerade eVars- och Events-elementen.<br/>Standardvärde: `false` |
| `Media.contextDataMapping` | **Syntax:** <br/><br/> `s.Media.contextDataMapping = {`<br/>      `"a.media.name":"eVar2, prop2",` <br/>     `"a.media.segment":"eVar3",` <br/>     `"a.contentType":"eVar1",` <br/>     `"a.media.timePlayed":"event3",` <br/>     `"a.media.view":"event1",` <br/>     `"a.media.segmentView":"event2",` <br/>     `"a.media.complete":"event7",` <br/>     `"a.media.milestones":{` <br/>         `25:"event4",` <br/>         `50:"event5",` <br/>         `75:"event6"` <br/>     ` }` <br/> `};` <br/><br/>Ett objekt som definierar variabelmappning för eVars och Händelser som du vill använda för videomätning. Objektet måste mappa följande fält: <br/><br/> **a.media.name:** (Obligatoriskt) Fyller variabler med videonamnet. Ange den eVar som du valde för att lagra videonamnet och den Custom Insight Video-variabel ( `s.prop` ) som du vill använda för videopappning. Ange värdena i en kommaavgränsad lista. <br/><br/> **a.media.segment:** (Valfritt) Den eVar som du vill lagra namnet på mediasegmentet. a.contentType: (Valfritt) Den eVar som du vill lagra videovärdet, som innehåller besöks- och besöksspårning aktiverat för att generera videobesök och besöksrapporter. Variabeln du väljer används troligen redan för att lagra data som bildspel för artiklar eller produktsidor <br/><br/> **a.media.view:** (Obligatoriskt) Händelsen som du vill räkna medievyer med. <br/><br/> **a.media.segmentVisa:** (Valfritt) Händelsen som du vill räkna segmentvyer. <br/><br/> **a.media.complete:** (Valfritt) Händelsen som du vill räkna hela vyer. <br/><br/> **a.media.timePlay:** (Valfritt, rekommenderas starkt) Den numeriska händelse som du vill lagra antalet videosekunder som ska spelas upp. <br/><br/> **a.media.millestone:** (Valfritt) Ett objekt som mappar s.Media.trackMilstolpar för att motverka händelser. Media.segmentByMilestone ska anges till true om du definierar milstolpar. <br/><br/> **Annonsspårning** För att spåra annonser finns följande kontextdatavariabler tillgängliga: <br/> **a.media.ad.name:** (Obligatoriskt) Fyller variabler med annonsnamnet. Ange den eVar som du valde för att lagra annonsnamnet och den Custom Insight Video-variabel ( `s.prop` ) som du vill använda för målning. Ange värdena i en kommaavgränsad lista. <br/><br/> **a.media.ad.pod:** Positionen i annonsens primära innehåll spelades upp. <br/><br/> **a.media.ad.podPosition:** Positionen i rutan där annonsen spelas upp. <br/><br/> **a.media.ad.CPM:** CPM eller krypterad CPM (prefix med ett &quot;~&quot;) som gäller för den här uppspelningen. <br/><br/> **a.media.ad.viytt:** Fungerar på samma sätt som `a.media.view`<br/><br/> **a.media.ad.clicked:** Räkna antalet klick för annonsen (`Media.click` anrop) <br/><br/> **a.media.ad.timePlay:** Fungerar på samma sätt som `a.media.timePlayed`<br/><br/> **a.media.ad.comcomplete:** Fungerar på samma sätt som `a.media.complete` a.media.ad.sesection: Fungerar på samma sätt som `a.media.segment`<br/><br/> **a.media.ad.sesegmentView:** Fungerar på samma sätt som `a.media.segmentView`<br/><br/> **a.media.ad.milestone:** Fungerar på samma sätt som `a.media.milestones`<br/><br/> **a.media.ad.offsetMilestone:** Fungerar på samma sätt som `a.media.offsetMilestones` |
| `Media.trackVars` | **Syntax:** <br/><br/> `s.Media.trackVars =` <br/>    `"events,``prop2,` `eVar1,``eVar2,` `eVar3";` <br/><br/>En kommaavgränsad lista med alla variabler som är angivna i videospårningskoden. |
| `Media.trackEvents` | **Syntax:** <br/><br/> `s.Media.trackEvents =` <br/>    `"event1,` `event2,``event3,` `event4,``event5,` `event6,` `event7"` <br/><br/>En kommaavgränsad lista över alla händelser som har angetts i videospårningskoden. |

## Valfria variabler {#optional-variables}

|  Variabel | Beskrivning |
| --- | --- |
| `Media.autoTrack` | **Syntax:** <br/><br/> `s.Media.autoTrack = true` Aktiverar automatisk spårning <br/><br/>för spelare som stöds. Följande spelare stöds: <ul> <li> OSMF (Open Source Media Framework) </li> <li> FLVPlayback (videospelare skapade med guiden Importera video i Flash Professional) </li> <li> Silverlight </li> <li> MediaDisplay </li> <li> MediaPlayback </li> <li> Brightcove API version 2 och 3 (se [Brightcove](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_other_players.html)) </li> <li> Windows Media Player, QuickTime eller Real Player med JavaScript </li> </ul> <br/><br/>Om du inte använder någon av spelarna ovan kan du använda `Media.open``Media.play` för `Media.stop` `Media.close` att spåra spelarhändelser. |
| `Media.autoTrackNetStreams` | **Syntax:** <br/><br/> `s.Media.autoTrackNetStreams = true` I <br/><br/>Flash 10.3 introducerades nya funktioner för NetStream-komponenten som möjliggör förbättrad videospårning. Om du använder en anpassad Flash NetStream-spelare kan du aktivera den här variabeln för att aktivera funktioner som liknar autoTrack. Den här metoden kräver att videoklipp visas i Flash 10.3 eller senare. |
| `Media.completeByCloseOffset` | **Syntax:** <br/><br/> <br/><br/>`s.Media.completeByCloseOffset = true` Med <br/><br/>den här inställningen kan du räkna en komplett videovy några sekunder innan den faktiska slutet av videon.  <br/><br/>Händelsen skickas baserat på antalet sekunder som anges i `completeCloseOffsetThreshold`. Detta gör att du kan mäta resultatet i videospelare som aldrig rapporterar en förskjutning som är lika lång som videon.<br/><br/>Som standard är det här värdet true och tröskelvärdet är 1 sekund. Med dessa standardvärden skickas complete-händelsen en sekund före slutet av videon. |
| `Media.completeCloseOffsetThreshold` | **Syntax:** <br/><br/> `s.Media.completeCloseOffsetThreshold = 1` Med <br/><br/>det här tröskelvärdet kan du räkna en fullständig videovy några sekunder innan den faktiska slutet av videon.  `Media.completeByCloseOffset` måste anges till true för att det här tröskelvärdet ska kunna användas.<br/><br/>Det heltalsvärde du anger avgör hur långt bort i sekunder förskjutningen kan vara från längden på videon vid stängning och ändå räknas som en fullständig. Detta gör att du kan mäta resultatet i videospelare som aldrig rapporterar en förskjutning som är lika lång som videon.  <br/><br/>Standardtröskelvärdet är 1 sekund. |
| `Media.playerName` | **Syntax:** <br/><br/> `s.Media.playerName = "Custom Player Name"` <br/><br/>Anger ett eget videospelarnamn. |
| `Media.trackSeconds` | **Syntax:** <br/><br/> `s.Media.trackSeconds = 15` <br/><br/>Definierar intervallet, i sekunder, för att skicka videospårningsdata till Adobes datainsamlingsservrar medan videon spelas upp. Värdet måste anges i steg om 5 sekunder. <br/><br/> När du aktiverar `Media.trackSeconds` utlöses bara de händelser som är definierade i `Media.contextDataMapping`. Om du vill skicka ytterligare variabler utanför de som angetts för videomätning måste du använda Media.Monitor. |
| `Media.trackMilestones` | Spårar milstolpar i procent av videolängden.  <br/><br/> **Syntax:** <br/><br/> `s.Media.trackMilestones = "25, 50, 75";` <br/><br/>Definierar intervallet, i procent av videolängden, för att skicka videospårningsdata till Adobes datainsamlingsservrar. Ange milstolparna som en kommaavgränsad lista med heltal. Till exempel: 10 = 10 %, 23 = 23 %.  <br/><br/>Eftersom dessa milstolpar är fasta punkter i videon, och besökaren sedan spolar tillbaka och skickar milstolpen 10 % igen, skickas spårningsdata flera gånger i mediemodulen om besökaren tittar förbi milstolpen på 10 %. På samma sätt skickas inte spårningsdata för den milstolpen om en besökare går framåt förbi en milstolpe.  <br/><br/>När du aktiverar `Media.trackMilestones` utlöses bara de händelser som är definierade i `Media.contextDataMapping`. Om du vill skicka ytterligare variabler utanför de som angetts för videomätning måste du använda Media.Monitor. |
| `Media.trackOffsetMilestones` | Spårar milstolpar när sekunder förflutit från videons början.  <br/><br/> **Syntax:** <br/><br/> `s.Media.trackOffsetMilestones = "20, 40, 60";` <br/><br/>Definierar intervallet, i sekunder, från videons början, för att skicka videospårningsdata till Adobes datainsamlingsservrar. Ange milstolparna som en kommaavgränsad lista med heltal. Till exempel: 20 = 20 sekunder, 40 = 40 sekunder).  <br/><br/>Eftersom de här milstolparna är fasta punkter i videon, och besökaren visar över milstolpen på 20 sekunder, sedan spolar tillbaka och skickar milstolpen på 20 sekunder igen, skickas spårningsdata flera gånger i mediemodulen. På samma sätt skickas inte spårningsdata för den milstolpen om en besökare går framåt förbi en milstolpe.  <br/><br/> När du aktiverar `Media.trackOffsetMilestones` utlöses bara de händelser som är definierade i `Media.contextDataMapping`. Om du vill skicka ytterligare variabler utanför de som angetts för videomätning måste du använda Media.Monitor. |
| `Media.segmentByMilestones` | **Syntax:** <br/><br/> `s.Media.segmentByMilestones = true;` Genererar <br/><br/>automatiskt data om segmentnamn, segmentnummer och segmentlängd baserat på mediets längd och de milstolpar som anges i `Media.trackMilestones` Segmentering efter <br/><br/>milstolpar är det enda sättet att definiera segment när `autoTrack`. <br/><br/>Standardvärde: `false` |
| `Media.segmentByOffsetMilestones` | **Syntax:** <br/><br/> `s.Media.segmentByOffsetMilestones = true;` Genererar <br/><br/>automatiskt data om segmentnamn, segmentnummer och segmentlängd baserat på mediets längd och de milstolpar som anges i `Media.trackOffsetMilestones` Segmentering efter <br/><br/>milstolpar är det enda sättet att definiera segment när `autoTrack`.  <br/><br/>Standardvärde: `false` |

## Annonsspårningsvariabler {#ad-tracking-variables}

Dessa variabler används för att skicka annonsinformation tillsammans med metoden openAd. Se [VAST - Spåra videoklipp.](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_ads.html)

| Variabel | Beskrivning |
| --- | --- |
| `Media.adTrackSeconds` | **Syntax:** <br/><br/> `s.Media.adTrackSeconds = 15;` <br/><br/>Definierar intervallet, i sekunder, för att skicka data för video- och spårningsdata till Adobes datainsamlingsservrar medan videon spelas upp. Värdet måste anges i steg om 5 sekunder.  <br/><br/> När du aktiverar `Media.adTrackSeconds` utlöses bara de händelser som är definierade i `Media.contextDataMapping`. Om du vill skicka ytterligare variabler utanför de som har angetts för videomätning måste du använda `Media.monitor`. |
| `Media.adTrackMilestones` | Spårar och milstolpar i procent av annonsens längd.  <br/><br/> **Syntax:** <br/><br/> `s.Media.adTrackMilestones = "25, 50, 75";` <br/><br/>Definierar intervallet, i procent av annonsens längd, för att skicka annonsspårningsdata till Adobes datainsamlingsservrar. Ange milstolparna som en kommaavgränsad lista med heltal. Till exempel: 10 = 10 %, 23 = 23 %).  <br/><br/>Eftersom de här milstolparna är fasta punkter i annonsen, och en besökare tittar förbi milstolpen på 10 %, sedan spolar tillbaka och skickar milstolpen på 10 % igen, skickas spårningsdata flera gånger i mediemodulen. På samma sätt skickas inte spårningsdata för den milstolpen om en besökare går framåt förbi en milstolpe.  <br/><br/> När du aktiverar `Media.adTrackMilestones` utlöses bara de händelser som är definierade i `Media.contextDataMapping`. Om du vill skicka ytterligare variabler utanför de som har angetts för videomätning måste du använda `Media.monitor`. |
| `Media.adTrackOffsetMilestones` | Spårar och milstolpar när sekunder förflutit från annonsens början.  <br/><br/> **Syntax:** <br/><br/> `s.Media.adTrackOffsetMilestones = "20, 40, 60";` <br/><br/>Definierar intervallet, i sekunder, från annonsens början, för att skicka annonsspårningsdata till Adobes datainsamlingsservrar. Ange milstolparna som en kommaavgränsad lista med heltal. Till exempel: 20 = 20 sekunder, 40 = 40 sekunder).  <br/><br/>Eftersom de här milstolparna är fasta punkter i annonsen, och besökaren visar över milstolpen på 20 sekunder, spolar tillbaka och skickar milstolpen på 20 sekunder igen, skickas spårningsdata flera gånger i mediemodulen. På samma sätt skickas inte spårningsdata för den milstolpen om en besökare går framåt förbi en milstolpe.  <br/><br/> När du aktiverar `Media.adTrackOffsetMilestones` utlöses bara de händelser som är definierade i `Media.contextDataMapping`. Om du vill skicka ytterligare variabler utanför de som har angetts för videomätning måste du använda `Media.monitor`. |
| `Media.adSegmentByMilestones` | **Syntax:** <br/><br/> `s.Media.adSegmentByMilestones = true;` Genererar <br/><br/>automatiskt data om segmentnamn, segmentnummer och segmentlängd baserat på mediets längd och de milstolpar som anges i `Media.adTrackMilestones` Segmentering efter <br/><br/>milstolpar är det enda sättet att definiera segment när `autoTrack`.  <br/><br/>Standardvärde: `false` |
| `Media.adSegmentByOffsetMilestones` | **Syntax:** <br/><br/> `s.Media.adSegmentByOffsetMilestones = true;` Genererar <br/><br/>automatiskt data om segmentnamn, segmentnummer och segmentlängd baserat på mediets längd och de milstolpar som anges i `Media.adTrackOffsetMilestones` Segmentering efter <br/><br/>milstolpar är det enda sättet att definiera segment när `autoTrack`. <br/><br/>Standardvärde: `false` |

## Media Module-metoder {#media-module-methods}

Metoderna i mediemodulen används för att manuellt spåra spelarhändelser och för att spåra ytterligare mått som inte ingår i standardvideorapporterna.

Om du använder `Media.autoTrack` och inte spårar ytterligare mått behöver du inte anropa någon av dessa metoder direkt. Alla argument är obligatoriska om de inte anges som valfria.

| Metod | Beskrivning |
| --- | --- |
| `Media.open` | **Syntax:** <br/><br/> `s.Media.open(mediaName, mediaLength, mediaPlayerName)` Mediemodulen <br/><br/>förbereds för insamling av videospårningsdata. Den här metoden har följande parametrar: <ul><li> **mediaName:** (Obligatoriskt) Namnet på videon som du vill att den ska visas i videorapporter. </li><li>  **mediaLength:** (Obligatoriskt) Videons längd i sekunder.  </li><li> **mediaPlayerName:** (Obligatoriskt) Namnet på den mediespelare som användes för att visa videon, så som du vill att den ska visas i videorapporter. </li></ul> |
| `Media.openAd` | **Syntax:** <br/><br/> `s.Media.openAd(name, length, playerName, parentName,`<br/>   `parentPod, parentPodPosition, CPM)` <br/><br/>Förbereder mediemodulen för att samla in annonsspårningsdata. Den här metoden har följande parametrar: <ul> <li> **namn:** (Obligatoriskt) Annonsens namn eller ID.  </li> <li> **längd:** (Obligatoriskt) Annonsens längd.  </li> <li> **playerName:** (Obligatoriskt) Namnet på den mediespelare som användes för att visa annonsen.  </li> <li> **parentName:** Namnet eller ID för det primära innehållet där annonsen är inbäddad.  </li> <li> **parentPod:** Positionen i annonsens primära innehåll spelades upp.  </li> <li> **parentPodPosition:** Positionen i rutan där annonsen spelas upp.  </li> <li> **CPM:** CPM eller krypterad CPM (prefix med ett &quot;~&quot;) som gäller för den här uppspelningen.  </li> </ul> |
| `Media.click` | **Syntax:** <br/><br/> `s.Media.click(name, offset)` Spåra <br/><br/>när någon klickar på en annons i en video. Den här metoden har följande parametrar: <ul> <li> **namn:** Annonsens namn. Det här måste matcha namnet som används i Media.openAd.  </li> <li> **förskjutning:** Förskjutningen i annonsen när klickningen inträffade.  </li> </ul> |
| `Media.close` | **Syntax:** <br/><br/> `s.Media.close(mediaName)` Avslutar <br/><br/>datainsamling och skickar information till Adobes datainsamlingsservrar. Anropa den här metoden i slutet av videon. Den här metoden använder följande parameter: <br/><br/> **mediaName:** Namnet på videon. Detta måste matcha namnet som används i `Media.open`. |
| `Media.complete` | **Syntax:** <br/><br/> `s.Media.complete(name, offset)` Den <br/><br/>här metoden spårar en complete-händelse manuellt. Den här metoden används när du behöver utlösa händelser med hjälp av speciell logik som inte kan hanteras med `Media.completeByCloseOffset`. <br/><br/>Om du till exempel mäter ett direktflöde som inte har någon definierad ände, kan du utlösa ett slutförande efter att en användare har tittat på ett direktflöde i X sekunder. Du kan mäta ett fullständigt värde med en procentberäkning som baseras på innehållets längd och typ. Den här metoden har följande parametrar: <ul> <li> **mediaName:** Namnet på videon. Det här måste matcha namnet som används i Media.open.  </li> <li> **mediaOffset:** Antalet sekunder i videon när complete-händelsen ska skickas. Ange förskjutningen baserat på videon med början vid andra noll. <br/><br/>Om mediespelaren spårar med millisekunder kontrollerar du att värdet konverteras till sekunder innan du anropar Media.complete.  </li> </ul> Om du tänker ringa ett fullständigt samtal manuellt anger du <br/><br/> `s.Media.completeByCloseOffset = false`. |
| `Media.play` | **Syntax:** <br/><br/> `s.Media.play(name, offset, segmentNum, segment, segmentLength)` <br/><br/>Anropa den här metoden när en video börjar spelas upp. När du använder manuell videomätning kan du ange aktuella segmentdata när du skickar videomätdata.  <br/><br/>Om spelaren av någon anledning ändras från ett segment till ett annat bör du ringa `Media.stop``Media.play`. <br/><br/>Den här metoden har följande parametrar: <br/><br/> **mediaName:** Namnet på videon. Det här måste matcha namnet som används i Media.open.  <br/><br/> **mediaOffset:** Antalet sekunder i videon som spelas upp börjar. Ange förskjutningen baserat på videon med början vid andra noll. Om mediespelaren spårar med millisekunder kontrollerar du att värdet konverteras till sekunder innan du anropar Media.play.  <br/><br/> **segmentNum:** (Valfritt) Det aktuella segmentnumret, som används i marknadsföringsrapporter för att beställa visningen av segment i rapporter. Parametern segmentNum måste vara större än noll.  <br/><br/> **segment:** (Valfritt) Det aktuella segmentnamnet.  <br/><br/> **segmentLength:** (Valfritt) <br/><br/>Det aktuella segmentets längd i sekunder.  <br/><br/>Exempel: <br/><br/> `s.Media.play("My Video", 1800, 2,"Second Quarter", 1800)` <br/><br/> `s.Media.play("My Video", 0, 1,"Preroll", 30)` |
| `Media.stop` | **Syntax:** <br/><br/> `s.Media.stop(mediaName, mediaOffset)` <br/><br/>Spårar en stopphändelse (stopp, paus, osv.) för den angivna videon. Den här metoden har följande parametrar: <ul> <li> **mediaName:** Namnet på videon. Detta måste matcha namnet som används i `Media.open`.  </li> <li> **mediaOffset:** Antalet sekunder i videon som händelsen stop eller pause inträffar. Ange förskjutningen baserat på videon med början vid andra noll.  </li> </ul> |
| `Media.monitor` | **Syntax:** <br/><br/> `s.Media.monitor(s, media)` <br/><br/> **Silverlight-syntax:** <br/><br/> `s.Media.monitor =` <br/>Appmedierövervakaren `new AppMeasurement_Media_Monitor(myMediaMonitor);` <br/><br/>i Silverlight implementerar designmönstret för Objective-C-delegaten. Klassmetoden tar parametrarna `myMediaMonitor` och `s` `media` . <br/><br/>Använd den här metoden om du vill skicka ytterligare videomått. Du kan ställa in ytterligare variabler (Props, eVars, Events) och skicka dem med hjälp av `Media.track` baserat på videons aktuella status när den spelas upp. <br/><br/>Se [Mäta ytterligare mått med Media.monitor.](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_mediamonitor.html) Den <br/><br/>här metoden har följande parametrar: <br/><br/>  **s:** The `AppMeasurement` instance (eller JavaScript- `s` objekt). <br/><br/> **media:** Ett objekt med medlemmar som anger videons status. Bland dessa medlemmar finns:  <ul><li> `media.name:` Namnet på videon. Detta måste överensstämma med namnet som används i `Media.open`; </li><li> `media.length:` Längden på videon i sekunder som anges i anropet till `Media.open`. </li><li> `media.playerName:` Namnet på mediespelaren som anges i samtalet till `Media.open`. </li><li> `media.openTime:` Ett NSDate-objekt som innehåller data om när `Media.open` anropades; </li><li> `media.offset:` Aktuell förskjutning i sekunder (faktisk punkt i videon) till videon. Förskjutningen börjar vid noll (den första sekunden i videon är sekundär 0). </li><li> `media.percent:` Den aktuella procentandelen av videon som har spelats upp, baserat på videolängden och aktuell förskjutning.;  </li><li> `media.timePlayed:` Det totala antalet sekunder som hittills har spelats upp.  </li><li> `media.eventFirstTime:` Anger om detta var första gången som den här mediahändelsen anropades för videon, </li><li> `media.mediaEvent:` En sträng som innehåller händelsenamnet som orsakade övervakaranropet. </li></ul> |
|  | `media.mediaEvent` händelser: <ul><li> `OPEN:` När uppspelningen först ses via `Media.autoTrack` eller anropar `Media.play`. </li><li> `CLOSE:` När uppspelningen avslutas när videon har slutförts via `Media.autoTrack` eller vid ett anrop till `Media.close`.</li><li> `PLAY:` När uppspelningen återupptas efter att ha pausats eller snabbspolats genom `Media.autoTrack` eller ett andra anrop till `Media.play`.</li><li> `STOP:` När uppspelningen stoppas på grund av en paus i början av snabbspolningen `Media.autoTrack` eller ett anrop till `Media.stop`.</li><li> `MONITOR:` När vår automatiska övervakning kontrollerar videons status medan den spelas upp (varje sekund),</li><li> `SECONDS:` Vid det andra intervall som definieras av `Media.trackSeconds` variabeln.</li><li> `MILESTONE:` Vid de milstolpar som definieras av `Media.trackMilestones` variabeln. </li></ul> |
| `Media.track` | **Syntax:** <br/><br/> `s.Media.track(mediaName)` Skickar <br/><br/>omedelbart det aktuella videoläget tillsammans med alla Media.trackEvents `Media.trackVars` som du har definierat. Den här metoden används inuti `Media.monitor`. <br/><br/>Se [Mäta ytterligare mått med Media.monitor.](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_mediamonitor.html) <br/><br/>Anropa `Media.open` och `Media.play` anropa videon innan den här metoden anropas. Den här metoden använder följande parameter: <ul> <li> **mediaName**: Namnet på videon. Detta måste matcha namnet som används i `Media.open`.</li> </ul> Den här metoden är det enda sättet att skicka ytterligare variabler när videon spelas upp. Den återställer antalet milstolperäknare för sekundintervall och procent till noll för att förhindra flera spårningsträffar. |


## Spåra videospelarhändelser {#track-video-player-events}

Du kan spåra mediespelare genom att skapa funktioner som är kopplade till videospelarens händelsehanterare. Då kan du ringa `Media.open`, `Media.play`, `Media.stop`och `Media.close` vid rätt tidpunkt. Exempel:

* **Läs in:** Utlysning `Media.open` och `Media.play`
* **Pausa:** Ring `Media.stop`. Om en användare till exempel pausar en video efter 15 sekunder ringer du `s.Media.stop("Video1", 15)`
* **Buffer:** Anropa `Media.stop` medan videon buffrar. Anropa `Media.play` när uppspelningen återupptas.
* **Återuppta:** Ring `Media.play`. Om en användare till exempel återupptar en video efter att först ha spelat upp 15 sekunder av videon, ska du ringa `s.Media.play("Video1", 15)`.
* **Skrubba (reglage):** Ring när användaren drar videobildrutan `Media.stop`. Ring när användaren släpper videobildrutan `Media.play`.
* **Slut:** Ring `Media.stop`då `Media.close`. I slutet av en 100-sekunders video anropar du `s.Media.stop("Video1", 100)`och sedan `s.Media.close("Video1")`.

För att uppnå detta kan du definiera fyra anpassade funktioner som du kan anropa från händelsehanterarna för mediespelaren. De olika parametrarna skickades till `Media.open`, `Media.play`, `Media.stop`och `Media.close` kom från spelaren. Följande pseudokod visar hur detta kan göras:

```javascript
/* Call on video load */ 
function startMovie() { 
    s.Media.open(mediaName, mediaLength, mediaPlayerName); 
    playMovie(); 
} 
 
/* Call on video resume from pause and slider release */ 
function playMovie() { 
    s.Media.play(mediaName, 
                 mediaOffset,  
                 segmentNum,  
                 segment,  
                 segmentLength); 
} 
/* Call on video pause and slider grab */ 
function stopMovie() { 
    s.Media.stop(mediaName, mediaOffset); 
} 
 
/* Call on video end */ 
/* Measuring Video for Developers 43 */ 
function endMovie() { 
    stopMovie(); 
    s.Media.close(mediaName); 
} 
```

## Autospår för JavaScript {#javascript-autotrack}

JavaScript-mediemodulen identifierar alla `<embed>` - eller `<object>` -taggar i sidans HTML-kod. Sedan genomsöks data i varje tagg för att avgöra vilken mediespelare, om någon, som används. Om spelaren är Windows Media Player, QuickTime eller Real Player `autoTrack` kan användas, men `autoTrack` för Windows Media Player fungerar bara med Internet Explorer. Manuell spårning för Windows Media Player krävs för att stödja alla andra webbläsare.

Du måste ha attributet angivet för det objekt som du vill spåra `classid` . Det `classid` krävs för att visa de händelsehanterare som används av mediemodulen för att automatiskt spåra videon.

```javascript
s.Media.autoTrack = true
```

## JavaScript-exempelkod {#javascript-sample-code}

```javascript
// Sample implementation 
s.usePlugins=true 
function s_doPlugins(s) { 
    /* Add manual calls to modules and plugins here */ 
} 
 
s.doPlugins=s_doPlugins 
 
/*********Media Module Calls**************/ 
s.loadModule("Media") 
 
/*Configure Media Module Functions */ 
s.Media.autoTrack= true; 
s.Media.trackVars="events, prop2, eVar1, eVar2, eVar3"; 
s.Media.trackEvents="event1, event2, event3, event4, event5, event6, event7" 
s.Media.trackMilestones="25, 50, 75"; 
s.Media.playerName="My Media Player"; 
s.Media.segmentByMilestones = true; 
s.Media.trackUsingContextData = true; 
s.Media.contextDataMapping = { 
    "a.media.name":"eVar2, prop2", 
    "a.media.segment":"eVar3", 
    "a.contentType":"eVar1", 
    "a.media.timePlayed":"event3", 
    "a.media.view":"event1", 
    "a.media.segmentView":"event2", 
    "a.media.complete":"event7", 
    "a.media.milestones":{ 
        25:"event4", 
        50:"event5", 
        75:"event6" 
    } 
} 
 
s.Media.monitor = function (s, media) { } //If Needed

/* Turn on and configure debugging here */ 
s.debugTracking = true; 
s.trackLocal = true; 
 
/* WARNING: Changing any of the below variables will cause drastic changes to how your visitor 
data is collected. Changes should only be made when instructed to do so by your account 
manager.*/ 
s.visitorNamespace = "yourNamespace"; 
s.trackingServer="metrics.mysite.com" //Use only if using first party cookies 
s.trackingServerSecure="smetrics.mysite.com" // Use only if using first party cookies in  
                                             // conjunction with SSL 
s.dc = '122'; 
 
/************************** PLUGINS SECTION *************************/ 
/* Insert any plugins code you want to use here. */ 
 
/****************************** MODULES *****************************/ 
/* Insert the media module tracking code here. */ 
```


---
title: Parametrar för � för direktuppspelad mediainsamling
description: '"Vad är Media Collection API-parametrarna för förfrågningar, nycklar och beskrivningar."'
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d8b10249c542d2875cba4916e4a2c7942c5589c4
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 4%

---

# Begär parametrar{#request-parameters}

## Analysdata

| Begär nyckel  | Obligatoriskt | Begärantypnyckel | Aktivera... |  Beskrivning  |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | Y | string | `sessionStart` | URL-adressen till din Adobe Analytics-server |
| `analytics.reportSuite` | Y | string | `sessionStart` | Det ID som identifierar analysrapportdata |
| `analytics.enableSSL` | N | boolesk | `sessionStart` | Sant eller falskt för aktivering av SSL |
| `analytics.visitorId` | N | string | `sessionStart` | Adobe Visitor-ID är ett anpassat ID som du kan använda i flera Adobe-program. Heartbeat `visitorId` är lika med Analytics `VID.` |

## Besökardata

| Begär nyckel  | Obligatoriskt | Begärantypnyckel | Aktivera... |  Beskrivning  |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | string | `sessionStart` | Organisations-ID för Experience Cloud. identifierar din organisation inom Adobe Experience Cloud ekosystem |
| `visitor.marketingCloudUserId` | N | string | `sessionStart` | Det här är användar-ID:t för Experience Cloud (ECID). I de flesta fall är detta det ID som du bör använda för att identifiera en användare. Heartbeat `marketingCloudUserId` är lika med `MID` i Adobe Analytics. Den här parametern krävs inte tekniskt, men den är nödvändig för att få tillgång till appar i Experience Cloud-familjen. |
| `visitor.aamLocationHint` | N | heltal | `sessionStart` | Tillhandahåller Adobe Audience Manager Edge-data - Om inget värde anges är värdet null. |
| `appInstallationId` | N | string | `sessionStart` | appInstallationId identifierar programmet och enheten unikt |

## Innehållsdata

| Begär nyckel  | Obligatoriskt | Begärantypnyckel | Aktivera... |  Beskrivning  |
| --- | :---: | :---: | :---: | --- |
| `media.id` | Y | string | `sessionStart` | Unik identifierare för innehållet |
| `media.name` | N | string | `sessionStart` | Innehållets läsliga namn |
| `media.length` | Y | tal | `sessionStart` | Innehållslängd (sekunder) |
| `media.contentType` | Y | string | `sessionStart` | Strömmens format (kan vara vilken sträng som helst, ett fåtal rekommenderade värden är &quot;Live&quot;, &quot;VOD&quot; eller &quot;Linear&quot;) |
| `media.playerName` | Y | string | `sessionStart` | Namnet på den spelare som ansvarar för återgivningen av innehållet |
| `media.channel` | Y | string | `sessionStart` | Innehållets distributionskanal. Det kan vara ett mobilprogramnamn eller ett webbplatsnamn, egenskapsnamn |
| `media.resume` | N | boolesk | `sessionStart` | Anger om en användare återupptar en tidigare session (till skillnad från att starta en ny session) |
| `media.sdkVersion` | N | string | `sessionStart` | SDK-versionen som används av spelaren |

## Metadata för Content Standard

| Begär nyckel  | Obligatoriskt | Begärantypnyckel | Aktivera... |  Beskrivning  |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | N | string | `sessionStart` | Strömformat, t.ex. &quot;HD&quot; |
| `media.show` | N | string | `sessionStart` | Program- eller serienamn |
| `media.season` | N | string | `sessionStart` | Det säsongsnummer som programmet eller serien tillhör |
| `media.episode` | N | string | `sessionStart` | Antal avsnitt |
| `media.assetId` | N | string | `sessionStart` | Den unika identifieraren för innehållet i videoresursen, till exempel TV-seriens avsnittsidentifierare, filmresursidentifierare eller live-händelseidentifierare. Vanligtvis härleds dessa ID:n från metadatautfärdare som EIDR, TMS/Gracenote eller Rovi. Dessa identifierare kan också komma från andra egenutvecklade eller interna system. |
| `media.genre` | N | string | `sessionStart` | Innehållstypen som definierats av innehållsproducenten |
| `media.firstAirDate` | N | string | `sessionStart` | Det datum då innehållet först skrevs på tv |
| `media.firstDigitalDate` | N | string | `sessionStart` | Det datum då innehållet först skrevs på en digital plattform |
| `media.rating` | N | string | `sessionStart` | Betyg enligt definitionen i TV:s föräldrariktlinjer |
| `media.originator` | N | string | `sessionStart` | Innehållets skapare |
| `media.network` | N | string | `sessionStart` | Nätverks-/kanalnamn |
| `media.showType` | N | string | `sessionStart` | Innehållstypen, uttryckt som ett heltal mellan 0 och 3: <ul> <li>0 - Hela avsnittet </li> <li>1 - Förhandsgranska </li> <li>2 - Klipp </li> <li>3 - Annan </li> </ul> |
| `media.adLoad` | N | string | `sessionStart` | Typen av annons som läses in |
| `media.pass.mvpd` | N | string | `sessionStart` | MVPD som tillhandahålls av Adobe-autentisering |
| `media.pass.auth` | N | string | `sessionStart` | Anger att användaren har autentiserats av Adobe (kan bara vara true om den har angetts) |
| `media.dayPart` | N | string | `sessionStart` | Tidpunkten när innehållet sändes |
| `media.feed` | N | string | `sessionStart` | Typ av foder, t.ex.&quot;West-HD&quot; |

## Annonsdata

| Begär nyckel  | Obligatoriskt | Begärantypnyckel | Aktivera... |  Beskrivning  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | string | `adBreakStart` | Eget namn på annonsbrytningen |
| `media.ad.podIndex` | Y | heltal | `adBreakStart` | Indexvärdet för annonspunkten i videon |
| `media.ad.podSecond` | Y | tal | `adBreakStart` | Den andra gången som fönstret började |
| `media.ad.podPosition` | Y | heltal | `adStart` | Indexvärdet för annonsen inuti annonsbrytningen med början vid 1 |
| `media.ad.name` | N | string | `adStart` | Annonsens namn |
| `media.ad.id` | Y | string | `adStart` | Annonsens namn |
| `media.ad.length` | Y | tal | `adStart` | Videoannons längd i sekunder |
| `media.ad.playerName` | Y | string | `adStart` | Namnet på spelaren som ansvarar för att återge annonsen |

## Standardmetadata för annons

| Begär nyckel  | Obligatoriskt | Begärantypnyckel | Aktivera... |  Beskrivning  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | N | string | `adStart` | Företaget eller varumärket vars produkt finns i annonsen |
| `media.ad.campaignId` | N | string | `adStart` | ID för annonskampanjen |
| `media.ad.creativeId` | N | string | `adStart` | Annonspersonalens ID |
| `media.ad.siteId` | N | string | `adStart` | Annonswebbplatsens ID |
| `media.ad.creativeURL` | N | string | `adStart` | Webbadressen till annonsens kreatör |
| `media.ad.placementId` | N | string | `adStart` | Annonsens placerings-ID |

## Kapiteldata

| Begär nyckel  | Obligatoriskt | Begärantypnyckel | Aktivera... |  Beskrivning  |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | Y | heltal | `chapterStart` | Identifierar kapitlets position i innehållet |
| `media.chapter.offset` | Y | tal | `chapterStart` | Den andra i uppspelningen där kapitlet börjar |
| `media.chapter.length` | Y | tal | `chapterStart` | Kapitelns längd i sekunder |
| `media.chapter.friendlyName` | N | string | `chapterStart` | Kapitlets användarvänliga namn |

## Kvalitetsdata

| Begär nyckel  | Obligatoriskt | Begärantypnyckel | Aktivera... |  Beskrivning  |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | N | heltal | Alla | Genomsnittlig bithastighet (i bps). Den genomsnittliga bithastigheten beräknas som ett vägt genomsnitt av alla bithastighetsvärden som relateras till uppspelningens varaktighet som inträffade under en uppspelningssession. |
| `media.qoe.droppedFrames` | N | heltal | Alla | Antalet uteslutna bildrutor i strömmen |
| `media.qoe.framesPerSecond` | N | heltal | Alla | Antalet bildrutor per sekund |
| `media.qoe.timeToStart` | N | heltal | Alla | Den tid (i millisekunder) som förflyter mellan att användaren träffar uppspelningen och att innehållet läses in och börjar spelas upp |

## CCPA-parametrar (California Consumer Privacy Act) {#ccpa-params}

| Begär nyckel  | Obligatoriskt | Begärantypnyckel | Aktivera... |  Beskrivning  |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | boolesk | `sessionStart` | Anges till true när slutanvändaren har valt att inte dela data mellan Adobe Analytics och andra Experience Cloud-lösningar (t.ex. Audience Manager) |
| `analytics.optOutShare` | N | boolesk | `sessionStart` | Anges till true när slutanvändaren har valt att inte använda data som federeras (t.ex. till andra Adobe Analytics-klienter). |

## Ytterligare information {#additional-details}

### visitor.marketingCloudUserId

Skicka användar-ID:t för Experience Cloud (kallas även `MID` eller `MCID`) på `sessionStart`-anropet genom att inkludera det i `params`-kartan med följande tangent: **visitor.marketingCloudUserId**. Detta är en användbar funktion om du redan har integrerat med andra Experience Cloud-produkter och redan har fått MCID.

>[!NOTE]
>
>Media Analytics (MA) är integrerat med Experience Cloud-appfamiljen (Adobe Analytics, Audience Manager, Target och så vidare). Du behöver ett Experience Cloud-ID för att få tillgång till dessa program. _ECID är det du bör använda för att identifiera användare i de flesta scenarier._

### appInstallationId

* **Om du  *inte* skickar något  `appInstallationId` värde kommer** den bakomliggande hanteringsservern inte längre att generera ett MCID, utan Adobe Analytics kommer att förlita sig på att detta sker. Adobe rekommenderar att du antingen skickar ett MCID om tillgängligt, eller ett `appInstallationId` (tillsammans med det fortfarande obligatoriska `marketingCloudOrgId`) så att Media Collection API genererar MCID och skickar det för alla anrop.

* **Om du  ** dopass  `appInstallationId` value -** MCID  *kan* genereras av MA-serverdelen om du skickar värden för  `appInstallationId` och (obligatoriska)  `marketingCloudOrgId` parametrar. Om du skickar `appInstallationId` själv måste du behålla värdet på klientsidan. Den måste vara unik för appen på en enhet och måste vara beständig så länge appen inte installeras om.

>[!NOTE]
>
>`appInstallationId` identifierar programmet *och enheten*. Det måste vara unikt för varje app på varje enhet, d.v.s. två användare som använder samma version av samma program på olika enheter måste skicka olika (unika) `appInstallationId`.

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

Förutom att den är nödvändig för MCID-generering när detta inte anges, används den här parametern också som värde för utgivar-ID (baserat på vilket Media Analytics utför [federationsregelmatchning.](/help/federated-analytics.md))

### Analyserar äldre användar-ID (hjälp) och deklarerade användar-ID:n (customerID:n)

* **analytics.aid:**

   Värdet för den här nyckeln måste vara en sträng som representerar det äldre användar-ID:t för Analytics
* **visitor.customerID:**

   Värdet för den här nyckeln måste vara ett objekt i följande format:

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>>
   }
   ```

Observera att `visitor.customerIDs`-värdet kan ha valfritt antal objekt i det angivna formatet.

### visitor.aamLocationHint

Den här parametern anger vilken Adobe Audience Manager (AAM) Edge ska påverkas när Adobe Analytics skickar kunddata till Audience Manager. Om inget värde anges är värdet null. Detta är särskilt viktigt när slutanvändarna tenderar att använda sina enheter på geografiskt avlägsna platser (t.ex. USA-öst, USA-väst, Europa, Asien). Annars sprids användardata över flera AAM kanter.

### media.resume

Om appen fastställer att en session stängdes och sedan återupptogs vid ett senare tillfälle, t.ex. om användaren lämnade videon men så småningom kom tillbaka, och spelaren återupptog videon från spelhuvudet där den stoppades, kan du skicka en valfri boolesk **media.resume**-parameter inuti parameterbegränsningen för anropet `sessionStart`.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->

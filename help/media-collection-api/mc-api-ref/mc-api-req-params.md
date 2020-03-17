---
title: Begär parametrar
description: null
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Begär parametrar{#request-parameters}

## Analysdata

| Begär nyckel | Obligatoriskt | Aktivera... |  Beskrivning |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | URL-adressen till Adobe Analytics-servern |
| `analytics.reportSuite` | Y | `sessionStart` | Det ID som identifierar analysrapportdata |
| `analytics.enableSSL` | N | `sessionStart` | Sant eller falskt för aktivering av SSL |
| `analytics.visitorId` | N | `sessionStart` | Adobe Visitor-ID:t är ett anpassat ID som du kan använda i flera Adobe-program. Heartbeat `visitorId` är lika med Analytics `VID.` |

## Besökardata

| Begär nyckel | Obligatoriskt | Aktivera... |  Beskrivning |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | Experience Clouds organisations-ID; identifierar din organisation i Adobe Experience Cloud-ekosystemet |
| `visitor.marketingCloudUserId` | N | `sessionStart` | Det här är Experience Cloud-användar-ID:t (ECID). I de flesta fall är detta det ID som du bör använda för att identifiera en användare. Heartbeat `marketingCloudUserId` är lika med `MID` i Adobe Analytics. Den här parametern krävs inte tekniskt, men den behövs för att få tillgång till Experience Cloud-apparna. |
| `visitor.aamLocationHint` | N | `sessionStart` | Tillhandahåller Edge-data för Adobe Audience Manager |
| `appInstallationId` | N | `sessionStart` | appInstallationId identifierar programmet och enheten unikt |

## Innehållsdata

| Begär nyckel | Obligatoriskt | Aktivera... |  Beskrivning |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | Unik identifierare för innehållet |
| `media.name` | N | `sessionStart` | Innehållets läsliga namn |
| `media.length` | Y | `sessionStart` | Innehållslängd (sekunder) |
| `media.contentType` | Y | `sessionStart` | Strömmens format (kan vara vilken sträng som helst, ett fåtal rekommenderade värden är &quot;Live&quot;, &quot;VOD&quot; eller &quot;Linear&quot;) |
| `media.playerName` | Y | `sessionStart` | Namnet på den spelare som ansvarar för återgivningen av innehållet |
| `media.channel` | Y | `sessionStart` | Innehållets distributionskanal. Det kan vara ett mobilprogramnamn eller ett webbplatsnamn, egenskapsnamn |
| `media.resume` | N | `sessionStart` | Anger om en användare återupptar en tidigare session (till skillnad från att starta en ny session) |
| `media.sdkVersion` | N | `sessionStart` | SDK-versionen som används av spelaren |

## Metadata för Content Standard

| Begär nyckel | Obligatoriskt | Aktivera... |  Beskrivning |
| --- | :---: | :---: | --- |
| `media.show` | N | `sessionStart` | Program- eller serienamn |
| `media.season` | N | `sessionStart` | Det säsongsnummer som programmet eller serien tillhör |
| `media.episode` | N | `sessionStart` | Antal avsnitt |
| `media.assetId` | N | `sessionStart` | Den unika identifieraren för innehållet i videoresursen, till exempel TV-seriens avsnittsidentifierare, filmresursidentifierare eller live-händelseidentifierare. Vanligtvis härleds dessa ID:n från metadatautfärdare som EIDR, TMS/Gracenote eller Rovi. Dessa identifierare kan också komma från andra egenutvecklade eller interna system. |
| `media.genre` | N | `sessionStart` | Innehållstypen som definierats av innehållsproducenten |
| `media.firstAirDate` | N | `sessionStart` | Det datum då innehållet först skrevs på tv |
| `media.firstDigitalDate` | N | `sessionStart` | Det datum då innehållet först skrevs på en digital plattform |
| `media.rating` | N | `sessionStart` | Betyg enligt definitionen i TV:s föräldrariktlinjer |
| `media.originator` | N | `sessionStart` | Innehållets skapare |
| `media.network` | N | `sessionStart` | Nätverks-/kanalnamn |
| `media.showType` | N | `sessionStart` | Innehållstypen, uttryckt som ett heltal mellan 0 och 3: <ul> <li>0 - Hela avsnittet </li> <li>1 - Förhandsgranska </li> <li>2 - Klipp </li> <li>3 - Annan </li> </ul> |
| `media.adLoad` | N | `sessionStart` | Typen av annons som läses in |
| `media.pass.mvpd` | N | `sessionStart` | Det MVPD som tillhandahålls av Adobes autentisering |
| `media.pass.auth` | N | `sessionStart` | Anger att användaren har autentiserats av Adobe (kan bara vara true om den har angetts) |
| `media.dayPart` | N | `sessionStart` | Tidpunkten när innehållet sändes |
| `media.feed` | N | `sessionStart` | Typ av foder, t.ex.&quot;West-HD&quot; |

## Annonsdata

| Begär nyckel | Obligatoriskt | Aktivera... |  Beskrivning |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Eget namn på annonsbrytningen |
| `media.ad.podIndex` | Y | `adBreakStart` | Indexvärdet för annonspunkten i videon |
| `media.ad.podSecond` | Y | `adBreakStart` | Den andra gången som fönstret började |
| `media.ad.podPosition` | Y | `adStart` | Indexvärdet för annonsen inuti annonsbrytningen med början vid 1 |
| `media.ad.name` | N | `adStart` | Annonsens namn |
| `media.ad.id` | Y | `adStart` | Annonsens namn |
| `media.ad.length` | Y | `adStart` | Videoannons längd i sekunder |
| `media.ad.playerName` | Y | `adStart` | Namnet på spelaren som ansvarar för att återge annonsen |

## Standardmetadata för annons

| Begär nyckel | Obligatoriskt | Aktivera... |  Beskrivning |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | Företaget eller varumärket vars produkt finns i annonsen |
| `media.ad.campaignId` | N | `adStart` | ID för annonskampanjen |
| `media.ad.creativeId` | N | `adStart` | Annonspersonalens ID |
| `media.ad.siteId` | N | `adStart` | Annonswebbplatsens ID |
| `media.ad.creativeURL` | N | `adStart` | Webbadressen till annonsens kreatör |
| `media.ad.placementId` | N | `adStart` | Annonsens placerings-ID |

## Kapiteldata

| Begär nyckel | Obligatoriskt | Aktivera... |  Beskrivning |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | Identifierar kapitlets position i innehållet |
| `media.chapter.offset` | Y | `chapterStart` | Den andra i uppspelningen där kapitlet börjar |
| `media.chapter.length` | Y | `chapterStart` | Kapitelns längd i sekunder |
| `media.chapter.friendlyName` | N | `chapterStart` | Kapitlets användarvänliga namn |

## Kvalitetsdata

| Begär nyckel | Obligatoriskt | Aktivera... |  Beskrivning |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Alla | Strömmens bithastighet |
| `media.qoe.droppedFrames` | N | Alla | Antalet uteslutna bildrutor i strömmen |
| `media.qoe.framesPerSecond` | N | Alla | Antalet bildrutor per sekund |
| `media.qoe.timeToStart` | N | Alla | Den tid (i millisekunder) som förflyter mellan att användaren träffar uppspelningen och att innehållet läses in och börjar spelas upp |

## CCPA-parametrar (California Consumer Privacy Act) {#ccpa-params}

| Begär nyckel | Obligatoriskt | Aktivera... |  Beskrivning |
| --- | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | `sessionStart` | Anges till true när slutanvändaren har valt att inte dela data mellan Adobe Analytics och andra Experience Cloud-lösningar (till exempel Audience Manager) |
| `analytics.optOutShare` | N | `sessionStart` | Anges till true när slutanvändaren har valt att inte använda data som federeras (t.ex. till andra Adobe Analytics-klienter). |

## Ytterligare information {#additional-details}

### visitor.marketingCloudUserId

Skicka Experience Cloud-användar-ID:t (kallas även `MID` eller `MCID`) för `sessionStart` anropet genom att inkludera det i `params` kartan med följande nyckel: **visitor.marketingCloudUserId**. Det här är en användbar funktion om du redan har integrerat med andra Experience Cloud-produkter och redan har fått MCID.

>[!NOTE]
>
>Media Analytics (MA) är integrerat med Experience Cloud-apparna (Adobe Analytics, Audience Manager, Target och så vidare). Du behöver ett Experience Cloud-ID för att få tillgång till dessa program. _ECID är det du bör använda för att identifiera användare i de flesta scenarier._

### appInstallationId

* **Om du *inte*skickar ett`appInstallationId`värde** genererar inte längre MA-serverdelen något MCID, utan använder Adobe Analytics för att göra detta. Adobes rekommendation är att antingen skicka ett MCID om tillgängligt, eller ett `appInstallationId` (tillsammans med det fortfarande obligatoriska `marketingCloudOrgId`) så att Media Collection API genererar MCID och skickar det på alla anrop.

* **Om du *skickar*`appInstallationId`värde -** MCID *kan* genereras av MA-serverdelen om du skickar värden för `appInstallationId` - och (obligatoriska) `marketingCloudOrgId` -parametrarna. Om du skickar `appInstallationId` själv måste du behålla värdet på klienten. Den måste vara unik för appen på en enhet och måste vara beständig så länge appen inte installeras om.

>[!NOTE]
>
>Den `appInstallationId` unika identifieringen av programmet *och enheten*. Den måste vara unik för varje program på varje enhet, dvs. två användare som använder samma version av samma program på olika enheter måste skicka olika (unika) `appInstallationId`.

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor.marketingCloudOrgId

Förutom att den är nödvändig för MCID-generering när detta inte anges, används den här parametern också som värde för utgivar-ID (baserat på vilket Media Analytics utför matchning av [federationsregler.](/help/federated-analytics.md))

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

Observera att värdet kan ha ett valfritt antal objekt i det format som visas. `visitor.customerIDs`

### visitor.aamLocationHint

Den här parametern anger vilken Adobe Audience Manager (AAM) Edge ska påverkas när Adobe Analytics skickar kunddata till Audience Manager. Om du inte skickar den här parametern kodar Adobe den till 1. Detta är särskilt viktigt när slutanvändarna tenderar att använda sina enheter på geografiskt avlägsna platser (t.ex. USA-öst, USA-väst, Europa, Asien). Annars sprids användardata över flera AAM-kanter.

### media.resume

Om appen avgör att en session stängdes och sedan återupptas vid ett senare tillfälle, t.ex. om användaren lämnade videon men så småningom kom tillbaka, och spelaren återupptog videon från spelhuvudet där den stoppades, kan du skicka en valfri boolesk **media.resume** -parameter i `sessionStart` anropets parameterintervall.

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
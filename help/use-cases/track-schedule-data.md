---
title: Överför schemadata för att spåra livematerial
description: Lär dig hur du överför schemadata för att spåra livematerial.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 875c4513-ea4e-4c5f-bfc1-34ea175007ca
source-git-commit: 65cd7987acb677b4f4c863b42dc809b5a23c2ed1
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 0%

---

# Överför schemadata för att spåra livematerial

>[!AVAILABILITY]
>
>Funktionerna som beskrivs i den här artikeln är i den begränsade testfasen av releasen och är kanske inte tillgängliga än i din miljö. Den här anteckningen tas bort när funktionen är allmänt tillgänglig. Mer information om versionsprocessen finns i [Customer Journey Analytics funktionsreleaser](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/releases).

Du kan överföra schemadata från tidigare direktuppspelat mediematerial för att enklare och exaktare kunna spåra hur det direktuppspelade innehållet visas. Du kan spåra visningen av enskilda program och till och med specifika ämnen eller programsegment.

Nedan följer exempel på live-innehåll som stöds vid schemalagd dataöverföring:

* FAST-plattformar (Free Ad Supported TV)

* Lokala strömmar

* Livesporter

* Nyheter eller ämnesprogrammering

## Funktioner

Olika funktioner är tillgängliga vid användning av schemalagda dataöverföringar av tidigare direktuppspelat mediematerial. I det här avsnittet beskrivs några av de viktigaste funktionerna som hjälper till att analysera programmets prestanda.

Dessa funktioner är tillgängliga oavsett hur du implementerade Streaming Media Collection.

* **Spåra programscheman** korrekt: Identifiera start- och sluttider för varje enskilt program i liveströmmen under den tidsperiod som du vill analysera. Med korrekta start- och sluttider återspeglas den exakta körtiden korrekt och kan analyseras mot varje visningsprogramsession.

  Exempelvis är exakta start- och sluttider inte alltid kända för ett idrottsevenemang förrän evenemanget är slut. Schemalägg dataöverföringar gör att du kan få korrekta rapporter genom att uppdatera start- och sluttider när programmet har slutförts.

* **Spåra enskilda ämnen eller programsegment**: Skapa nya tidsbaserade dimensioner för specifika ämnen eller programsegment (tidsintervall) inom ett visst program. Med dessa tidsbaserade dimensioner kan ni analysera tittandet av ett program på en mer specifik nivå, vilket hjälper er att samla insikter om vilka ämnen eller programsegment som fick bäst gensvar.

  När du till exempel analyserar ett idrottsevenemang, till exempel en fotbollsmatchning, kan du skapa separata dimensioner för den första halvan, halva tiden och den andra halvan. Genom att spåra specifika ämnen eller segment i ett program på det här sättet kan du få en mer detaljerad beskrivning av visningsprogrammets beteende.

* **Bygg användarresor i Journey Optimizer**: Spåra vilka program en person har tittat på under en viss session (eller till och med vilka avsnitt eller programsegment personen har tittat på) och använd sedan dessa data i Adobe Journey Optimizer för att skapa användarresor för kunder som tittade på ett visst program eller som visade intresse för ett visst ämne.

## Förstå hur schemalagda data fungerar för Streaming Media

Schemaläggningsfunktionaliteten för direktuppspelningsmedia fungerar på följande sätt:

1. Läser från schemaläggningsprogramdatauppsättningen för schemaprogramposter, filtrerar efter schemadatum.

   Fungerar bara för program som har gått mellan 24 och 48 timmar tidigare.

2. Läser mediastängningshändelser från mediedatauppsättningen, filtrera efter datum och efter XDM-sökvägen i schemaprogramposterna.

3. För varje mediastängningshändelse genereras samma antal starthändelser för medieschemat som det fanns program som överlappade mediesessionen.

   Varje medieschemastarthändelse innehåller schemats namn och längd.

   Dessutom innehåller ett nytt tidsmått med namnet **scheduleTimePlayed** det antal sekunder som mediesessionen överlappade med det schemalagda programmet. Tidsstämpeln för schemastarthändelsen är den tidsstämpel som användes när programmet startades.

4. Skriver de nya schemastarthändelserna i AEP mediedatauppsättning.

## Förutsättningar

För att kunna överföra schemadata från tidigare livematerial måste miljön för direktuppspelning av media uppfylla följande krav:

* Direktuppspelad mediainsamling måste vara aktiverad för spårning av innehållet som du vill överföra schemadata för, vilket beskrivs i [Spårningsöversikt](/help/use-cases/track-av-playback/track-core-overview.md). <!--specifics??? -->

* Använd Streaming Media Collection med Customer Journey Analytics. Det går inte att överföra schemadata med Adobe Analytics.

## Skapa en programschemadatauppsättning i AEP

Innan du kan skicka schemainformation måste du skapa en programschemadatauppsättning i Experience Platform:

1. Skapa ett schema baserat på XDM-klassen **Media Analytics Scheduled Program** .

   ![Schema för schemaprogram för medieanalys](assets/media_schedule_finish_schema_creation.png)

   Detta är XDM-definitionen för den schemalagda programklassen Media Analytics.

   [https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json](https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json)

1. Skapa en datauppsättning baserat på det schema som du skapade.

1. Fortsätt med följande avsnitt: [Push schedule information](#push-schedule-information).

## Information om push-schema

När du har [skapat en programschemadatauppsättning](#create-a-program-schedule-dataset-in-aep) kan du skicka schemainformation:

1. Skapa en JSON-fil med schemainformationen.

   .json-filen måste innehålla en array med Schedule Program-objekt, i enlighet med XDM-schemat.

1. Överför .json-filen:

   >[!NOTE]
   >
   >cURL-exemplen i det här avsnittet använder följande variabler:
   >
   >* För autentisering med Adobe Developer:
   >     * CUSTOMER_API_KEY
   >     * AUTH_TOKEN
   >* organisations-ID: CUSTOMER_ORG_ID
   >* datauppsättnings-ID för postdatauppsättningen som skapades i konfigurationen: DATASET_ID
   >* batch-ID som skapades i den första begäran som användes vid filöverföringen: BATCH_ID
   >* Namnet på filen som används för att skicka poster: FILE_NAME

   1. Skapa en ny batch och hämta batch-ID:t från svaret.

      Titta på följande exempel på hur du använder cURL för att skapa en ny AEP Batch:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches' \
          -X POST \
          -H 'Accept: application/json' \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --data-raw '{"datasetId":"<DATASET_ID>","inputFormat":{"format":"json","isMultiLineJson":true},"tags":{"test":["2"]}}'
      
          HTTP/1.1 201 Created
          {
              "id": "BATCH_ID",
              "imsOrg": "CUSTOMER_ORG_ID",
              "updated": 1749838941763,
              "status": "loading",
              "created": 1749838941763,
              "relatedObjects": [
                  {
                      "type": "dataSet",
                      "id": "DATASET_ID"
                  }
              ],
              "version": "1.0.0",
              ............
          }
      ```

   1. Skicka .json-filen som innehåller programschemadataposterna med batch-ID:t.

      Om du vill skicka schemainformation ska du använda AEP batch-API:er, enligt beskrivningen i [API-översikt för gruppinläsning](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/batch/overview).

      Tänk på följande exempel på hur du använder cURL för att skicka en fil med schemaposterna:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>/datasets/<DATASET_ID>/files/<FILE_NAME>' \
          -X PUT \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --upload-file ./schedule_21_05_2025.json`
      ```

   1. Slutför batchen.

      Titta på följande exempel på hur du använder cURL för att slutföra gruppen:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>?action=COMPLETE' \
          -X POST \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>'
      ```

1. Fortsätt med följande avsnitt: [Logga en supportanmälan med Adobe kundtjänst](#log-a-support-ticket-with-adobe-customer-care).

## Logga ett supportärende hos Adobe kundtjänst

Logga ett supportärende hos Adobe kundtjänst med följande information:

* **Mediedatauppsättning**: Ange datauppsättnings-ID för den datauppsättning från vilken mediessionsdata läses.

* **Schemalägg datauppsättning**: Ange datauppsättnings-ID för den datauppsättning som schemaposterna skickas till.

* **Datauppsättning för utdata**: Ange datauppsättnings-ID för den datauppsättning som starthändelserna för schemat sparas i.

  Detta datauppsättnings-ID kan vara samma datauppsättnings-ID som används för mediedatauppsättningen. Om det är ett annat datauppsättnings-ID bör det fortfarande ha samma XDM-schema som mediedatauppsättningen.

* **Organisations-ID**: Ange ditt organisations-ID.

## Exempel på en .json-schemafil med två poster

Följande exempel är en .json-schemafil med två poster. Varje .json-fil ska innehålla alla schemalagda program för en dag.

```
   [
        {
            "_id": "any_identifier_as_id_1",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 1800,
                "name": "Show Name",
                "startTimestamp": "2025-05-01T00:30:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            },
        },
        {
            "_id": "any_identifier_as_id_2",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 3600,
                "name": "Show Name 2",
                "startTimestamp": "2025-05-01T01:00:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            }
        }
    ]
```

### Förstå schemafält i exemplet

1. **mediaProgramDetails**: Ska innehålla den information som krävs för att skapa schemats starthändelse:
   * **startTimestamp**: Den tid då programmet startades.
   * **namn**: Visningens egna namn.
   * **length**: Antalet sekunder som visningen varade.

     >[!IMPORTANT]
     >
     >Om du har flera schemalagda dataförfrågningar kan de inte ha överlappande start- och sluttider.

1. **scheduleDate**: Det datum då programmet skrevs. Formatet ska vara YYY-MM-DD. Den används för att filtrera schemadatauppsättningen och hämta alla scheman som adobe skapar schemat för.
1. **scheduleFilter**: Används för att filtrera alla stängningshändelser för mediesessioner.
   * **filterPath**: En XDM-sökväg till fältet som används för filtrering.
   * **filterValue**: Det värde som används för filtrering.
1. **customMetadata**: Anpassade metadata som du vill lägga till i schemat startar händelser. Dessa metadata används för att skriva över anpassade metadata som finns i sessionens stängningshändelser.
1. **defaultMetadata**: En specifik lista över dimensioner som kan lägga till eller skriva över standardmetadata som finns i mediastängningsanropen.

   Här följer några exempel på dimensioner som du kan skapa och sedan rapportera om i Customer Journey Analytics:

   * **[&quot;_Avsnittsnamn_&quot;](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters#episode)**: Den här dimensionen kan hjälpa dig att lära dig vilka avsnitt i en viss serie som fungerar bäst.

   * **[Resurs-ID](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters#asset-id)**

1. Fortsätt med [Analysera data i Customer Journey Analytics](#analyze-data-in-customer-journey-analytics).

## Analysera data i Customer Journey Analytics

Inom en dag efter att du har överfört din datafil enligt beskrivningen i [Begär och överför schemadatafilen](#request-and-upload-the-schedule-data-file) är dina data klara att rapporteras i Customer Journey Analytics.

Så här rapporterar du om tidigare liveströmmande mediedata i Customer Journey Analytics:

1. Skapa ett nytt projekt eller öppna ett befintligt projekt.

1. Bygg upp projektet genom att skapa tabeller eller visualiseringar som behövs för att analysera tidigare livedata i Streaming Media.

   När du bygger upp ett projekt ska du använda den information som du har angett i schemadatafilen och skickat till Adobe kundtjänst. Detta inkluderar matchande nyckel, dimensioner och eventuella ytterligare metadata. Mer information finns i [Begär och överföra schemadatafilen](#request-and-upload-the-schedule-data-file).




<!-- 

Extra

Things they need to upload:
Everything on that slide + other metadata
You can't overlap 2 schedules.
You can build a journey in AJO for the people who watch Mike, Mike, and Mike. e.g. 
This is recurring.
Available to all SKUs? "Increases cost for updated data by 22%, but included in the new higher tier Streaming Media SKU."

You can now upload schedule data of past live content to more easily and accurately track viewership. Live content includes content from FAST (Free Ad Supported TV) platforms or local streams.
You can track which programs a person viewed in a given session, or even which topics or program segments they viewed. These capabilities are available regardless of how you implemented Streaming Media Collection.
Previously, it was difficult to accurately tie a given session to specific programs when analyzing live content, and it wasn't possible to tie a given session to individual topics or program segments.
Schedule data uploads of live content in Streaming Media Collection includes the following capabilities:
Upload schedules for past live content, regardless of your Streaming Media Collection implementation.
Identify the start and end times of each individual program in the live stream for the period of time that you want to analyze. With accurate start and end times, the precise running time is accurately reflected and can be analyzed against each viewer session.
For example, precise beginning and end times are not always known for a live sporting event until the event is over. Schedule data uploads allow you to get accurate reporting by updating the start and end times after the program finishes.
Create new time-based dimensions for specific topics or program segments (time slots) within a given program. These time-based dimensions allow you to analyze viewership of a program at a more specific level, helping to gather insights about which topics or program segments resonated best.
For example, when analyzing a live sporting event, such as a soccer match, you can create separate dimensions for the first half, half time, and second half. This allows for more detailed breakdowns of viewer behavior for specific segments of a program.
These capabilities allow you to:
Analyze show viewership to understand performance.
Target users based on program viewership.
Analyze viewership based on metadata like topic, sports league, sponsorship, and so forth.
Target based on metadata viewership.
Correct media metrics for show dimensions of live sports/events for easier analysis at scale.
Increased ease of use for live sports

-->

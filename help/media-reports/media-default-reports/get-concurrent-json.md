---
title: Hämta JSON-rapportdata för samtidiga visningsprogram
description: Hämta JSON-rapportdata för samtidiga visningsprogram
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 4%

---


# Hämta JSON-rapportdata för samtidiga visningsprogram{#get-concurrent-viewers-json-report-data}

Du kan hämta rapportdata för samtidiga visningsprogram med hjälp av _*1.4-versionen*_ av API:erna för analys:
* [API:er för Analytics](https://github.com/AdobeDocs/analytics-1.4-apis)
* [Swagger](https://adobedocs.github.io/analytics-1.4-apis/swagger-docs.html#/Report/Report.Get)

1. Filtrera data med ett segment som bygger på användargränssnittet. Om du vill filtrera efter ett visst innehålls-ID skapar du ett nytt segment.
1. Ange `elements` -> `id` i begärandetexten som `videoconcurrentviewers`.
1. Begär tillräckligt med data. Adobe rekommenderar 3200 datapunkter för att säkerställa att det inte finns några luckor i data.

   * Det dataområde som du anger i rapporten samlar alla samtidiga visningsdata _när videosessionen avslutades._
Du måste alltså redovisa sessioner som börjar en dag och slutar efter midnatt (dvs. nästa dag).

   * Begär mer än en dag data, men i din analys _*använd bara den första dagen i data.*_

Nyttolasten för en exempelbegäran för det här scenariot skulle se ut så här:

```
{
  "reportDescription":{
    "reportSuiteID":"[YOUR_RSID]",
    "dateFrom":"2018-07-01",
    "dateTo":"2018-07-02",
    "metrics":[
      {
        "id":"instances"
      }
    ],
    "elements":[
      {
        "id":"videoconcurrentviewers",
        "top":"3200"
      }
    ],
    "segments":[
      {
        "id":"s1234_58ca4fc7e4b0abc238707bb9"                                         
      }
    ],
    "sortBy":"instances",
    "locale":"en_US"
  }
}
```

<!--
You can extract the concurrent viewers report data using the Experience Cloud API Explorer as follows. 

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html)
        
        * `dateTo` - End date of the report.         
        
          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`
        
        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }
      
      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The concurrent viewers report data, in JSON format, is presented in the Response field.
   
   For example:
   
   ![](assets/api_helper_2.png) 

   ![](assets/api_helper_1.png)

-->

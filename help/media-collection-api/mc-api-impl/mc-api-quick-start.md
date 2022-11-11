---
title: "API för direktuppspelning av mediainsamling - snabbstart"
description: Kom igång med API:t för direktuppspelande media. Lär dig hur du snabbt verifierar data för din begäran.
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Snabbstart{#quick-start}

>[!TIP]
>
>Samla in de data som behövs för att slutföra ett projekt [Sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) till bakomliggande server för Media Analytics (MA) Collection API. Du kan snabbt verifiera data i din begäran genom att skicka förfrågningar manuellt (med `curl`, eller Postman osv.). Detta ger dig omedelbar feedback om du har problem med felaktiga datatyper eller felaktig information i din begäran. Använd [JSON-valideringsscheman](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) för att verifiera att du har angett korrekta data för begäran.

1. Samla in de Adobe Analytics- och Visitor-data som behövs för att köra något av Experience Cloud-programmen:

   * Besökarens Experience Cloud organisation-ID
   * Användar-ID för besökare i Experience Cloud
   * Analytics Report Suite-ID
   * URL för analysspårningsserver

1. Skapa ett JSON-objekt för `sessions` begärandetext, som innehåller de minimidata som krävs för ett lyckat anrop. Exempel:

   ```
   { 
       "playerTime": { 
           "playhead": 0, 
           "ts": 1234560890123 
       }, 
       "eventType": "sessionStart", 
       "params": { 
           "media.playerName": "sample-html5-api-player", 
           "analytics.trackingServer": "[YOUR_TS]", 
           "analytics.reportSuite": "[YOUR_RSID]", 
           "media.contentType": "VOD", 
           "media.length": 60.39333333333333, 
           "media.id": "MA Collection API Sample Player", 
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]", 
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe", 
           "media.channel": "sample-channel", 
           "media.sdkVersion": "va-api-0.0.0", 
           "analytics.enableSSL": false 
       } 
   }
   ```

   >[!NOTE]
   >
   >Du måste använda rätt datatyper i JSON-begärandetexten. t.ex., `analytics.enableSSL` kräver ett booleskt värde, `media.length` är numerisk osv. Du kan kontrollera parametertyper och obligatoriska eller valfria krav genom att markera [JSON-valideringsscheman.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Skicka sessionsbegäranden till API-slutpunkten för MA-samling. Om nyttolasten är ogiltig identifierar du problemet och försöker igen tills du får en `201 Created` svar. I den här `curl` JSON-begärandetexten finns i en fil med namnet `sample_data_session`:

   ```
   $ curl -i -d \ 
     @sample_data_session https://{uri}/api/v1/sessions \ 
     > curl.sessions.out 
   
   $ cat curl.sessions.out 
   HTTP/1.1 201 Created 
   Server: nginx/1.13.5 
   Date: Mon, 18 Dec 2017 22:34:12 GMT 
   Content-Type: application/octet-stream 
   Content-Length: 0 
   Connection: keep-alive 
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: * 
   Access-Control-Allow-Methods: OPTIONS,POST,PUT 
   Access-Control-Allow-Headers: Content-Type 
   Access-Control-Expose-Headers: Location
   ```

Om [Sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) lyckas får du en `201 Created` samma svar som ovan. Svaret innehåller ett sessions-ID i platshuvudet. Sessions-ID är den viktigaste informationen i svaret, eftersom det krävs för alla efterföljande spårningsanrop. När en [Sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)kan du med tillförsikt fortsätta implementera videospårning med hjälp av MA API i videospelaren.

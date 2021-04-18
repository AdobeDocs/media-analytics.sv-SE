---
title: Snabbstart
description: Snabbstart
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Snabbstart{#quick-start}

>[!TIP]
>
>Samla in de data som behövs för att slutföra en lyckad [sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) till bakomliggande server för Media Analytics-samlingen (MA). Du kan snabbt verifiera dina begärandedata genom att skicka förfrågningar manuellt (med `curl`, eller Postman, osv.). Detta ger dig omedelbar feedback om du har problem med felaktiga datatyper eller felaktig information i din begäran. Använd [JSON-valideringsscheman](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) för att verifiera att du anger korrekta begärandedata.

1. Samla in de Adobe Analytics- och Visitor-data som behövs för att köra något av Experience Cloud-programmen:

   * Besökarens Experience Cloud organisation-ID
   * Användar-ID för besökare i Experience Cloud
   * Analytics Report Suite-ID
   * URL för analysspårningsserver

1. Skapa ett JSON-objekt för din `sessions`-begärandebrödtext, som innehåller de minimidata som krävs för ett lyckat anrop. Exempel:

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
   >Du måste använda rätt datatyper i JSON-begärandetexten. `analytics.enableSSL` kräver t.ex. ett booleskt värde, `media.length` är numeriskt osv. Du kan kontrollera parametertyper och obligatoriska eller valfria krav genom att kontrollera [JSON-valideringsscheman.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Skicka sessionsbegäranden till API-slutpunkten för MA-samling. Om nyttolasten för din begäran är ogiltig identifierar du problemet och försöker igen tills du får ett `201 Created`-svar. I det här `curl`-exemplet finns JSON-begärandetexten i en fil med namnet `sample_data_session`:

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

Om [sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) lyckas får du ett `201 Created`-svar som liknar det ovan. Svaret innehåller ett sessions-ID i platshuvudet. Sessions-ID är den viktigaste informationen i svaret, eftersom det krävs för alla efterföljande spårningsanrop. När en [sessionsbegäran](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) har returnerats kan du fortsätta implementera videospårning med MA API i videospelaren.

---
title: Spåra hämtat innehåll
description: Lär dig hur du använder funktionen Hämtat innehåll för att spåra medieförbrukning när en användare är offline.
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: 8da6889ecb50edd12b7ea4139500c35b923830f2
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# Spåra hämtat innehåll{#track-downloaded-content}

## Översikt {#overview}

Funktionen för hämtat innehåll gör det möjligt att spåra medieanvändning när en användare är offline. En användare kan till exempel hämta och installera en app på en mobilenhet och sedan använda appen för att hämta innehåll till den lokala lagringen på enheten. För att spåra nedladdade data utvecklade Adobe funktionen för nedladdat innehåll. Med den här funktionen lagras spårningsdata på enheten när användaren spelar upp innehåll från enhetens lagring, oavsett enhetens anslutning. När användaren är klar med uppspelningssessionen och enheten återgår online, skickas den lagrade spårningsinformationen till Media Collection API:ts baksida i en enda nyttolast. Den lagrade spårningsinformationen bearbetas sedan och rapporteras som vanligt i Media Collection API.

Jämför de två metoderna:

* Online

   Med den här realtidsmetoden skickar mediespelaren spårningsdata för varje spelarhändelse och skickar nätverkssamtal var tionde sekund (varje sekund för annonser), en i taget till baksidan.

* Offline (funktionen Hämtat innehåll)

   Med denna gruppbearbetningsmetod måste samma sessionshändelser genereras, men de lagras på enheten tills de skickas till back end som en enda session (se exemplet nedan).

Varje strategi har sina fördelar och nackdelar:
* Scenariot online spåras i realtid. Detta kräver en anslutningskontroll före varje nätverksanrop.
* Offlinescenariot (funktionen Hämtat innehåll) behöver bara en nätverksanslutningskontroll, men kräver också större minnesutrymme på enheten.

## Implementering {#implementation}

### Plattformar som stöds

Innehållsspårning stöds på iOS- och Android-mobilenheter.

### Händelsescheman

Funktionen för nedladdat innehåll är en offlineversion av (standard) API:t för onlinematerial, så händelsedata som spelaren batchar och skickar till back end måste använda samma händelsescheman som du använder när du gör onlineanrop. Mer information om dessa scheman finns i:
* [Översikt;](/help/media-collection-api/mc-api-overview.md)
* [Validerar händelsebegäranden](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordning för händelser

* Den första händelsen i batchnyttolasten måste vara `sessionStart` som vanligt med Media Collection API.
* **Du måste inkludera metadataparametrarna (`media.downloaded: true`** nyckeln) `params` i  `sessionStart` händelsen för att ange för backend-mottagaren att du skickar hämtat innehåll. Om den här parametern inte finns eller är inställd på false när du skickar hämtade data returnerar API:t en 400-svarskod (felaktig begäran). Den här parametern skiljer nedladdat och direktsänt innehåll från baksidan. Om `media.downloaded: true` anges för en live-session resulterar detta även i ett 400-svar från API:t.
* Det är implementeringens ansvar att lagra spelarhändelser korrekt i den ordning de visas.

### Svarskoder

* 201 - Skapad: Slutförd begäran; data är giltiga och sessionen skapades och kommer att bearbetas.
* 400 - Ogiltig begäran; Schemavalideringen misslyckades, alla data ignoreras och inga sessionsdata bearbetas.

## Integrering med Adobe Analytics {#integration-with-adobe-analtyics}

När du beräknar anrop för att starta/stänga analysen för det hämtade innehållsscenariot anger back-end ett extra analysfält med namnet `ts.` Dessa är tidsstämplar för de första och sista händelser som tas emot (start och slutförd). Den här funktionen gör att en slutförd mediesession kan placeras vid rätt tidpunkt (dvs. även om användaren inte ansluter igen på flera dagar, rapporteras mediesessionen ha inträffat vid den tidpunkt då innehållet visades). Du måste aktivera den här funktionen på Adobe Analytics-sidan genom att skapa en _tidsstämpelsrapport (valfri)._ Information om hur du aktiverar en tidsstämpelsrapport (valfri) finns i  [Tidsstämplar (valfritt).](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html)

## Exempel på sessionsjämförelse {#sample-session-comparison}

### Onlineinnehåll

```
POST /api/v1/sessions HTTP/1.1

{
  eventType: "sessionStart",
  playerTime: {
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ }
}
```

### Hämtat innehåll

```
POST /api/v1/downloaded HTTP/1.1

[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },  
    params:{...},
    customMetadata:{},  
    qoeData:{}
},
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}},
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}},
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}},
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},},
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559}
}]
```

### Meddelande om borttagning

>[!IMPORTANT]
>
>Det hämtade innehållet kunde tidigare också skickas till API:t `/api/v1/sessions`. Det här sättet att spåra hämtat innehåll är **inaktuellt** och kommer att **tas bort** i framtiden.


API:t `/api/v1/sessions` accepterar endast sessioninitieringshändelser.
När du använder det nya API:t behövs inte längre den tidigare obligatoriska `media.downloaded`-flaggan.
Vi rekommenderar starkt att du använder API:t `/api/v1/downloaded` för implementeringar av nytt nedladdat innehåll, samt att du uppdaterar befintliga implementeringar som är beroende av det gamla API:t.


```
POST /api/v1/sessions HTTP/1.1
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },
    params:{
        "media.downloaded": true,
        ...
    },
    customMetadata:{},  
    qoeData:{}
},
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}},
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}},
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}},
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},},
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559}
}]
```

## API-referens för mediespårare

Mer information om hur du konfigurerar hämtat innehåll finns i [API-referens för mediespåraren](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#media-api-reference).

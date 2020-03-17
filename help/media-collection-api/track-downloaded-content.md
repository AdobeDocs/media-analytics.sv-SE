---
title: Spåra hämtat innehåll
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Spåra hämtat innehåll{#track-downloaded-content}

## Översikt {#overview}

Funktionen för hämtat innehåll gör det möjligt att spåra medieanvändning när en användare är offline. En användare kan till exempel hämta och installera ett program på en mobilenhet. Användaren hämtar sedan innehåll med appen till den lokala lagringen på enheten. Adobe har utvecklat funktionen för nedladdat innehåll för att spåra dessa nedladdade data. Med den här funktionen lagras spårningsdata på enheten när användaren spelar upp innehåll från enhetens lagring, oavsett enhetens anslutning. När användaren är klar med uppspelningssessionen och enheten returnerar online, skickas den lagrade spårningsinformationen till Media Collection API:ts baksida i en enda nyttolast. Därifrån sker bearbetningen och rapporteringen som vanligt i Media Collection API.

Jämför de två metoderna:

* Online

   Med den här realtidsmetoden skickar mediespelaren spårningsdata vid varje spelarhändelse och skickar nätverkssamtal var 10:e sekund (varje sekund för annonser), en i taget till baksidan.

* Offline (funktionen Hämtat innehåll)

   Med denna gruppbearbetningsmetod måste samma sessionshändelser genereras, men de lagras på enheten tills de skickas till back end som en enda session (se exemplet nedan).

Varje strategi har sina fördelar och nackdelar:
* Scenariot online spåras i realtid. Detta kräver en anslutningskontroll före varje nätverksanrop.
* Offlinescenariot (funktionen Hämtat innehåll) behöver bara en nätverksanslutningskontroll, men kräver också större minnesutrymme på enheten.

## Implementering {#implementation}

### Händelsescheman

Funktionen för nedladdat innehåll är helt enkelt offline-versionen av (standard) API:t för onlinematerial, så händelsedata som spelaren batchar och skickar till back end måste använda samma händelsescheman som du använder när du ringer online. Mer information om dessa scheman finns i:
* [Översikt;](/help/media-collection-api/mc-api-overview.md)
* [Validerar händelsebegäranden](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordning för händelser

* Den första händelsen i batchnyttolasten måste vara `sessionStart` som vanligt med Media Collection API.
* **Du måste inkludera standardmetadataparametrarna (`media.downloaded: true`**key)`params``sessionStart`för händelsen för att ange för back-end att du skickar hämtat innehåll. Om den här parametern inte finns eller är inställd på false när du skickar hämtade data returnerar API:t en 400-svarskod (felaktig begäran). Den här parametern skiljer nedladdat och direktsänt innehåll från baksidan. (Observera att om`media.downloaded: true`detta anges för en live-session, kommer det även att resultera i ett 400-svar från API:t.)
* Det är implementeringens ansvar att lagra spelarhändelser korrekt i den ordning de visas.

### Svarskoder

* 201 - Skapad: Slutförd begäran; data är giltiga och sessionen skapades och kommer att bearbetas.
* 400 - Ogiltig begäran; Schemavalideringen misslyckades, alla data ignoreras och inga sessionsdata bearbetas.

## Integrering med Adobe Analytics {#integration-with-adobe-analtyics}

När du beräknar anropen för att starta/stänga analysen för det hämtade innehållsscenariot, anger back end ett extra analysfält som kallas `ts.` Dessa är tidsstämplar för den första och sista händelsen som tas emot (start och slutförd). Den här funktionen gör att en slutförd mediesession kan placeras vid rätt tidpunkt (dvs. även om användaren inte ansluter igen på flera dagar, rapporteras mediesessionen ha inträffat vid den tidpunkt då innehållet visades). Du måste aktivera den här funktionen på Adobe Analytics-sidan genom att skapa en _tidsstämpelsrapport (valfritt)._ Information om hur du aktiverar en tidsstämpelsrapport (valfri) finns i [Tidsstämplar (valfritt).](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Exempel på sessionsjämförelse {#sample-session-comparison}

```
[url]/api/v1/sessions
```

### Onlineinnehåll

```
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
[{ 
    eventType: "sessionStart", 
    playerTime:{
      playhead: 0, 
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
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


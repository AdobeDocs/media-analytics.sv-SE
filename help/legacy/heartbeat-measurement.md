---
title: Om mätning av hjärtslag
description: Lär dig hur hjärtslag används för att samla in videostatistik.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 27%

---

# Om mätning av pulsslag

Adobe Streaming Media Collection samlar in videostatistik med &quot;hjärtslag&quot;. Under videouppspelningen skickas pulsslag till en spårningsserver för att mäta uppspelningstiden. Pulsslagsanropen skickas var tionde sekund. Pulsslagen genererar detaljerad statistik om videoengagemang och mer korrekta rapporter om videobortfall. Direktuppspelande media-mätningar fångar pulsen med Adobe Launch med Media Analytics-tillägget, Media SDK och Media Collection API. Komponenterna `AppMeasurement` och `VisitorID` används för att ta emot videodata.

Att använda pulsslag i Streaming Media Collection ger följande fördelar:

| Funktion | Beskrivning |
|---|---|
| Mediehändelser | Detaljerade och anpassade händelser skickas var 10:e sekund för huvudinnehållet och varje sekund för annonser |
| Mätvärden och mått | Tydliga standardiserade mätvärden, dimensioner och riktvärden för olika leverantörer. Med en standardiserad lösning för alla plattformar kan ni använda enhetliga, standardiserade variabler för alla medier och plattformar för att få en effektivare jämförelse mellan kampanjer, enheter och leverantörer. |
| Integreringar | Experience Cloud ID är länkat till Adobe Experience Cloud för enklare korsanalys. Med automatisk integrering med Adobe Experience Cloud kan ni segmentera era mediemålgrupper, inrikta er på dem och ta fram medierekommendationer utifrån användarnas önskemål. |
| Priser | Genomskinlig spårning efter medieström (enkel) |
| Implementering och support | Effektiv konfiguration med pågående uppdateringar och förbättringar. Med en smidig implementeringsprocess kan du snabbt mappa variabler via spelar-API:t och validera implementeringar med Adobe Debug Tool för att säkerställa att alla nödvändiga variabler spåras korrekt. |
| Partnerdelning | Federated Media och Certified Metrics. Med delade data via Federated Media kan ni utnyttja våra branschledande funktioner för mediedelning för att utvärdera data enhetligt i alla mediedistributionspartners - operatörer, programmerare och distributörer. |
| Avancerad spårning | Hämtade innehållsspårning, spårning av felåterställning och samtidiga visningsprogram. Du kan spåra direktuppspelat medieinnehåll som har laddats ned och spelats upp på en enhet oavsett dess anslutningsmöjligheter. |

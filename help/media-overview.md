---
title: Mäta spelmedia i Adobe Analytics
description: Adobe Analytics for Media (även kallat Media Analytics) ger kunderna robusta mediemätningar för innehåll, ljud och annonser.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: fdec4da99a43d889690638f1ff3579e145548b69
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 85%

---


# Mäta spelmedia i Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banderoll](./assets/media_analytics_banner.png)

## Om Adobe Analytics for Streaming Media

Adobe Analytics for Streaming Media är ett tillägg till Adobe Analytics som innehåller kraftfulla mätverktyg för ljud, video och reklam. Adobe Analytics ingår i Adobe Experience Platform.

Med Adobe Analytics for Streaming Media kan ni spåra hela kundresan på er webbplats. Mätvärdena kan enkelt integreras i Adobe Analytics-rapporter och andra Adobe Experience Cloud-produkter. Med mediemätning kan ni kategorisera data i flera dimensioner och segment och samla in alla metadata ni behöver för att göra en fullständig och detaljerad analys. Sedan kan ni analysera data och attribuera framgångsmått för helt konsumerad media, genomsnittlig tid som tillbringats på platsen och slutförda annonser.

Ni kan mäta viktiga leveransvärden som rör QoS, som uteslutna bildrutor, tidsåtgång för buffring och genomsnittlig bithastighet. Och ni kan kombinera mätvärdena med webbplats- eller appdata för att visualisera kundens väg och intressen, så att ni kan ta fram bättre rekommendationer och personalisera kundupplevelserna med Adobe Experience Cloud.

## Funktioner {#features}

Fördelarna med Adobe Analytics för Streaming Media är bland annat övervakning i realtid, detaljerad analys, användbara insikter och möjligheter till intäktsgenerering.
* **Realtidsanalys** – Fatta smarta beslut i realtid med hjälp av nyckeltal som varaktighet, ex2 och ex3 över flera kanaler. Huvudsakliga innehållshändelser mäts i intervall på 10 sekunder för att fånga all aktivitet när den inträffar. Annonsspårningshändelser utförs med intervall på 1 sekund.
* **Öka engagemanget** – Engagera användarna mer med färre buffringshändelser och förstå var och när annonser ska spelas upp i innehållet för att skapa en smidig, mindre påträngande upplevelse som får användarna att komma tillbaka.
* **Heltäckande bild** – Kombinera flera datapunkter för alla innehållsdistributörer för att få en fullständig bild av alla medieaktiviteter. Mät engagemang och visningar/avlyssningar i alla möjliga kanaler via funktionen Federated Analytics.
* **Ökad detaljrikedom** – Utvärdera tittarnas beteende på den mest detaljerade nivån, inklusive besökstid, samtidigt antal tittare/lyssnare per minut och genomsnittlig tid som innehållet konsumeras.
* **Exakta mätningar** – Mät över olika enheter som används för mediekonsumtion, bland annat OTT-enheter, smarttelefoner, surfplattor och datorer, och övervaka användarnas engagemangsmönster och vanor.
* **Segmentering** – Använd klassificeringar för spelare, enheter, genrer, kapitel och shower för att se hur de påverkar övergripande visningar/avlyssningar och kundernas engagemang med innehåll, ljud och annonser samt kombinationer av dem.

## Mätning av pulsslag {#heartbeat}

Adobe Analytics använder ”pulsslag” för att samla in videostatistik. Under videouppspelningen skickas pulsslag till en spårningsserver för att mäta uppspelningstiden. Pulsslagsanropen skickas var tionde sekund. Pulsslagen genererar detaljerad statistik om videoengagemang och mer korrekta rapporter om videobortfall. Adobe Analytics for Streaming Media-mätning fångar pulsen med Adobe Launch med Media Analytics-tillägget, Media SDK och Media Collection API. Komponenterna `AppMeasurement` och `VisitorID` används för att ta emot videodata.

Att använda pulsslag Adobe Analytics för direktuppspelande media ger följande fördelar:

| Funktion | Beskrivning |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Mediehändelser | Detaljerade och anpassade händelser skickas var 10:e sekund för huvudinnehållet och varje sekund för annonser |
| Mätvärden och mått | Tydliga standardiserade mätvärden, dimensioner och riktmärken för alla leverantörer<br>Med en standardiserad lösning för alla plattformar kan ni använda enhetliga, standardiserade variabler för alla medier och plattformar för att få en effektivare jämförelse mellan kampanjer, enheter och leverantörer. |
| Integreringar | Experience Cloud ID är länkat till Adobe Experience Cloud för enklare korsanalys<br>Tack vare den automatiska integreringen med Adobe Experience Cloud kan ni segmentera mediemålgrupper, inrikta er på dem och ta fram medierekommendationer baserat på användarnas önskemål. |
| Priser | Genomskinlig spårning efter medieström (enkel) |
| Implementering och support | Effektiv konfiguration med kontinuerliga uppdateringar och förbättringar<br>Tack vare den smidiga implementeringsprocessen kan ni snabbt mappa variabler via spelar-API:et och validera implementeringar med Adobe Debug Tool för att säkerställa att alla nödvändiga variabler spåras korrekt. |
| Partnerdelning | Federated Analytics och certifierade mätvärden<br>Tack vare delade data via Federated Analytics kan ni använda våra branschledande funktioner för mediedelning för att utvärdera data enhetligt för alla mediedistributionspartners som operatörer, programplanerare och distributörer. |
| Avancerad spårning | Spårning av hämtat innehåll, spårning av felåterställning och samtidiga visningsprogram<br>Du kan spåra direktuppspelat medieinnehåll som har laddats ned och spelats upp på en enhet oavsett dess anslutningsmöjligheter. |



## Säkerhet {#security}

På Adobe tar vi säkerheten för ert digitala material på allvar. Från ett rigoröst säkerhetstänk i våra interna processer och verktyg för programutveckling till våra funktionsövergripande incidentresponsteam så strävar vi efter att alltid ligga steget före och vara flexibla. Vårt samarbete med partners, forskare och andra branschorganisationer hjälper oss dessutom att få insikt om de senaste hoten och de bästa arbetsmetoderna samt att kontinuerligt bygga in säkerhet i de produkter och tjänster vi erbjuder.


### Transport Layer Security {#transport-layer-security}

**TLS-meddelande –** Adobe har standarder för säkerhetsefterlevnad som kräver att äldre säkerhetsprotokoll dras tillbaka. För att fortsätta uppfylla säkerhetsprotokollstandarderna går Adobe mot att använda TLS 1.2 för att använda den senaste och säkraste versionen. Från och med 20 februari 2019 har Adobe endast stöd för TLS 1.1 och senare. I och med den här ändringen kommer Adobe inte längre att samla in data från slutanvändare med äldre enheter eller webbläsare som använder TLS 1.0. Att migrera till TLS 1.2 ger högre säkerhet. Det är viktigt att du går igenom detaljerna och planerar ändringarna för en smidig övergång.

>[!NOTE]
>
>TLS är för närvarande det vanligaste säkerhetsprotokollet i webbläsare och andra program när data måste utväxlas säkert över nätverk.

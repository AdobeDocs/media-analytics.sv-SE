---
title: Mäta ljud och video i Adobe Analytics
description: Adobe Analytics for Media (även kallat Media Analytics) ger kunderna robusta mediemätningar för innehåll, ljud och annonser.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: bddcbcd844145788518c60399bee9e4744e42d3a

---


# Mäta ljud och video i Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banderoll](./assets/media_analytics_banner.png)

## Om Adobe Analytics för ljud och video

Adobe Analytics for Audio and Video är ett tillägg till Adobe Analytics som innehåller kraftfulla mätverktyg för ljud, video och reklam. Adobe Analytics ingår i Adobe Experience Platform.

Med Adobe Analytics för ljud och video kan ni spåra hela kundresan på hela webbplatsen. Mätvärdena kan enkelt integreras i Adobe Analytics-rapporter och andra Adobe Experience Cloud-produkter. Med mediemätning kan ni kategorisera era data i flera dimensioner och segment och samla in alla metadata ni behöver för att göra en fullständig och detaljerad analys. Sedan kan ni analysera data och attribuera resultatkriterier för helt förbrukade media, genomsnittlig tid som tillbringats och slutförda annonser.

Du kan mäta vitala leveransvärden relaterade till QoS, t.ex. uteslutna bildrutor, använd buffringstid och genomsnittlig bithastighet. Och mätvärdena kan kombineras med era webbplats- eller appdata för att visualisera kundens väg och intressen, för att ge förbättrade rekommendationer och personalisera kundupplevelser med Adobe Experience Cloud.

## Funktioner {#features}

Fördelarna med Adobe Analytics för ljud och video omfattar övervakning i realtid, detaljerad analys, användbara insikter och intäktsmöjligheter.
* **Realtidsanalys**- Fatta konkreta, åtgärdbara beslut i realtid med nyckeltal som duration, ex2 och ex3, i flera kanaler. Huvudsakliga innehållshändelser mäts i intervall på 10 sekunder för att fånga all aktivitet när den inträffar. Annonsspårningshändelser utförs med intervall på 1 sekund.
* **Öka engagemanget**- Engagera användarna fullständigt genom färre buffringshändelser och förstå var och när annonser ska spelas upp i innehållet för att skapa en smidig och mindre påträngande upplevelse som levererar återkommande besök.
* **Holistisk bild**- Kombinera flera datapunkter för alla era innehållsdistributörer för att få en fullständig bild av alla era medieaktiviteter. Mät engagemanget och se/lyssna på alla möjliga kanaler med funktionen för federerad analys.
* **Ökad granularitet**- Utvärdera tittarnas beteende på den mest detaljerade nivån, inklusive besökarnas tid på dygnet, samtidigt antal tittare/avlyssnare per minut och genomsnittlig tid som innehållet förbrukades.
* **Exakt mätning**- Mät i olika enheter som används för mediekonsumtion, inklusive OTT, smarttelefon, surfplatta, dator med mera, för att övervaka användarnas engagemangsmönster och vanor.
* **Segmentering**- Använd klassificeringar på spelare, enheter, genrer, kapitel och bildspel för att se hur de påverkar era övergripande vyer/avlyssningar och kundernas engagemang med innehåll, ljud, annonser och kombinationer.

## Mätning av pulsslag {#heartbeat}

Adobe Analytics använder&quot;hjärtslag&quot; för att samla in videostatistik. Under videouppspelningen skickas hjärtslag till hjärtslagets spårningsserver för att mäta uppspelningstiden. Anrop om hjärtslag skickas var tionde sekund. Heartbeats ger detaljerade videointeraktionsvärden och exaktare videofallorapporter. Adobe Analytics for Audio and Video-mätningar fångar pulsen med Adobe Launch med Media Analytics-tillägget, Media SDK och Media Collection API. Komponenterna `AppMeasurement` och `VisitorID` används för att ta emot videodata.

Adobe Analytics för ljud och video har följande fördelar:

| Funktion | Beskrivning |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Mediehändelser | Detaljerade och anpassade händelser skickas var 10:e sekund för huvudinnehållet och var 1:e sekund för annonser |
| Mätvärden och mått | Tydliga standardiserade mätvärden, dimensioner och riktmärken för olika<br>leverantörerMed en standardiserad lösning för alla plattformar kan ni använda enhetliga, standardiserade variabler för alla medier och plattformar för att få en effektivare jämförelse mellan kampanjer, enheter och leverantörer. |
| Integreringar | Experience Cloud ID är länkat till Adobe Experience Cloud för enklare<br>korsanalysMed automatisk integrering med Adobe Experience Cloud kan ni segmentera era mediemålgrupper, inrikta er på dem och göra medierekommendationer baserat på användarpreferenser. |
| Priser | Genomskinlig spårning efter medieström (enkel) |
| Implementering och support | Effektiv konfiguration med pågående uppdateringar och<br>förbättringarMed en smidig implementeringsprocess kan du snabbt mappa variabler via spelar-API:t och validera implementeringar med Adobe Debug Tool för att säkerställa att alla nödvändiga variabler spåras korrekt. |
| Partnerdelning | Federated Analytics and Certified Metrics<br>With shared data through Federated Analytics, you can capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors. |
| Avancerad spårning | Spårning av hämtat innehåll, spårning av felåterställning och samtidiga<br>visningsprogramDu kan spåra ljud- och videoinnehåll som laddas ned och spelas upp på en enhet oavsett dess anslutning. |



## Säkerhet {#security}

På Adobe tar vi säkerheten för era digitala resurser på allvar. Från vår rigorösa integrering av säkerhet i vår interna programutvecklingsprocess och verktyg till våra funktionsövergripande incidentresponsteam - vi strävar efter att vara proaktiva och omöjliga. Dessutom hjälper vårt samarbete med partners, forskare och andra branschorganisationer oss att förstå de senaste hoten och bästa säkerhetspraxis, samt att kontinuerligt bygga in säkerheten i de produkter och tjänster vi erbjuder.


### Transport Layer Security {#transport-layer-security}

**TLS-meddelande –** Adobe har standarder för säkerhetsefterlevnad som kräver att äldre säkerhetsprotokoll dras tillbaka. För att fortsätta uppfylla säkerhetsprotokollstandarderna går Adobe mot att använda TLS 1.2 för att använda den senaste och säkraste versionen. Från och med 20 februari 2019 har Adobe endast stöd för TLS 1.1 och senare. I och med den här ändringen kommer Adobe inte längre att samla in data från slutanvändare med äldre enheter eller webbläsare som använder TLS 1.0. Att migrera till TLS 1.2 ger högre säkerhet. Det är viktigt att du går igenom detaljerna och planerar ändringarna för en smidig övergång.

>[!NOTE]
>
>TLS är för närvarande det vanligaste säkerhetsprotokollet i webbläsare och andra program när data måste utväxlas säkert över nätverk.

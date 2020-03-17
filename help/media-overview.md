---
title: Mäta ljud och video i Adobe Analytics
description: 'Adobe Analytics for Media (även kallat Media Analytics) ger kunderna robusta mediemått för innehåll, ljud och annonser. '
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: 689b7d4ce632d3ddba6704bb8040eec52bfc326f

---


# Mäta ljud och video i Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banderoll](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>Dokumentationen här är specifik för kunder som använder version 1.5 eller senare av Adobes *Media SDK* för hjärtslagsmätning eller Adobes nyare *Media Collection API* för hjärtslagsmätning. Det innehåller inga instruktioner om den gamla implementeringen av videon Milestone. Vi uppmuntrar alla kunder att gå mot att använda en eller båda av de två senaste mediespårningslösningarna för att dra nytta av förbättringar och utökad mätning. Du kan se [fördelarna med att gå över till de senaste lösningarna](media-overview.md#heartbeat-versus-milestone-benefits) nedan. Vi kommer att fortsätta att ha stöd för milstolpe-metoden för att spåra videoklipp, men det kommer inte att finnas några planerade uppdateringar, korrigeringar eller funktionsförbättringar. Kontakta din kontoansvarige på Adobe om du har ytterligare frågor.

## Översikt {#overview}

Adobe Analytics for Media (även kallat Media Analytics) är ett tillägg till grundanalyseringserbjudandet som ger kunderna robusta mediemätningar för innehåll, ljud och annonser. Media Analytics ger kunderna många fördelar och möjliggör övervakning i realtid, detaljerad analys, användbara insikter och intäktsmöjligheter.

Mediespårning aktiveras genom något av följande:

* **Media SDK -** Kan integreras med de vanligaste mediespelarna.
* **Media Collection API -** (RESTful API) Integreras med spelare som saknar SDK-stöd för (eller med spelare som inte kräver SDK-integrering).

Med Adobe Analytics for Media kan kunderna spåra hela kundresan på webbplatsen, inklusive mediekonsumtion, och dessa mått kan enkelt integreras i Analytics-rapporter och andra Experience Cloud-produkter. Med mediemätning kan ni segmentera och dela upp era data i flera dimensioner och segment, samla in alla metadata ni behöver för att göra en fullständig detaljerad analys och attribuera resultatkriterier till helt förbrukade medier, genomsnittlig tid som tillbringats och slutförda annonser.

Medielösningarna mäter inte bara viktiga leveransvärden relaterade till QoS, som uteslutna bildrutor, tidsåtgången för buffring och genomsnittlig bithastighet. De kan också kombineras med era webbplats- eller appdata för att visualisera kundflödet och deras intressen, för att bättre kunna göra rekommendationer och personalisera sina upplevelser via Adobe Experience Cloud.

## Fördelar {#benefits}

Några av fördelarna med Adobes mediemätningslösningar:

* **Tidsbestämd analys -** Fatta konkreta, åtgärdbara beslut i realtid med nyckeltal (t.ex. varaktighet) i flera kanaler. Huvudsakliga innehållshändelser mäts i **10 sekunders** intervall för att fånga all aktivitet när den inträffar. Annonsuppföljningshändelser inträffar med **1-sekunders** intervall.
* **Öka engagemanget -** Engagera användarna fullständigt genom färre buffringshändelser och förstå var och när annonser ska spelas upp i innehållet för att skapa en smidig, mindre påträngande upplevelse som för användarna tillbaka och ger dem återkommande besök.
* **Holistisk bild -** Kombinera flera datapunkter i alla era innehållsdistributörer för att få en fullständig bild av alla era medieaktiviteter och mät engagemang och vyer/avlyssningar i alla möjliga kanaler via funktionen [Federated Analytics](/help/federated-analytics.md) .
* **Ökad granularitet -** Utvärdera tittarnas beteende på den mest detaljerade nivån, inklusive besökarnas tid på dygnet, samtidigt antal tittare/avlyssnare per minut och genomsnittlig tid som innehållet förbrukades.
* **Exakt mätning -** Mät i de olika enheter som används för mediekonsumtion, inklusive OTT, smarttelefon, surfplatta, dator med mera för att övervaka användarnas engagemangsmönster och vanor.
* **Segmentering -** Använd klassificeringar på spelare, enheter, genrer, kapitel och bildspel för att se hur de påverkar era övergripande vyer/avlyssningar och kundernas engagemang med innehåll, ljud, annonser och kombinationer.

## Fördelar mellan pulsslag och milstolpe {#heartbeat-versus-milestone-benefits}

Adobe Analytics for Media kan mätas på två sätt: den gamla milstolpemetoden (endast video) och den aktuella Heartslag-metoden (ljud och video, som finns i både Media SDK och Media Collection API). Metoden Heartbeats är den bästa mätmetoden och vi uppmuntrar alla kunder att gå över till den här versionen om de inte redan gjort det, för att utnyttja fördelarna som beskrivs nedan.

Den gamla milstolpemetoden baseras på enskilda serveranrop till Analytics-servern, för videostart, kvartiler, varaktighet och slutförande. Metoden Heartbeats ger en mer robust mediespårningslösning som mäter huvudinnehållet med 10-sekunders intervall för att ge förbättrad, standardiserad statistik. Dessutom har Adobe dragit lärdom av vår milstolpe-metod för att skapa en smidigare och smidigare implementeringsprocess via Media SDK eller Media Collection API som används av Heartbeats.

Några av fördelarna med Heartbeats-metoden:

* **Effektiv implementeringsprocess -** Mappa variabler enklare via spelar-API:t och validera implementeringar med Adobe Debug Tool för att säkerställa att alla nödvändiga variabler spåras korrekt.
* **Automatisk integrering** med Adobe Experience Cloud - Utnyttja den automatiska integrationen med Adobe Experience Cloud via Experience Cloud-ID, segmentera era mediepubliken, rikta in dem mot dem och gör medierekommendationer baserat på användarpreferenser.
* **Delade data med Federated Analytics -** Använd våra branschledande mediedelningsfunktioner för att utvärdera data enhetligt i alla era mediedistributionspartners - operatörer, programmerare och distributörer.
* **Standardiserad lösning för alla plattformar -** Aktivera enhetliga, standardiserade variabler för alla medier och plattformar för att möjliggöra en effektivare jämförelse mellan kampanjer, enheter och leverantörer.
* **Spårning av nedladdat innehåll -** Spåra mediematerial (video och ljud) som laddas ned och spelas upp på en enhet oavsett dess anslutning.

### Jämförelsetabell

|  | Videoanalys - milstolpe | Media Analytics - Heartbeats |
|---|---|---|
| **Mediehändelser** | Standardhändelser på hög nivå | Detaljerade och anpassade händelser var 10:e sekund för huvudinnehåll, var 1:e sekund för annonser |
| **Mätvärden och mått** | Avvikelser mellan leverantörer, icke-standardiserade mått och mått | Tydliga, standardiserade mätvärden, dimensioner och riktmärken för olika leverantörer |
| **Integreringar med Adobe-produkter** | Enskilda sessioner med vissa mappningar och integreringar | Stitched Experience Cloud ID linked to full Adobe Experience Cloud för enklare korsanalys |
| **Priser** | Spårat och fakturerat för varje serversamtal | Genomskinlig spårning efter medieström (enkel) |
| **Implementering och support** | Längre integreringar med begränsat stöd för äldre versioner och inga uppgraderingar | Effektiv konfiguration med pågående uppdateringar och förbättringar |
| **Partnerdelning** | Ej tillämpligt | Federated Analytics och Certified Metrics |
| **Avancerad spårning** | Ej tillämpligt | Spårning av felåterställning och samtidiga visningsprogram |

## Enheter som stöds {#devices-supported}

Adobe Analytics for Media har utvecklats i samarbete med branschen för att tillhandahålla kraftfulla datainsamlingsverktyg som säkerställer att alla medieströmmar samlas in och rapporteras på alla meningsfulla enheter. Vår Media SDK har utvecklats för alla de mest använda enheterna, inklusive:

* iOS- och Android-smartphones och surfplattor
* OTT-enheter för ROKU, AppleTV, FireTV och Android TV
* JavaScript Browser for Desktop and Laptop

SDK uppdateras regelbundet när nya versioner av enheter släpps, och du kan använda dessa SDK för att integrera med de flesta av de största mediaspelarna idag, inklusive Brightcove och Oyala.

För enheter och plattformar som för närvarande inte har SDK-stöd (eller även om de gör det) kan du implementera API:t för Media Collection, genom vilket du gör RESTful-API-anrop direkt från enheten/plattformen till Media Analytics-backend.

Tabellen nedan innehåller en lista över de enheter som för närvarande stöds via vår Media SDK-implementering och Media Collection API-implementering. Information om hur du hämtar den senaste versionen av SDK finns i [Hämta SDK:er.](sdk-implement/download-sdks.md) Om det finns en enhet som inte finns med i listan som du vill mäta mot kontaktar du kundtjänst eller din lösningskonsult för att få information om enhetens status.

|      | Media SDK | Media Collection API |
|---|:---:|:---:|
| **JavaScript Browser** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **iOS-enheter** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android-enheter** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Enhetliga Windows-plattformar (UWP)** |  | ![](assets/icon-blue-check.png) |
| **Blackberry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (ny/äldre)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (inbyggt program)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **Fire TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android-TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Kromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(Andra/Nya anslutna enheter)** |  | ![](assets/icon-blue-check.png) |

För Media SDK, se även [Stöd för minimiplattformsversion](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Säkerhet för transportlager {#transport-layer-security}

**TLS Notice —** Adobe har standarder för säkerhetsefterlevnad som kräver att äldre säkerhetsprotokoll upphör att gälla. För att fortsätta uppfylla de föränderliga säkerhetsprotokollstandarderna går Adobe mot att använda TLS 1.2 för att få den senaste och säkraste versionen i bruk. Från och med 20 februari 2019 stöder Adobe endast TLS 1.1 eller senare. Med den här ändringen kommer Adobe inte längre att samla in data från slutanvändare med äldre enheter eller webbläsare som distribuerar TLS 1.0. Att migrera till TLS 1.2 ger bättre säkerhet. Det är viktigt att du går igenom detaljerna och planerar ändringarna för en smidig övergång.

>[!NOTE]
>
>TLS är för närvarande det vanligaste säkerhetsprotokollet som används i webbläsare och andra program som kräver att data utbyts på ett säkert sätt över ett nätverk.


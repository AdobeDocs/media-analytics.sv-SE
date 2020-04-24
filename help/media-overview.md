---
title: Mäta ljud och video i Adobe Analytics
description: 'Adobe Analytics for Media (även kallat Media Analytics) ger kunderna robusta mediemätningar för innehåll, ljud och annonser. '
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: ht
source-git-commit: 689b7d4ce632d3ddba6704bb8040eec52bfc326f

---


# Mäta ljud och video i Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banderoll](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>Den här dokumentationen gäller kunder som använder version 1.5 eller senare av Adobes *Media SDK* för hjärtslagsmätning eller Adobes nyare *Media Collection API* för hjärtslagsmätning. Den innehåller inga instruktioner om den äldre implementeringen för videomilstolpar. Vi uppmuntrar alla kunder att överväga att använda en eller båda av de två senaste mediespårningslösningarna för att dra nytta av förbättringar och utökade mätningar. Du kan se [fördelarna med att byta till de senaste lösningarna](media-overview.md#heartbeat-versus-milestone-benefits) nedan. Vi kommer att fortsätta att stödja milstolpemetoden för att spåra video, men det finns inga planerade uppdateringar, korrigeringar eller funktionsförbättringar. Kontakta din kontoansvarige på Adobe om du har fler frågor.

## Översikt {#overview}

Adobe Analytics for Media (även kallat Media Analytics) är ett tillägg till basprodukten Analytics som ger kunderna robusta mediemätningar för innehåll, ljud och annonser. Media Analytics ger kunderna många fördelar som övervakning i realtid, detaljerade analyser, användbara insikter och intäktsmöjligheter.

Mediespårning aktiveras genom något av följande:

* **Media SDK –** Kan integreras med de populäraste mediespelarna.
* **Media Collection API –** (RESTful API) Integreras med spelare som saknar SDK-stöd (eller med spelare där SDK-integrering inte önskas).

Med Adobe Analytics for Media kan kunderna spåra hela kundresan på webbplatsen, inklusive mediekonsumtion, och dessa mått kan enkelt integreras i Analytics-rapporter och andra Experience Cloud-produkter. Med mediemätningar kan ni segmentera och dela upp era data i flera dimensioner och segment, samla in alla metadata som behövs för en fullständig detaljerad analys och attribuera resultatkriterier till förbrukade medier, genomsnittlig tid och slutförda annonser.

Medielösningarna mäter inte bara viktiga leveransvärden relaterade till QoS, som uteslutna bildrutor, tidsåtgång för buffring och genomsnittlig bithastighet. De kan också kombineras med era webbplats- eller appdata för att visualisera kundflödet och kundernas intressen, så att ni bättre kan göra rekommendationer och personalisera upplevelser via Adobe Experience Cloud.

## Fördelar {#benefits}

Några av de många fördelarna med Adobes mediemätningslösningar:

* **Tidsbaserad analys –** Fatta konkreta, verkställbara beslut i realtid med nyckeltal (t.ex. varaktighet) för flera kanaler. Huvudsakliga innehållshändelser mäts i intervall på **10 sekunder** för att fånga all aktivitet när den inträffar. Annonsspårningshändelser utförs med intervall på **1 sekund**.
* **Öka engagemanget –** Engagera användarna mer med färre buffringshändelser och förstå var och när annonser ska spelas upp i innehållet för att skapa en smidig, mindre påträngande upplevelse som får användarna att komma tillbaka och ger återkommande besök.
* **Holistisk bild –** Kombinera flera datapunkter för alla innehållsdistributörer för att få en fullständig bild av alla era medieaktiviteter och mät engagemang och visningar/avlyssningar i alla möjliga kanaler via funktionen [Federated Analytics](/help/federated-analytics.md).
* **Ökad granularitet –** Utvärdera tittarnas beteende på den mest detaljerade nivån, inklusive besökstid, samtidigt antal tittare/lyssnare per minut och genomsnittlig tid som innehållet konsumeras.
* **Exakta mätningar –** Mätningar på olika enheter som används för mediekonsumtion, bland annat OTT, smartphone, surfplatta, dator med mera, för att övervaka användarnas engagemangsmönster och vanor.
* **Segmentering –** Använd klassificeringar för spelare, enheter, genrer, kapitel och shower för att se hur de påverkar övergripande visningar/avlyssningar och kundernas engagemang med innehåll, ljud och annonser samt kombinationer av dem.

## Fördelar med hjärtslag jämfört med milstolpar {#heartbeat-versus-milestone-benefits}

Adobe Analytics for Media kan mäta på två sätt: med den gamla milstolpemetoden (endast video) och den nuvarande hjärtslagsmetoden (ljud och video, finns i både Media SDK och Media Collection API). Hjärtslagsmetoden är den bästa mätmetoden och vi uppmuntrar alla kunder som inte redan gjort det att gå över till den versionen för att dra nytta av fördelarna som beskrivs nedan.

Den gamla milstolpemetoden baseras på enskilda serveranrop till Analytics-servern för videostart, kvartiler, varaktighet och slutförande. Hjärtslagsmetoden är en robustare lösning för mediespårning som mäter huvudinnehållet med intervall på 10 sekunder för förbättrade, standardiserade mätningar. Dessutom har Adobe dragit lärdom av milstolpemetoden för att skapa en smidigare implementeringsprocess för hjärtslag via Media SDK eller Media Collection API.

Några av de många fördelarna med hjärtslagsmetoden:

* **Smidig implementering –** Mappa variabler enklare via din spelares API och validera implementeringar via Adobe Debug Tool för att säkerställa att alla nödvändiga variabler spåras korrekt.
* **Automatisk integrering med Adobe Experience Cloud** – Dra nytta av den automatiska integreringen med Adobe Experience Cloud via ert Experience Cloud ID, segmentera er mediepublik, anpassa innehåll för dem och gör medierekommendationer baserat på användarpreferenser.
* **Delade data med Federated Analytics –** Använd våra branschledande mediedelningsfunktioner för att utvärdera data enhetligt för alla mediedistributionspartners som operatörer, programmerare och distributörer.
* **Standardiserad lösning för alla plattformar –** Aktivera enhetliga, standardiserade variabler för alla medier och plattformar för effektivare jämförelser av kampanjer, enheter och leverantörer.
* **Spårning av nedladdat innehåll –** Spåra medieinnehåll (video och ljud) som laddas ned och spelas upp på en enhet oavsett anslutning.

### Jämförelsetabell

|  | Videoanalys – milstolpe | Medieanalys – hjärtslag |
|---|---|---|
| **Mediehändelser** | Standardhändelser på hög nivå | Detaljerade och anpassade händelser var 10:e sekund för huvudinnehåll, varje sekund för annonser |
| **Mätvärden och mått** | Avvikelser mellan leverantörer, icke-standardiserade mätvärden och mått | Tydliga, standardiserade mätvärden, mått och riktmärken för olika leverantörer |
| **Integrering med Adobe-produkter** | Enskilda sessioner med vissa mappningar och integreringar | Experience Cloud ID länkat till Adobe Experience Cloud för enklare korsanalys |
| **Priser** | Spåras och faktureras för varje serveranrop | Genomskinlig spårning efter medieström (enkel) |
| **Implementering och support** | Längre integreringar med begränsat stöd för äldre versioner och inga uppgraderingar | Smidig konfigurering med löpande uppdateringar och förbättringar |
| **Partnerdelning** | Ej tillämpligt | Federated Analytics och Certified Metrics |
| **Avancerad spårning** | Ej tillämpligt | Spårning av felåterställning och samtidiga tittare |

## Enheter som stöds {#devices-supported}

Adobe Analytics for Media har utvecklats i samarbete med branschen för att tillhandahålla kraftfulla datainsamlingsverktyg som säkerställer att alla medieströmmar samlas in och rapporteras på alla betydelsefulla enheter. Media SDK har utvecklats för de populäraste enheterna, bland annat:

* iOS- och Android-smartphones och surfplattor
* OTT-enheter för ROKU, AppleTV, FireTV och Android TV
* JavaScript-webbläsare för stationära och bärbara datorer

SDK:erna uppdateras regelbundet när nya versioner av enheterna släpps och du kan använda dessa SDK:er för att integrera med de flesta populära mediespelarna, inklusive Brightcove och Ooyala.

För enheter och plattformar som för närvarande inte har SDK-stöd (eller även om de har det) kan du implementera Media Collection API genom vilket du kan göra RESTful-API-anrop direkt från enheten/plattformen till Media Analytics-serverdelen.

Tabellen nedan innehåller en lista över de enheter som för närvarande stöds via vår Media SDK-implementering och Media Collection API-implementering. Information om hur du hämtar den senaste SDK-versionen finns i [Hämta SDK:er.](sdk-implement/download-sdks.md) Om en enhet som du vill mäta inte finns med i listan kan du kontakta kundtjänsten eller din lösningskonsult för information om enhetens status.

|      | Media SDK | Media Collection API |
|---|:---:|:---:|
| **JavaScript-webbläsare** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **iOS-enheter** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android-enheter** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Enhetliga Windows-plattformar (UWP)** |  | ![](assets/icon-blue-check.png) |
| **Blackberry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (ny/äldre)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (inbyggt program)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **Fire TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(Andra/nya anslutna enheter)** |  | ![](assets/icon-blue-check.png) |

För Media SDK, se även [Stöd för lägsta plattformsversion](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Transport Layer Security {#transport-layer-security}

**TLS-meddelande –** Adobe har standarder för säkerhetsefterlevnad som kräver att äldre säkerhetsprotokoll dras tillbaka. För att fortsätta uppfylla säkerhetsprotokollstandarderna går Adobe mot att använda TLS 1.2 för att använda den senaste och säkraste versionen. Från och med 20 februari 2019 har Adobe endast stöd för TLS 1.1 och senare. I och med den här ändringen kommer Adobe inte längre att samla in data från slutanvändare med äldre enheter eller webbläsare som använder TLS 1.0. Att migrera till TLS 1.2 ger högre säkerhet. Det är viktigt att du går igenom detaljerna och planerar ändringarna för en smidig övergång.

>[!NOTE]
>
>TLS är för närvarande det vanligaste säkerhetsprotokollet i webbläsare och andra program när data måste utväxlas säkert över nätverk.


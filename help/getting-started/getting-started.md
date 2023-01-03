---
title: Komma igång
description: Kom igång med Adobe Analytics for Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: b022bed6b7be0cc97caaaf6b7bbc42474a57b400
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Komma igång {#getting-started}

Adobe Analytics for Streaming Media har två huvudsakliga implementeringsmetoder, Media SDK:er och Media Collection API:er.

![metoder](assets/getting-started2.png)

Använda den inbyggda logiken i **Media SDKs** kan du mäta olika mediaplattformar korrekt, inklusive webbplatser, mobiltelefoner, anslutna tv-apparater, surfplattor, OTT-enheter, digitalboxar och spelkonsoler. Du kan till och med mäta hämtat innehåll. De insikter ni får är djupgående när det gäller användartittarnas engagemang, så att ni kan förstå hur lång tid, när och var tittarna interagerar. Media-SDK:erna använder **Media Collection API:er** för spårning. Media Collection-API:erna är anpassningsbara, om ditt program kräver anpassade spårningsfunktioner. För enheter som inte stöds av Media SDK:er kan du använda Media Collection-API:erna.

Adobe Analytics Streaming Media finns för följande medieplattformar:

* Webb
* Mobil
* Över toppen
* Alla anslutna enheter som kan användas för direktuppspelningsmedia eller en server-till-server-integrering

Mer information finns i [Enheter och plattformar som stöds](/help/getting-started/supported-devices.md).

>[!IMPORTANT]
>
>Om du vill implementera Adobe Analytics Streaming Media kontaktar du säljaren eller kontohanteraren på Adobe för att kontrollera att Streaming Media ingår i produktportföljen.

## Media SDK för direktuppspelande media {#media-sdks}

Media-SDK för direktuppspelningsmedia är tillgängliga för plattformarna JavaScript, Android, iOS, tvOS, Chromecast och Roku.

Mer information om hur du hämtar och installerar SDK:er för media finns i [Hämta SDK:er för media, tillägg med hjälp av taggar och OTT SDK:er](/help/getting-started/download-sdks.md).


## Media Collection API:er {#media-collection-apis}

The **Media Collection API:er** gör att ni kan anpassa implementeringen av medieanalyser. Använd API:erna för Media Collection för att direkt anropa Adobe-servrar för att utföra nästan alla åtgärder du kan utföra med hjälp av SDK:er med mera. Anpassa din datainsamling för att skapa rapporter som utforskar, får insikter eller besvarar viktiga frågor om dina strömmande mediedata.

Mer information om hur du använder API:er för mediainsamling finns i [API-dokumentation för strömmande media](/help/implementation/media-collection-api/mc-api-overview.md).

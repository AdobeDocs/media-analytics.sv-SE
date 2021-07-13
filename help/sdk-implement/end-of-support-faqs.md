---
title: Lär dig mer om vanliga frågor och svar om Media Analytics SDK End of Support
description: Det här avsnittet innehåller frågor och svar om att stödet för SDK:er för Media Analytics har upphört.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---

# Vanliga frågor om supporten för Media Analytics SDK

När stödet för version 4 Mobile SDK upphör den 31 augusti 2021 upphör även stödet för Media Analytics SDK för iOS och Android i Adobe. Efter den 31 augusti 2021 kommer Adobe inte att tillhandahålla korrigeringar, OS-relaterade uppdateringar eller stöd för Media Analytics SDK.  Under migreringen till dessa nya Experience Platform SDK:er måste du komma ihåg att [Media Analytics-tilläggen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) måste implementeras för att Adobe Analytics ska kunna användas för direktuppspelningsmedia.

## De fem viktigaste sakerna att veta

1. Stöd för v4 SDK:er för mobiler kommer inte längre att finnas efter den 31 augusti 2021. Du bör migrera till Adobe Experience Platform (AEP) Mobile SDK för iOS och Android. Mer information finns i [Version 4 Mobile SDKs end-of-support FAQ](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. Analyser för Streaming Media-implementering kräver AEP Mobile SDK och användning av tilläggen Analytics och Media Analytics. Från och med 1 september 2021 bör du använda de nya AEP Mobile SDK:erna och tilläggen.  Media Analytics-tillägg konfigureras med Adobe Launch.  Mer information finns i [Migrera från fristående media SDK till Adobe Launch](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. Funktionsutvecklingen har upphört för Media Analytics SDK:er för iOS och Android.  Nya funktioner som introducerades från och med hösten 2019 aktiveras med Media Analytics-tilläggen och Media Collection API.

1. Roku och Chromecast SDK är fortfarande tillgängliga för Analytics för Streaming Media-kunder. Roku- och Chromecast-SDK:erna kommer att fortsätta förbättras och stödjas som fristående SDK:er.  Om du använder JS SDK för Media Analytics kan du fortsätta använda den fristående SDK:n eller aktivera Media Analytics-tillägget med Adobe Launch.

1. Före den 1 september 2021 får Adobe efter eget gottfinnande ta fram nya korrigeringar för problem med stor teknisk inverkan eller affärsexponering. På grundval av kundernas synpunkter kommer Adobe att fastställa graden av påverkan, exponering och efterföljande aktiviteter.

Kontakta din Customer Success Manager på Adobe om du har några frågor.

## Vanliga frågor

1. **Kommer stödet för Roku och Chromecast SDK att påverkas? &#x200B;**

   Nej.  Roku- och Chromecast-SDK:er stöds för närvarande som fristående SDK:er. &#x200B;
&#x200B;
1. **Kommer JS SDK-implementeringar för Media Analytics att påverkas av den här ändringen &#x200B;?**

   Nej.  Kunder som använder JS SDK för Media Analytics kan fortsätta använda SDK eller aktivera det via Adobe Launch.
&#x200B;
1. **Vilken nivå av insats krävs för att migrera till Media Analytics-tilläggen&#x200B;**

   LOE är beroende av varje kunds implementering, så det varierar.  Efter att ha läst migreringsdokumentationen nedan kan du kontakta konsulttjänster och/eller kundtjänst för att få ytterligare support.

   [Media Analytics-tillägg: Android-migrering](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics-tillägg: iOS-migrering](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics-tillägg: nya implementeringar](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Måste jag ha Launch som tagghanteringssystem? Vad händer om jag inte vill använda Launch?**

   För mobilappsanvändning används Launch inte som ett tagghanteringssystem som det är för webben.  Det krävs ett startgränssnitt för att konfigurera SDK-tilläggen. Detta liknar hur du använder användargränssnittet för Adobe Mobile Services för att konfigurera det mobila v4 SDK:t. Fördelen med att använda Launch är att det ger dig anpassade installationsinstruktioner baserat på det tillägg du väljer.

1. **Påverkar detta slutet på stödet SDK för tvOS?**

   Ja, för tvOS (version 10+) rekommenderas att implementeringen migreras till Media Analytics-tilläggen.  Mer information finns i [Migrera från det fristående Media SDK till Adobe Launch - iOS](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Påverkar detta slutet på stödet SDK för FireTV och AndroidTV &#x200B;?**

   Ja, för FireTV och AndroidTV rekommenderas att migrera till Media Analytics-tilläggen.  Mer information finns i [Migrera från det fristående Media SDK till Adobe Launch - Android](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).

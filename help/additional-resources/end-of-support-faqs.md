---
title: Läs mer om Media Analytics - Vanliga frågor och svar om SDK support
description: Det här avsnittet innehåller frågor och svar om att stödet för SDK:er för Media Analytics har upphört.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Media Analytics Mobile SDK End of Support - frågor och svar

När stödet för version 4 Mobile SDK upphörde den 31 augusti 2021 upphörde även stödet för Media Analytics Mobile SDK för iOS och Android. (Detta omfattar inte Media Analytics SDK för webben (JS) och OTT-plattformar som Chromecast och Roku, som fortfarande stöds.)

Det innebär att Adobe inte längre tillhandahåller korrigeringar, OS-relaterade uppdateringar eller stöd för Media Analytics Mobile SDK. När du migrerar till de nya SDK:erna för Experience Platform ska du vara medveten om att [Media Analytics-tilläggen](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) måste implementeras för att aktivera mediesamlingen för direktuppspelning i Adobe.


## De fem viktigaste sakerna att veta

1. Mobile v4 SDK:er stöds inte längre per den 31 augusti 2021. Du bör migrera till Adobe Experience Platform (AEP) Mobile SDK för iOS och Android.

1. Analytics per contenuti in streaming-implementering kräver AEP Mobile SDK och användning av tilläggen Analytics och Media Analytics. Från och med 1 september 2021 bör du använda de nya AEP Mobile SDK:erna och tilläggen.  Media Analytics-tillägg konfigureras med Adobe-taggar (datainsamling). Mer information finns i [Migrera från fristående media SDK till Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)

1. Funktionsutvecklingen för Media Analytics SDK:er för iOS och Android har upphört. Nya funktioner som introducerades från och med hösten 2019 aktiveras med Media Analytics-tilläggen och Media Collection API.

1. Roku och Chromecast SDK är fortfarande tillgängliga för Analytics per contenuti in streaming-kunder. Roku- och Chromecast-SDK:erna kommer att fortsätta förbättras och stödjas som fristående SDK:er. Om du använder JS SDK for Media Analytics kan du fortsätta använda den fristående SDK eller aktivera Media Analytics-tillägget med Adobe Data Collection (tidigare Adobe Launch).

Kontakta ditt kontoteam på Adobe om du har några frågor.

## Vanliga frågor

1. **Kommer stödet för Roku- och Chromecast-SDK att påverkas? &#x200B;**

   Nej.  Roku- och Chromecast-SDK:er stöds för närvarande som fristående SDK:er. &#x200B;
&#x200B;
1. **Kommer JS SDK-implementeringar för Media Analytics att påverkas av den här ändringen? &#x200B;**

   Nej.  Kunder som använder JS SDK for Media Analytics kan fortsätta använda SDK eller aktivera det via Adobe Launch.
&#x200B;
1. **Vilken nivå av arbete ska migreras till Media Analytics-tilläggen? &#x200B;**

   LOE är beroende av varje kunds implementering, så det varierar.  Efter att ha läst migreringsdokumentationen nedan kan du kontakta konsulttjänster och/eller kundtjänst för att få ytterligare support.

[Media Analytics-tillägg: Android-migrering](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Media Analytics-tillägg: iOS-migrering](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Media Analytics-tillägg: nya implementeringar](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **Måste jag ha Launch som tagghanteringssystem? Vad gör jag om jag inte vill använda Launch?**

   För mobilappsanvändning används Launch inte som ett tagghanteringssystem som det är för webben. Du måste använda startgränssnittet för att konfigurera SDK-tilläggen. Det liknar hur du använder användargränssnittet för Adobe Mobile Services för att konfigurera SDK för mobilen v4. Fördelen med att använda Launch är att det ger dig anpassade installationsinstruktioner baserat på det tillägg du väljer.

1. **Påverkar det här slutet av stödet SDK för tvOS?**

   Ja, för tvOS (version 10+) rekommenderas att migrera till Media Analytics-tilläggen. Mer information finns i [Migrera från det fristående mediet SDK till Adobe Launch - iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **Påverkar det här slutet av stödet SDK för Fire TV och AndroidTV? &#x200B;**

   Ja, för Fire TV och AndroidTV rekommenderas att migrera till Media Analytics-tilläggen. Mer information finns i [Migrera från det fristående mediet SDK till Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).

---
title: Vanliga frågor om supporten för Media Analytics SDK
description: Det här avsnittet innehåller frågor och svar om att stödet för SDK:er för Media Analytics har upphört.
translation-type: tm+mt
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# Vanliga frågor om supporten för Media Analytics SDK

När stödet för version 4 Mobile SDK upphör den 31 augusti 2021 upphör även stödet för Media Analytics SDK för iOS och Android. Efter den 31 augusti 2021 kommer Adobe inte att tillhandahålla korrigeringar, OS-relaterade uppdateringar eller stöd för Media Analytics SDK.  Under migreringen till dessa nya Experience Platform SDK:er måste du tänka på att [Media Analytics-tilläggen](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) måste implementeras för att Adobe Analytics ska kunna aktiveras för ljud och video.

## De fem viktigaste sakerna att veta

1. Stöd för v4 SDK:er för mobiler kommer inte längre att finnas efter den 31 augusti 2021. Du bör migrera till Adobe Experience Platform (AEP) SDK för iOS och Android.

1. Analyser för ljud- och videoimplementering kräver AEP SDK och användning av tilläggen Analytics och Media Analytics. Från och med 1 september 2021 bör du använda de nya AEP SDK:erna och tilläggen.  Media Analytics-tillägg konfigureras med Adobe Launch.  Mer information finns i [Migrera från fristående media SDK till Adobe Launch](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. Funktionsutvecklingen har upphört för Media Analytics SDK:er för iOS och Android.  Nya funktioner som introducerades från och med hösten 2019 aktiveras med Media Analytics-tilläggen och Media Collection API.

1. Roku- och Chromecast-SDK:er är fortfarande tillgängliga för Analytics för ljud- och videokunder. Roku- och Chromecast-SDK:erna kommer att fortsätta förbättras och stödjas som fristående SDK:er.  Om du använder JS SDK för Media Analytics kan du fortsätta använda den fristående SDK:n eller aktivera Media Analytics-tillägget med Adobe Launch.

1. Före den 1 september 2021 kan Adobe efter eget gottfinnande ta fram nya korrigeringar för problem med stor teknisk påverkan eller affärsexponering. Baserat på kundens synpunkter kommer Adobe att fastställa graden av påverkan, exponering och efterföljande aktiviteter.

Kontakta Adobe Customer Success Manager om du har några frågor.

## Vanliga frågor

1. **Kommer stödet för Roku och Chromecast SDK att påverkas? &#x200B;**

   Nej.  Roku- och Chromecast-SDK:er stöds för närvarande som fristående SDK:er. &#x200B; &#x200B;
1. **Kommer JS SDK-implementeringar för Media Analytics att påverkas av den här ändringen &#x200B;?**

   Nej.  Kunder som använder JS SDK för Media Analytics kan fortsätta använda SDK eller aktivera det via Adobe Launch.
&#x200B;
1. **Vilken nivå av insats krävs för att migrera till Media Analytics-tilläggen&#x200B;**

   LOE är beroende av varje kunds implementering, så det varierar.  Efter att ha läst migreringsdokumentationen nedan kan du kontakta konsulttjänster och/eller kundtjänst för att få ytterligare support.

   [Media Analytics-tillägg: Android-migrering](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics-tillägg: iOS-migrering](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics-tillägg: nya implementeringar](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Måste jag ha Launch som tagghanteringssystem? Vad händer om jag inte vill använda Launch?**

   För mobilen krävs Launch för att konfigurera medietillägg som gränssnittet för mobila tjänster. I mobilappens användningsfall används det inte som ett tagghanteringssystem.

1. **Påverkar detta slutet på stödet SDK för tvOS?**

   Ja, för tvOS (version 10+) rekommenderas att implementeringen migreras till Media Analytics-tilläggen.  Stöd för AEP SDK och Media Analytics Extension planeras till juni 2020.  Mer information finns i [Migrera från det fristående Media SDK till Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Påverkar detta slutet på stödet SDK för FireTV och AndroidTV &#x200B;?**

   Ja, för FireTV och AndroidTV rekommenderas att migrera till Media Analytics-tilläggen.  Stöd för AEP SDK och Media Analytics Extension planeras till juni 2020.  Mer information finns i [Migrera från det fristående Media SDK till Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).

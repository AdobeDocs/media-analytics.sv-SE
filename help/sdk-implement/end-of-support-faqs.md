---
title: Media Analytics SDK - slut på vanliga frågor och svar om support
description: I det här avsnittet finns vanliga frågor och svar om att stödet för SDK:er för medieanalys har upphört.
translation-type: tm+mt
source-git-commit: cea8c4b31b21f1b13a55268fbcfb9100a7bdbd7c
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 1%

---


# Media Analytics SDK - slut på vanliga frågor och svar om support

Med slutet på stödet för version 4 Mobile SDKs den 31 augusti 2021 kommer Adobe också att avsluta stödet för Media Analytics SDKs för iOS och Android. Efter den 31 augusti 2021 kommer Adobe inte att tillhandahålla korrigeringar, OS-relaterade uppdateringar eller stöd för Media Analytics SDK.  Under migreringen till dessa nya erfarenhetsplattformar bör du tänka på att [Media Analytics-tillägg](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) måste implementeras om du vill aktivera Adobe Analytics för ljud och video.

## De fem vanligaste sakerna att lära känna

1. Mobile v4 SDKs stöds inte längre efter den 31 augusti 2021. Du bör migrera till Adobe Experience Platform (AEP) SDK:er för iOS och Android. Mer information finns i [Version 4 Mobile SDKs end-of-support FAQ](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. Analys för ljud- och videoimplementering kräver AEP SDK och användning av tilläggen Analytics and Media Analytics. Från och med den 1 september 2021 bör du använda de nya AEP SDK:erna och tilläggen.  Media Analytics-tillägg har konfigurerats med Adobe Launch.  Mer information finns i [Migrera från fristående Media SDK till Adobe Launch](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. Funktionsutvecklingen har avslutats för Media Analytics SDK:er för iOS och Android.  Nya funktioner som introducerades från och med 2019 aktiveras med hjälp av Media Analytics-tilläggen och Media Collection API.

1. Roku- och Chromecast-SDK:er är fortfarande tillgängliga för analytiker för ljud- och videokunder. SDK:erna Roku och Chromecast kommer att fortsätta att förbättras och stödjas som fristående SDK:er.  Om du använder JS SDK for Media Analytics kan du fortsätta att använda den fristående SDK eller aktivera Media Analytics-tillägget med Adobe Launch.

1. Före den 1 september 2021 får Adobe efter eget gottfinnande utveckla nya lösningar för problem med hög teknisk inverkan eller affärsexponering. Baserat på kundens indata avgör Adobe graden av påverkan och exponering och de aktiviteter som blir följden.

Om du har några frågor kontaktar du din Adobe Customer Success Manager.

## Vanliga frågor och svar

1. **Kommer stödet för Roku- och Chromecast-SDK-produkter att påverkas? &#x200B;**

   Nej.  Roku- och Chromecast-SDKs stöds som fristående SDKs för tillfället. &#x200B; &#x200B;
1. **Kommer den här ändringen att påverka JS SDK-implementeringen av Media Analytics? &#x200B;**

   Nej.  Kunder som använder JS SDK för Media Analytics kan fortsätta att använda SDK eller aktivera det via Adobe Launch. &#x200B;
1. **Hur stor ansträngning gör man för att migrera till Media Analytics-förlängningarna? &#x200B;**

   LOE beror på varje kunds implementering, så den kommer att variera.  När du har granskat migreringsdokumentationen nedan kan du kontakta konsultation och/eller kundservice för ytterligare support.

   [Media Analytics-tillägg: Android-migrering](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics-tillägg: iOS-migrering](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics-tillägg: nya implementeringar](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Behöver jag lansera som ett tagghanteringssystem? Tänk om jag inte vill använda Launch?**

   För mobilappens användningsfall används Launch inte som ett tagghanteringssystem som det är för webben.  Du måste använda startgränssnittet för att konfigurera SDK-tilläggen. Detta liknar hur du använder gränssnittet för Adobe Mobile Services för att konfigurera det mobila v4 SDK. Fördelen med att använda Starta vid installationen är att du får anpassade installationsinstruktioner baserade på det tillägg du väljer.

1. **Påverkar detta supportslut SDK för TVOS?**

   Ja, för TVOS (version 10+) rekommenderas migrering till Media Analytics Extensions.  Mer information finns i [Migrera från fristående Media SDK till Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Påverkar detta slut på stödet SDK för FireTV och AndroidTV? &#x200B;**

   Ja, för FireTV och AndroidTV är den rekommenderade implementeringen att migrera till Media Analytics Extensions.  Mer information finns i [Migrera från fristående Media SDK till Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).

---
title: Så här konfigurerar du Media SDK på iOS
description: Följ de här stegen för att konfigurera Media SDK-programmet på iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
exl-id: fe7662b5-1700-4bd6-b542-66aa8493459d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 3%

---

# Konfigurera iOS{#set-up-ios}

Lär dig hur du konfigurerar direktuppspelningstjänster för iOS-enheter.

>[!IMPORTANT]
>
>När stödet för version 4 Mobile SDK upphör den 31 augusti 2021 upphör även stödet för Media Analytics SDK för iOS och Android.  Mer information finns i [Vanliga frågor och svar om SDK End-of-Support i Media Analytics](/help/additional-resources/end-of-support-faqs.md).

## Förutsättningar

* **Hämta giltiga konfigurationsparametrar för Media SDK**
Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.
* **Implementera ADBMobil för iOS i ditt program**
Mer information om dokumentationen för Adobe Mobile SDK finns i [iOS SDK 4.x for Experience Cloud Solutions.](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html?lang=sv-SE)

  >[!IMPORTANT]
  >
  >Från och med iOS 9 introducerade Apple en funktion som kallas ATS (App Transport Security). Den här funktionen syftar till att förbättra nätverkssäkerheten genom att säkerställa att dina appar endast använder protokoll och ciphers som följer branschstandard. Den här funktionen är aktiverad som standard, men du har konfigurationsalternativ som ger dig möjlighet att arbeta med ATS. Mer information om ATS finns i [App Transport Security.](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/app-transport-security.html?lang=sv-SE)

* **Tillhandahåll följande funktioner i din mediespelare:**

   * _Ett API för att prenumerera på spelarhändelser_ - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * _Ett API som tillhandahåller spelarinformation_ - Den här informationen innehåller information som medienamnet och spelhuvudets position.

## SDK-implementering

>[!IMPORTANT]
>
>Från och med version 2.3.0 distribueras SDK via XCFrameworks.
>
>Version 2.3.0 av SDK kräver Xcode 12.0 eller senare och, om tillämpligt, Cocoapods 1.10.0 eller senare.

* När en binär biblioteksfil nämns bör XCFramwork-ersättaren användas i stället:
   * MediaSDK.a > MediaSDK.xcframework
   * MediaSDK_TV.a > MediaSDKTV.xcframework
* Om du lägger till Adobe XCFrameworks manuellt i ditt projekt måste du se till att de inte är inbäddade.

1. Lägg till din [hämtade](/help/getting-started/download-sdks.md) Media SDK i ditt projekt.

   1. Kontrollera att följande programvarukomponenter finns i katalogen `libs`:

      * `ADBMediaHeartbeat.h`: Mål-C-huvudfilen som används för iOS API:er för pulsslagsspårning.
      * `ADBMediaHeartbeatConfig.h`: Objekt-C-huvudfilen för SDK-konfigurationen.
      * `MediaSDK.a`: En bitkodsaktiverad binär fetthalt som innehåller biblioteksbyggen för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386 och x86_64).

        Den här binärfilen bör länkas när målet är avsett för en iOS-app.

      * `MediaSDK_TV.a`: En streckkodsaktiverad binärfil som innehåller biblioteket för nya Apple TV-enheter (arm64) och simulator (x86_64).

        Den här binärfilen bör länkas när målet är avsett för en Apple TV-app (tvOS).

   1. Lägg till biblioteket i ditt projekt:

      1. Starta Xcode IDE och öppna appen.
      1. I **[!UICONTROL Project Navigator]** drar du katalogen `libs` och släpper den under projektet.

      1. Kontrollera att kryssrutan **[!UICONTROL Copy Items if Needed]** är markerad, att **[!UICONTROL Create Groups]** är markerad och att ingen av kryssrutorna i **[!UICONTROL Add to Target]** är markerad.

      ![Välj alternativ](assets/choose-options_ios.png)

      1. Klicka på **[!UICONTROL Finish]**.
      1. I **[!UICONTROL Project Navigator]** väljer du din app och dina mål.
      1. Länka de nödvändiga strukturerna och biblioteken i avsnittet **[!UICONTROL Linked Frameworks]** och **[!UICONTROL Libraries]** på fliken **[!UICONTROL General]**.

         **iOS-appmål:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**

         **Apple TV-mål (tvOS):**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**

      1. Verifiera att appen byggs utan fel.

1. Importera biblioteket.

   ```
   #import "ADBMediaHeartbeat.h"
   #import "ADBMediaHeartbeatConfig.h"
   ```

1. Skapa en `ADBMediaHeartbeatConfig`-instans.

   I det här avsnittet får du hjälp med att förstå konfigurationsparametrarna `MediaHeartbeat` och att ange korrekta konfigurationsvärden för instansen `MediaHeartbeat` för korrekt spårning.

   Här följer ett exempel på `ADBMediaHeartbeatConfig`-initiering:

   ```
   // Media Heartbeat Initialization
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>;
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>;
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>;
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>;
   config.playerName     = <SAMPLE_PLAYER_NAME>;
   config.ssl            = <YES/NO>;
   config.debugLogging   = <YES/NO>;
   ```

1. Implementera protokollet `ADBMediaHeartbeatDelegate`.

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate>
   
   @end
   
   @implementation VideoAnalyticsProvider
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values.
   - (ADBMediaObject *)getQoSObject {
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>];
   }
   
   // Return the current video player playhead position.
   // Replace <currentPlaybackTime> with the video player current playback time
   - (NSTimeInterval)getCurrentPlaybackTime {
       return <currentPlaybackTime>;
   }
   
   @end
   ```

1. Använd `ADBMediaHeartBeatConfig` och `ADBMediaHeartBeatDelegate` för att skapa `ADBMediaHeartbeat`-instansen.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Kontrollera att din `ADBMediaHeartbeat`-instans är tillgänglig och att *inte frigörs förrän i slutet av sessionen*. Den här instansen kommer att användas för alla följande spårningshändelser.

## Migrera från version 1.x till 2.x i iOS {#migrate-to-two-x}

I version 2.x konsolideras alla publika metoder i klassen `ADBMediaHeartbeat` så att det blir enklare för utvecklare. Alla konfigurationer har konsoliderats till klassen `ADBMediaHeartbeatConfig`.

Mer information om hur du migrerar från 1.x till 2.x finns i dokumentationen för den äldre implementeringen.)

## Konfigurera en intern app för tvOS

I och med den nya Apple TV-funktionen kan du nu skapa program som kan köras i den inbyggda tvOS-miljön. Du kan antingen skapa ett helt inbyggt program med hjälp av ett eller flera ramverk i iOS, eller så kan du skapa programmet med hjälp av XML-mallar och JavaScript. Från och med MediaSDK version 2.0 finns stöd för tvOS. Mer information om tvOS finns på webbplatsen [tvOS Developer.](https://developer.apple.com/tvos/)

Utför följande steg i Xcode-projektet. Den här guiden är skriven under förutsättning att ditt projekt har ett mål som är en Apple TV-app som riktar sig till tvOS:

1. Dra biblioteksfilen `VideoHeartbeat_TV.a` till projektets `lib`-mapp.

1. Utöka avsnittet **[!UICONTROL Build Phases]** på fliken **[!UICONTROL Link Binary with Libraries]** i målet för din tvOS-app och lägg till följande bibliotek:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

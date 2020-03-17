---
title: Konfigurera iOS
description: Installation av Media SDK-program för implementering på iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Konfigurera iOS{#set-up-ios}

## Förutsättningar

* **Hämta giltiga konfigurationsparametrar för Media SDK** Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.
* **Implementera ADBMomobile för iOS i ditt program** Mer information om dokumentationen för Adobe Mobile SDK finns i [iOS SDK 4.x för Experience Cloud Solutions.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >Från och med iOS 9 introducerade Apple en funktion som kallas ATS (App Transport Security). Den här funktionen syftar till att förbättra nätverkssäkerheten genom att säkerställa att dina appar endast använder protokoll och ciphers som följer branschstandard. Den här funktionen är aktiverad som standard, men du har konfigurationsalternativ som ger dig möjlighet att arbeta med ATS. Mer information om ATS finns i [App Transport Security.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **Tillhandahåll följande funktioner i din mediespelare:**

   * _Ett API för att prenumerera på spelarhändelser_ - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * _Ett API som tillhandahåller spelarinformation_ - Den här informationen innehåller information som medienamnet och spelhuvudets position.

## SDK-implementering

1. Lägg till din [hämtade](/help/sdk-implement/download-sdks.md#download-2x-sdks) Media SDK i projektet.

   1. Kontrollera att följande programvarukomponenter finns i `libs` katalogen:

      * `ADBMediaHeartbeat.h`: Objektiv-C-huvudfilen som används för API:er för iOS-pulsspårning.
      * `ADBMediaHeartbeatConfig.h`: Mål-C-huvudfilen för SDK-konfigurationen.
      * `MediaSDK.a`: En streckkodsaktiverad binär fetthalt som innehåller biblioteksbyggen för iOS-enheter (armv7, armv7s, arm64) och simulatorer (i386 och x86_64).

         Den här binärfilen bör länkas när målet är avsett för en iOS-app.

      * `MediaSDK_TV.a`: En streckkodsaktiverad binärfil som innehåller biblioteket för nya Apple TV-enheter (arm64) och simulator (x86_64).

         Den här binärfilen bör länkas när målet är avsett för en Apple TV-app (tvOS).
   1. Lägg till biblioteket i ditt projekt:

      1. Starta Xcode IDE och öppna appen.
      1. I **[!UICONTROL Project Navigator]** drar du `libs` katalogen och släpper den under projektet.

      1. Kontrollera att **[!UICONTROL Copy Items if Needed]** kryssrutan är markerad, **[!UICONTROL Create Groups]** markerad och att ingen av kryssrutorna i **[!UICONTROL Add to Target]** är markerad.

         ![](assets/choose-options_ios.png)

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

1. Skapa en `ADBMediaHeartbeatConfig` instans.

   I det här avsnittet får du hjälp med att förstå `MediaHeartbeat` konfigurationsparametrarna och att ställa in korrekta konfigurationsvärden för din `MediaHeartbeat` instans för korrekt spårning.

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

1. Implementera `ADBMediaHeartbeatDelegate` protokollet.

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

1. Använd `ADBMediaHeartBeatConfig` och `ADBMediaHeartBeatDelegate` för att skapa `ADBMediaHeartbeat` instansen.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Se till att din `ADBMediaHeartbeat` instans är tillgänglig och *inte tas bort förrän i slutet av sessionen*. Den här instansen används för alla följande spårningshändelser.

## Migrera från version 1.x till 2.x i iOS {#migrate-to-two-x}

I version 2.x konsolideras alla publika metoder i `ADBMediaHeartbeat` klassen så att det blir enklare för utvecklare. Alla konfigurationer har konsoliderats i `ADBMediaHeartbeatConfig` klassen.

Mer information om hur du migrerar från 1.x till 2.x finns i [VHL 1.x till 2.x-migrering.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Konfigurera en intern app för tvOS

Med den nya Apple TV-versionen kan du nu skapa program som kan köras i den inbyggda tvOS-miljön. Du kan antingen skapa ett helt inbyggt program med hjälp av något av flera ramverk som är tillgängliga i iOS, eller så kan du skapa programmet med hjälp av XML-mallar och JavaScript. Från och med MediaSDK version 2.0 finns stöd för tvOS. Mer information om tvOS finns på [webbplatsen för tvOS-utvecklare.](https://developer.apple.com/tvos/)

Utför följande steg i Xcode-projektet. Den här guiden är skriven under förutsättning att ditt projekt har ett mål som är en Apple TV-app som har tvOS som mål:

1. Dra biblioteksfilen till `VideoHeartbeat_TV.a` projektets `lib` mapp.

1. Expandera avsnittet **[!UICONTROL Link Binary with Libraries]** på fliken **[!UICONTROL Build Phases]** i målet för din tvOS-app och lägg till följande bibliotek:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

---
title: Implementera SDK:er som förklaras
description: '"Lär dig hur du konfigurerar Media SDK för mediespårning i dina mobil-, OTT- och webbläsarprogram (JS)."'
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 165c7f01a2d2c32df518c89a5c49637107d41086
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 3%

---

# Översikt{#setup-overview}

Följande instruktioner gäller för 2.x Media SDK:er. Om du implementerar en 1.x-version av Media SDK kan du läsa [1.x Media SDK Documentation.](/help/sdk-implement/download-sdks.md) Information om Primetime-integratörer finns på _Primetime Media SDK-dokumentation_ nedan.

>[!IMPORTANT]
>
>När stödet för version 4 Mobile SDK upphör den 31 augusti 2021 upphör även stödet för Media Analytics SDK för iOS och Android i Adobe.  Mer information finns i [Vanliga frågor om supporten för Media Analytics SDK](/help/sdk-implement/end-of-support-faqs.md).


## Stöd för minst plattformsversion {#minimum-platform-version}

I följande tabell beskrivs de lägsta plattformsversioner som stöds för varje SDK från och med den 19 februari 2019.

| OS/webbläsare | Min version krävs |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Krom | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Allmänna riktlinjer för genomförandet {#general-implementation-guidelines}

Det finns tre SDK-huvudkomponenter för mediespårning:
* Konfiguration för pulsslag i media - Konfigurationen innehåller de grundläggande inställningarna för rapportering.
* Media Heartbeat Delegate - Delegaten styr uppspelningstiden och QoS-objektet.
* Mediepulsslag - Det primära biblioteket som innehåller medlemmar och metoder.

Utför följande implementeringssteg:

1. Skapa en `MediaHeartbeatConfig` och ange värden för config-parametern.

   |  Variabelnamn  | Beskrivning  | Obligatoriskt |  Standardvärde  |
   |---|---|:---:|---|
   | `trackingServer` | Spårningsserver för medieanalys. Detta skiljer sig från analysspårningsservern. | Ja | Tom sträng |
   | `channel` | Kanalnamn | Nej | Tom sträng |
   | `ovp` | Namnet på onlinemedieplattformen som innehållet distribueras via | Nej | Tom sträng |
   | `appVersion` | Version av mediespelarappen/SDK | Nej | Tom sträng |
   | `playerName` | Namnet på den mediespelare som används, dvs.&quot;AVPlayer&quot;,&quot;HTML5 Player&quot;,&quot;My Custom Player&quot; | Nej | Tom sträng |
   | `ssl` | Anger om anrop ska göras via HTTPS | Nej | falskt |
   | `debugLogging` | Anger om felsökningsloggning är aktiverat | Nej | falskt |

1. Implementera `MediaHeartbeatDelegate`.

   |  Metodnamn  |  Beskrivning  | Obligatoriskt |
   | --- | --- | :---: |
   | `getQoSObject()` | Returnerar `MediaObject` -instans som innehåller aktuell QoS-information. Den här metoden anropas flera gånger under en uppspelningssession. Spelarimplementeringen måste alltid returnera de senast tillgängliga QoS-data. | Ja |
   | `getCurrentPlaybackTime()` | Returnerar spelhuvudets aktuella position. <br /> För VOD-spårning anges värdet i sekunder från mediaobjektets början. <br /> Om spelaren inte anger information om innehållets varaktighet för direktuppspelning kan värdet anges som antalet sekunder sedan midnatt UTC den dagen. <br /> Obs! När du använder förloppsmarkörer krävs innehållets längd och spelhuvudet måste uppdateras som antal sekunder från början av medieobjektet, med början från 0. | Ja |

   >[!TIP]
   >
   >QoS-objektet (Quality of Service) är valfritt. Om QoS-data är tillgängliga för spelaren och du vill spåra dessa data, krävs följande variabler:

   | Variabelnamn | Beskrivning   | Obligatoriskt |
   | --- | --- | :---: |
   | `bitrate` | Mediets bithastighet i bitar per sekund. | Ja |
   | `startupTime` | Starttiden för media i millisekunder. | Ja |
   | `fps` | Bildrutorna som visas per sekund. | Ja |
   | `droppedFrames` | Antalet uteslutna bildrutor hittills. | Ja |

1. Skapa `MediaHeartbeat` -instans.

   Använd `MediaHertbeatConfig` och `MediaHertbeatDelegate` för att skapa `MediaHeartbeat` -instans.

   >[!IMPORTANT]
   >
   >Se till att `MediaHeartbeat` -instansen är tillgänglig och tas inte bort förrän i slutet av sessionen. Den här instansen kommer att användas för alla följande mediespårningshändelser.

   >[!TIP]
   >
   >`MediaHeartbeat` kräver en instans av `AppMeasurement` för att ringa Adobe Analytics.

1. Kombinera alla bitar.

   I följande exempelkod används JavaScript 2.x SDK för en HTML5-videospelare:

   ```javascript
   // Create local references to the heartbeat classes
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   
   //Media Heartbeat Config
   var mediaConfig = new MediaHeartbeatConfig();
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net";
   mediaConfig.playerName = "HTML5 Basic";
   mediaConfig.channel = "Video Channel";
   mediaConfig.debugLogging = true;
   mediaConfig.appVersion = "2.0";
   mediaConfig.ssl = false;
   mediaConfig.ovp = "";
   
   // Media Heartbeat Delegate
   var mediaDelegate = new MediaHeartbeatDelegate();
   
   // Set mediaDelegate CurrentPlaybackTime
   mediaDelegate.getCurrentPlaybackTime = function() {
       return video.currentTime;
   };
   
   // Set mediaDelegate QoSObject - OPTIONAL
   mediaDelegate.getQoSObject = function() {
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes);
   }
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## Validera {#validate}

Spåra implementeringar med Media Analytics genererar två typer av spårningsanrop:

* Media- och startanrop skickas direkt till Adobe Analytics-servern (AppMeasurement).
* Anrop till pulsslag skickas till Media Analytics-spårningsservern (hjärtslag) som bearbetas där och skickas vidare till Adobe Analytics-servern.

* **Adobe Analytics-server (AppMeasurement)**
Mer information om alternativ för spårning av server finns i [Fyll i variablerna trackingServer och trackingServerSecure korrekt.](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Det krävs en RDC-spårningsserver eller CNAME som kan matchas till en RDC-server för Experience Cloud Visitor ID-tjänsten.

   Analysspårningsservern ska sluta med &quot;`.sc.omtrdc.net`eller vara CNAME.

* ** Media Analytics-server (Heartbeats)** Den har alltid formatet &quot;`[your_namespace].hb.omtrdc.net`&quot;. Värdet för`[your_namespace]`&quot; anger ditt företag och tillhandahålls av Adobe.

Mediespårning fungerar likadant på alla plattformar, både datorer och mobila enheter. Ljudspårning fungerar för närvarande på mobilplattformar. För alla spårningsanrop finns det några viktiga universella variabler som ska valideras:

## SDK 1.x-dokumentation {#sdk-1x-documentation}

| Video Analytics 1.x SDKs  |  Utvecklarhandböcker (endast PDF) |
| --- | --- |
| Android | [Konfigurera för Android ](vhl-dev-guide-v15_android.pdf) |
| AppleTV | [Konfigurera för AppleTV ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Konfigurera för Chromecast ](chromecast_1.x_sdk.pdf) |
| iOS | [Konfigurera för iOS ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Konfigurera för JavaScript ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Konfigurera medieanalys](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Konfigurera medieanalys](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Konfigurera medieanalys](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Konfigurera för TVML ](vhl_tvml.pdf) |

## Primetime Media SDK-dokumentation {#primetime-docs}

* [Användarhandböcker för Primetime](https://helpx.adobe.com/se/primetime/user-guide.html)

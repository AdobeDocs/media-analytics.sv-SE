---
title: Implementera SDK:er som förklaras
description: Lär dig hur du konfigurerar Media SDK för mediespårning i dina mobil-, OTT- och webbläsarprogram (JS).
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# Äldre - Media SDK Setup Overview {#setup-overview}

När du har laddat ned Media SDK för din videoapp eller spelare följer du informationen i det här avsnittet för att konfigurera och implementera Media SDK.


## Allmänna riktlinjer för genomförandet {#general-implementation-guidelines}

Det finns tre huvudkomponenter i SDK som används för att spåra direktuppspelande medietjänster:
* Konfiguration för pulsslag i media - `MediaHeartbeatConfig` innehåller de grundläggande inställningarna för rapportering.
* Media Heartbeat Delegate - `MediaHeartbeatDelegate` styr uppspelningstiden och QoS-objektet.
* Mediepulsslag - `MediaHeartbeat` är det primära biblioteket som innehåller medlemmar och metoder.

## Implementera Streaming Media SDK

Om du vill installera och använda Streaming Media SDK utför du följande implementeringssteg:

1. Skapa en `MediaHeartbeatConfig`-instans och ange parametervärden för konfigurationen.

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
   | `getQoSObject()` | Returnerar instansen `MediaObject` som innehåller aktuell QoS-information. Den här metoden anropas flera gånger under en uppspelningssession. Spelarimplementeringen måste alltid returnera de senast tillgängliga QoS-data. | Ja |
   | `getCurrentPlaybackTime()` | Returnerar spelhuvudets aktuella position. <br /> För VOD-spårning anges värdet i sekunder från början av medieobjektet. <br /> Om spelaren inte anger information om innehållets varaktighet för direktuppspelning kan värdet anges som antalet sekunder sedan midnatt UTC den dagen. <br /> Obs! När du använder förloppsmarkörer krävs innehållets varaktighet och spelhuvudet måste uppdateras som antal sekunder från början av medieobjektet, med början från 0. | Ja |

   >[!TIP]
   >
   >QoS-objektet (Quality of Service) är valfritt. Om QoS-data är tillgängliga för spelaren och du vill spåra dessa data, krävs följande variabler:

   | Variabelnamn | Beskrivning   | Obligatoriskt |
   | --- | --- | :---: |
   | `bitrate` | Mediets bithastighet i bitar per sekund. | Ja |
   | `startupTime` | Starttiden för media i millisekunder. | Ja |
   | `fps` | Bildrutorna som visas per sekund. | Ja |
   | `droppedFrames` | Antalet uteslutna bildrutor hittills. | Ja |

1. Skapa instansen `MediaHeartbeat`.

   Använd `MediaHertbeatConfig` och `MediaHertbeatDelegate` för att skapa `MediaHeartbeat`-instansen.

   >[!IMPORTANT]
   >
   >Se till att din `MediaHeartbeat`-instans är tillgänglig och inte tas bort förrän i slutet av sessionen. Den här instansen kommer att användas för alla följande mediespårningshändelser.

   >[!TIP]
   >
   >`MediaHeartbeat` kräver en instans av `AppMeasurement` för att kunna skicka anrop till Adobe Analytics.

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

* Media- och startsamtal skickas direkt till Adobe Analytics-servern (AppMeasurement).
* Anrop till pulsslag skickas till Media Analytics-spårningsservern (hjärtslag) som bearbetas där och skickas vidare till Adobe Analytics-servern.

* **Adobe Analytics-server (AppMeasurement)**
Mer information om alternativ för spårning av serveralternativ finns i [Fylla i variablerna trackingServer och trackingServerSecure korrekt.](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

  >[!IMPORTANT]
  >
  >En RDC-spårningsserver eller CNAME som löser problem med en RDC-server krävs för tjänsten Experience Cloud Visitor ID.

  Analysspårningsservern ska avslutas med `.sc.omtrdc.net` eller vara en CNAME.

* ** Media Analytics-server (Heartbeats)**
Det här har alltid formatet `[your_namespace].hb.omtrdc.net`. Värdet `[your_namespace]` anger ditt företag och tillhandahålls av Adobe.

Mediespårning fungerar likadant på alla plattformar, både datorer och mobila enheter. Ljudspårning fungerar för närvarande på mobilplattformar. För alla spårningsanrop finns det några viktiga universella variabler som ska valideras:

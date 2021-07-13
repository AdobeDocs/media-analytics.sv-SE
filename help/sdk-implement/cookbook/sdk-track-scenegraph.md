---
title: Spårning i SceneGraph (Roku)
description: Lär dig spåra media med Roku SceneGraph XML-programmeringsramverket.
uuid: fa85e546-c79b-4df4-8c03-d6593fa296d5
exl-id: e428d3cd-dbc7-48bb-82ff-61b6b892884c
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 1%

---

# Spårning i SceneGraph (Roku){#tracking-in-scenegraph-roku}

## Introduktion {#introduction}

Roku har infört ett nytt ramverk för programmering av applikationer: SceneGraph XML-programmeringsramverket. Det nya ramverket innehåller två nya viktiga begrepp:

* SceneGraph-återgivning av programskärmar
* XML-konfiguration för SceneGraph-skärmar

Adobe Mobile SDK for Roku är skriven i BrightScript. SDK använder många komponenter som inte är tillgängliga för ett program som körs på SceneGraph (till exempel trådar). Därför kan en Roku-apputvecklare som tänker använda SceneGraph-ramverket inte anropa Adobe Mobile SDK-API:er (de senare liknar de som finns i äldre BrightScript-program).

## Arkitektur {#architecture}

För att lägga till stöd för SceneGraph i AdobeMobile SDK har Adobe lagt till ett nytt API som skapar en anslutningsbrygga mellan AdobeMobile SDK och `adbmobileTask`. Det senare är en SceneGraph-nod som används för SDK:s API-körning. (Användning av `adbmobileTask` förklaras i detalj i resten av det här dokumentet.)

Kopplingsbryggan är utformad för att fungera så här:

* Bryggan returnerar en SceneGraph-kompatibel instans av AdobeMobile SDK. SceneGraph-kompatibel SDK har alla API:er som den äldre SDK:n visar.
* Du använder API:erna för AdobeMobile SDK i SceneGraph på ungefär samma sätt som du använde tidigare API:er.
* Bryggan visar också en mekanism för att lyssna efter återanrop för API:er som returnerar vissa data.

![](assets/SceneGraph_arch.png)

## Komponenter {#components}

**SceneGraph-program:**

* Använder `AdobeMobileLibrary` API:er via API:erna för anslutningsbryggan i SceneGraph.
* Registrerar för svarsåteranrop på `adbmobileTask` för förväntade utdatavariabler.

**AdobeMobileLibrary:**

* Visar en uppsättning offentliga API:er (äldre), inklusive API:t för anslutningsbryggan.
* Returnerar en instans av en SceneGraph-koppling som omsluter alla tidigare offentliga API:er.
* Kommunicerar med en `adbmobileTask` SceneGraph-nod för körning av API:er.

**adbmobileTask Node:**

* En SceneGraph-aktivitetsnod som kör `AdobeMobileLibrary` API:er på en bakgrundstråd.
* Fungerar som ett ombud som returnerar data till programscener.

## Public SceneGraph APIs {#public-scenegraph-apis}

### ADBMobleConnector

| Kategori | Metodnamn | Beskrivning |
|---|---|---|
| **Konstanter** |  |  |
|  | `sceneGraphConstants` | Returnerar ett objekt som innehåller `SceneGraphConstants`. Se tabellen ovan för mer information. |
|  |  |  |
| **Felsökningsloggning** |  |  |
|  | `setDebugLogging` | SceneGraph API för att ställa in felsökningsloggning på ADBMomobile SDK. |
|  | `getDebugLogging` | SceneGraph API för att hämta felsökningsloggning från ADBMomobile SDK. |
|  | Mer information finns i avsnittet Felsökningsloggning i äldre SDK. |  |
|  |  |  |
| **Sekretessstatus/avanmäl dig** |  |  |
|  | `setPrivacyStatus` | SceneGraph API för att ange sekretessstatus för ADBMomobile SDK. |
|  | `getPrivacyStatus` | SceneGraph API för att få sekretessstatus från ADBMomobile SDK. |
|  | Mer information finns i avsnittet Avanmäl dig/Sekretessstatus i äldre SDK. |  |
|  |  |  |
| **Analytics**  |  |  |
|  | `trackState` | SceneGraph API för att spåra status på ADBMomobile SDK. |
|  | `trackAction` | SceneGraph API för att spåra åtgärder i ADBMomobile SDK. |
|  | `trackingIdentifier` | SceneGraph API för att hämta en spårningsidentifierare från ADBMomobile SDK. |
|  | `userIdentifier` | SceneGraph API för att hämta en användaridentifierare från ADBMomobile SDK. |
|  | `setUserIdentifier` | SceneGraph API för att ange användaridentifieraren i ADBMomobile SDK. |
|  | `getAllIdentifiers` | SceneGraph API hämtar alla användaridentiteter som är kända och beständiga av Roku SDK. |
|  | Mer information finns i avsnittet Analytics (Analyser) i det äldre SDK:t. |  |
|  |  |  |
| **Experience Cloud** |  |  |
|  | `visitorSyncIdentifiers` | SceneGraph API för att synkronisera Experience Cloud-identifierare på ADBMoble SDK. |
|  | `visitorMarketingCloudID` | SceneGraph API för att hämta Visitor Experience Cloud ID från ADBMomobile SDK. |
|  | Mer information finns i avsnittet Experience Cloud i den äldre SDK:n. |  |
|  |  |  |
| **Audience Manager** |  |  |
|  | `audienceSubmitSignal` | SceneGraph API för att skicka en målgruppshanteringssignal med trait. |
|  | `audienceVisitorProfile` | SceneGraph API för att hämta en besökarprofil för målgruppshanteraren från ADBMomobile SDK. |
|  | `audienceDpid` | SceneGraph API för att hämta en målgrupp Dpid från ADBMomobile SDK. |
|  | `audienceDpuuid` | SceneGraph API för att hämta en publik från ADBMomobile SDK. |
|  | `audienceSetDpidAndDpuuid` | SceneGraph API för att ange målgrupp Dpid och Dpuuid på ADBMomobile SDK. |
|  | Mer information finns i avsnittet Audience Manager i den äldre SDK:n. |  |
|  |  |  |
| **MediaHeartbeat** |  |  |
|  | `mediaTrackLoad` | SceneGraph API för att läsa in videoinnehåll för MediaHeartbeat-spårning. |
|  | mediaTrackStart | SceneGraph API för att starta videospårningssession med MediaHeartbeat. |
|  | `mediaTrackUnload` | SceneGraph API för att ta bort videoinnehåll från MediaHeartbeat-spårning. |
|  | `mediaTrackPlay` | SceneGraph API för att spåra uppspelning av videoinnehåll. |
|  | mediaTrackPause | SceneGraph API för att spåra pausat videoinnehåll. |
|  | `mediaTrackComplete` | SceneGraph API för att spåra uppspelning slutförd för videoinnehåll. |
|  | `mediaTrackError` | SceneGraph API för att spåra uppspelningsfel. |
|  | mediaTrackEvent | SceneGraph API för att spåra uppspelningshändelser under spårning. Till exempel: Ads, Chapters. |
|  | `mediaUpdatePlayhead` | SceneGraph API för att skicka uppdateringar av spelhuvudet till MediaHeartbeat under videospårning. |
|  | `mediaUpdateQoS` | SceneGraph API för att skicka QoS-uppdateringar till MediaHeartbeat under videospårning. |
|  | Mer information finns i avsnittet MediaHeartbeat i det äldre SDK:t. |  |

### SceneGraphConstants

| Konstantnamn | Beskrivning |
|---|---|
| `API_RESPONSE` | Används för att hämta svarsobjektet från `adbmobileTask`-nodens `adbmobileApiResponse`-fält |
| `DEBUG_LOGGING` | Används som `apiName` för `getDebugLogging` |
| `PRIVACY_STATUS` | Används som `apiName` för `getPrivacyStatus` |
| `TRACKING_IDENTIFIER` | Används som `apiName` för `trackingIdentifier` |
| `USER_IDENTIFIER` | Används som `apiName` för `userIdentifier` |
| `VISITOR_MARKETING_CLOUD_ID` | Används som `apiName` för `visitorMarketingCloudID` |
| `AUDIENCE_VISITOR_PROFILE` | Används som `apiName` för `audienceVisitorProfile` |
| `AUDIENCE_DPID` | Används som `apiName` för `audienceDpid` |
| `AUDIENCE_DPUUID` | Används som `apiName` för `audienceDpuuid` |

### adbmobileTask Node

<table>
<thead>
<tr>
<td> Fält </td><td> Typ </td><td> Standard </td><td> Användning </td>
</tr>
</thead>
<tbody>
<tr>
<td> adbmobileApiCall </td>
<td> assocarray </td>
<td> Ogiltig </td>
<td> Ändra INTE det här fältet och låt inte användas av programmet. Det här fältet används av ADBMomobile SceneGraphConnector för att dirigera API-anrop via SceneGraph-noder och för att hämta svar. Nyckeln/fältet är därför reserverat för AdobeMobileSDK för SceneGraph-kompatibilitet. <b>Viktigt:</b> Alla ändringar i det här fältet kan leda till att AdobeMobileSDK inte fungerar som det ska.</td>
</tr>
<tr>
<td> adbmobileApiResponse </td>
<td> assocarray </td>
<td> Ogiltig </td>
<td> Skrivskydda Alla API:er som körs på AdobeMobileSDK returnerar svar i det här fältet. Registrera dig för ett återanrop för att lyssna efter uppdateringar av det här fältet för att kunna ta emot svarsobjekt. Här följer formatet för svarsobjektet:  
<pre>
response = {
  "apiName" : &lt;SceneGraphConstants.
               API_NAME&gt; 
  "returnValue : &lt;API_RESPONSE&gt; 
}</pre>
En instans av det här svarsobjektet skickas för alla API-anrop på AdobeMobileSDK som förväntas returnera ett värde enligt API-referenshandboken. Ett API-anrop till exempel för visitorMarketingCloudID() returnerar följande svarsobjekt: 
<pre>
response = {
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : "07050x25671x33760x72644x14"  
} 
</pre>
Eller så kan svarsdata vara ogiltiga: 
<pre>
response = {  
  "apiName" : m.
              adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID  
  "returnValue : ogiltig 
} 
</pre>
</td>
</tr>
</tbody>
</table>

### `adbmobile.brs`

#### `getADBMobileConnectorInstance`

API-signatur: `ADBMobile().getADBMobileConnectorInstance()`\
Indata: `adbmobileTask`
Returtyp: `ADBMobileConnector`

#### `sgConstants`

API-signatur: `ADBMobile().sgConstants()`
Indata: Ingen\
Returtyp: `SceneGraphConstants`

>[!NOTE]
>Mer information finns i API-referensen för `ADBMobileConnector`.

### ADBMomobile-konstanter

|  Funktion  | Konstantnamn | Beskrivning   |
|---|---|---|
| Versionshantering | `version` | Konstant för att hämta AdobeMobileLibrary-versionsinformation |
| Sekretess/avanmälan | `PRIVACY_STATUS_OPT_IN` | Konstant för sekretessstatus har valts i |
|  | `PRIVACY_STATUS_OPT_OUT` | Konstant för sekretesstatus har avvalts |
| MediaHeartbeat-konstanter | Se konstanterna på den här sidan: <br/><br/>[Metoder för pulsslag i media.](/help/sdk-implement/track-av-playback/track-core/track-core-roku.md) | Använd dessa konstanter med MediaHeartbeat-API:er |
| Standardmetadata | Se konstanterna på den här sidan: <br/><br/>[Standardmetadataparametrar.](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md) | Använd dessa konstanter för att bifoga standardmetadata för video/annonsering i MediaHeartbeat-API:er |

Globalt definierade `MediaHeartbeat`-API:er för det äldre AdobeMobileLibrary är tillgängliga *som* i SceneGraph-miljön eftersom de inte använder några Brightscript-komponenter som inte är tillgängliga i SceneGraph-noder. Mer information om dessa metoder finns i tabellen nedan:

### Globala metoder för MediaHeartbeat

| Metod | Beskrivning |
| --- | --- |
| `adb_media_init_mediainfo` | Den här metoden returnerar ett initierat medieinformationsobjekt `Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object` |
| `adb_media_init_adinfo` | Den här metoden returnerar det initierade Ad Information-objektet `Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object` |
| `adb_media_init_chapterinfo` | Den här metoden returnerar det initierade kapitelinformationsobjektet.  `Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object` |
| `adb_media_init_adbreakinfo` | Den här metoden returnerar initierat AdBreak Information-objekt.  `Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object` |
| `adb_media_init_qosinfo` | Den här metoden returnerar ett initierat QoS Information-objekt.  `Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object` |

## Implementering {#implementation}

1. **Ladda ned Roku Library -** Ladda ned det  [senaste Roku-biblioteket.](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.2)

1. **Konfigurera utvecklingsmiljön**

   1. Kopiera `adbmobile.brs` (AdobeMobileLibrary) till din `pkg:/source/`-katalog.

   1. Kopiera `adbmobileTask.brs` och `adbMobileTask.xml` till din `pkg:/components/`-katalog om du vill ha stöd för scengrafik.

1. **Initiera**

   1. Importera `adbmobile.brs` till scenen.

      ```
      <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
      ```

   1. Skapa en instans av noden `adbmobileTask` i scenen.

      ```
      m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
      ```

   1. Hämta en instans av `adbmobile`-kopplingen för SceneGraph med instansen `adbmobileTask`.

      ```
      m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
      ```

   1. Hämta `adbmobile` SG-konstanter.

      ```
      m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
      ```

   1. Registrera ett återanrop för att ta emot ett svarsobjekt för alla `AdbMobile` API-anrop.

      ```
      m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE,  
                                   "onAdbmobileApiResponse") 
      
      ' Sample implementation of the callback 
      ' Listen for all the constants for which API calls are made on the SDK 
      function onAdbmobileApiResponse() as void 
          responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE] 
      
          if responseObject <> invalid 
              methodName = responseObject.apiName 
              retVal = responseObject.returnValue 
      
              if methodName = m.adbmobileConstants.DEBUG_LOGGING 
                  if retVal 
                      print "API Response: DEBUG LOGGING: " + "True" 
                  else 
                      print "API Response: DEBUG LOGGING: " + "False" 
                  endif 
              else if methodName = m.adbmobileConstants.PRIVACY_STATUS 
                  print "API Response: PRIVACY STATUS: " + retVal 
              else if methodName = m.adbmobileConstants.TRACKING_IDENTIFIER 
                  if retVal <> invalid 
                      print "API Response: TRACKING IDENTIFIER: " + retVal 
                  else 
                      print "API Response: TRACKING IDENTIFIER: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.USER_IDENTIFIER 
                  if retVal <> invalid 
                      print "API Response: USER IDENTIFIER: " + retVal 
                  else 
                      print "API Response: USER IDENTIFIER: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.VISITOR_MARKETING_CLOUD_ID 
                  if retVal <> invalid 
                      print "API Response: MCID: " + retVal 
                  else 
                      print "API Response: MCID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_DPID 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE DPID: " + retVal 
                  else 
                      print "API Response: AUDIENCE DPID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_DPUUID 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE DPUUID: " + retVal 
                  else 
                      print "API Response: AUDIENCE DPUUID: " + "invalid" 
                  endif 
              else if methodName = m.adbmobileConstants.AUDIENCE_VISITOR_PROFILE 
                  if retVal <> invalid 
                      print "API Response: AUDIENCE VISITOR PROFILE: Valid Object" 
                  else 
                      print "API Response: AUDIENCE VISITOR PROFILE: " + "invalid" 
                  endif 
              endif 
          endif 
      end function 
      ```

## Exempelimplementering {#sample-implementation}

### Exempel på API-anrop till äldre SDK

```
'get an instance of SDK 
m.adbmobile = ADBMobile() 
   
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
   
'execute getter APIs 
debugLogging = m.adbmobile.getDebugLogging()
```

### Exempel-API-anrop till SG SDK

```
'create adbmobileTask instance 
m.adbmobileTask = createObject("roSGNode", "adbmobileTask") 
   
'get an instance of SDK using task instance 
m.adbmobile =  
  ADBMobile().getADBMobileConnectorInstace(m.adbmobileTask) 
m.adbmobileConstants = m.adbmobile.sceneGraphConstants() 
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
  
'execute getter APIs 
m.adbmobileTask.ObserverField(m.adbConstants.API_RESPONSE,  
                              "onAdbmobileApiResponse") 
m.adbmobile.getDebugLogging() 
   
'listen for return data in registered callbacks 
function onAdbmobileApiResponse() as void 
    responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE] 
  
        if responseObject <> invalid 
            methodName = responseObject.apiName 
            retVal = responseObject.returnValue 
  
        if methodName = m.adbmobileConstants.DEBUG_LOGGING 
            if retVal 
                print "API Response: DEBUG LOGGING: " + "True" 
            else 
                print "API Response: DEBUG LOGGING: " + "False" 
         endif 
    endif 
end function
```

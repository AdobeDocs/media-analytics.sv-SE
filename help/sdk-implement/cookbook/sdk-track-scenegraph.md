---
title: Spårning i SceneGraph (Roku)
description: Spåra media med Roku SceneGraph XML-programmeringsramverket.
uuid: fa85e546-c79b-4df4-8c03-d6593fa296d5
translation-type: tm+mt
source-git-commit: 305f97d6d1350a3bb8b0ad9c4c58e0a5fefca045
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 1%

---


# Spårning i SceneGraph (Roku){#tracking-in-scenegraph-roku}

## Inledning {#introduction}

Roku har infört en ny programram för utveckling av tillämpningar: SceneGraph XML-programmeringsramen. Denna nya ram innehåller två nya nyckelbegrepp:

* SceneGraph-återgivning av programskärmar
* XML-konfiguration för SceneGraph-skärmar

Adobe Mobile SDK for Roku är skriven i BrightStorScript. SDK använder många komponenter som inte är tillgängliga för en app som körs på SceneGraph (till exempel trådar). Därför kan en Roku-apputvecklare som avser att använda SceneGraph-ramverket inte anropa Adobe Mobile SDK API:er (de senare liknar de som finns i äldre BrightStor-appar).

## Arkitektur {#architecture}

Om du vill lägga till stöd för SceneGraph till AdobeMobile SDK har Adobe lagt till ett nytt API som skapar en anslutningsbro mellan AdobeMobile SDK och `adbmobileTask`. Den senare är en SceneGraph-nod som används för SDK:s API-körning. (Användning av `adbmobileTask` förklaras i detalj i resten av detta dokument.)

Kopplingsbron är utformad för att utföra följande:

* Bron returnerar en SceneGraph-kompatibel instans av AdobeMobile SDK. SceneGraph-kompatibel SDK har alla API:er som det äldre SDK visar.
* Du använder AdobeMobile SDK API:er i SceneGraph på ungefär samma sätt som du använde de äldre API:erna.
* Bron visar också en mekanism för att lyssna efter återanrop till API:er som returnerar vissa data.

![](assets/SceneGraph_arch.png)

## Komponenter {#components}

**SceneGraph-program:**

* Konsumenter `AdobeMobileLibrary` API:er via SceneGraph-anslutningsbryggens API:er.
* Registrerar för svarsinanrop på `adbmobileTask` för förväntade utdatavariabler.

**AdobeMobileLibrary:**

* Exponerar en uppsättning offentliga API:er (äldre), inklusive API:t för anslutningsbrygga.
* Returnerar en SceneGraph-kopplingsinstans som omsluter alla äldre offentliga API:er.
* Kommunicera med en `adbmobileTask` SceneGraph-nod för körning av API:er.

**adbmobileTask-nod:**

* En sceneGraph-aktivitetsnod som körs `AdobeMobileLibrary` API:er på en bakgrundstråd.
* Tjänstar som ombud för att returnera data till programscener.

## Public SceneGraph API:er {#public-scenegraph-apis}

### ADBMobileConnector

| Kategori | Metodnamn | Beskrivning |
|---|---|---|
| **Konstanter** |  |  |
|  | `sceneGraphConstants` | Returnerar ett objekt som innehåller `SceneGraphConstants`. Mer information finns i tabellen ovan. |
|  |  |  |
| **Felsökningsloggning** |  |  |
|  | `setDebugLogging` | SceneGraph API för att ställa in felsökningsloggning på ADBMobile SDK. |
|  | `getDebugLogging` | SceneGraph API för att hämta felsökningsloggning från ADBMobile SDK. |
|  | Mer information finns i avsnittet Felsökningsloggning i det äldre SDK. |  |
|  |  |  |
| **Sekretesspolicy/opt-out** |  |  |
|  | `setPrivacyStatus` | SceneGraph API för att ange sekretesstatus för ADBMobile SDK. |
|  | `getPrivacyStatus` | SceneGraph API för att hämta sekretesstatus från ADBMobile SDK. |
|  | Mer information finns i avsnittet Opt-Out/Privacy Status i det äldre SDK. |  |
|  |  |  |
| **Analytics**   |  |  |
|  | `trackState` | SceneGraph API för att spåra status på ADBMobile SDK. |
|  | `trackAction` | SceneGraph API för att spåra åtgärd på ADBMobile SDK. |
|  | `trackingIdentifier` | SceneGraph API för att hämta en spårningsidentifierare från ADBMobile SDK. |
|  | `userIdentifier` | SceneGraph API för att hämta en användaridentifierare från ADBMobile SDK. |
|  | `setUserIdentifier` | SceneGraph-API för att ange användaridentifieraren på ADBMobile SDK. |
|  | `getAllIdentifiers` | SceneGraph API hämtar alla användaridentiteter som är kända och beständiga av Roku SDK. |
|  | Mer information finns i avsnittet Analytik i det äldre SDK. |  |
|  |  |  |
| **Experience Cloud** |  |  |
|  | `visitorSyncIdentifiers` | SceneGraph API för att synkronisera Experience Cloud-identifierare på ADBMobile SDK. |
|  | `visitorMarketingCloudID` | SceneGraph API för att hämta Visitor Experience Cloud ID från ADBMobile SDK. |
|  | Mer information finns i avsnittet Experience Cloud i äldre SDK. |  |
|  |  |  |
| **Audience Manager** |  |  |
|  | `audienceSubmitSignal` | SceneGraph API för att skicka en målgruppshanteringssignal med egenskaper. |
|  | `audienceVisitorProfile` | SceneGraph API för att hämta en målgruppshanterarprofil från ADBMobile SDK. |
|  | `audienceDpid` | SceneGraph API för att få en målgrupp-Dpid från ADBMobile SDK. |
|  | `audienceDpuuid` | SceneGraph API för att få en målgrupp Dpuuid från ADBMobile SDK. |
|  | `audienceSetDpidAndDpuuid` | SceneGraph API för att ange målgrupp Dpid och Dpuuid på ADBMobile SDK. |
|  | Mer information finns i avsnittet Audience Manager i det äldre SDK. |  |
|  |  |  |
| **MediaHjärtslag** |  |  |
|  | `mediaTrackLoad` | SceneGraph API för att läsa in videoinnehåll för MediaHeartslag-spårning. |
|  | mediaTrackStart | SceneGraph API för att starta videospårningssession med MediaHeartslag. |
|  | `mediaTrackUnload` | SceneGraph API för att ta bort videoinnehåll från MediaHeartslag-spårning. |
|  | `mediaTrackPlay` | SceneGraph API för att spåra uppspelning av videoinnehåll. |
|  | mediaTrackPaus | SceneGraph API för att spåra pausat videoinnehåll. |
|  | `mediaTrackComplete` | SceneGraph-API för att spåra uppspelningen har slutförts för videoinnehåll. |
|  | `mediaTrackError` | SceneGraph API för att spåra uppspelningsfel. |
|  | mediaTrackEvent | SceneGraph API för att spåra uppspelningshändelser under spårning. Exempel: Ads, kapitel. |
|  | `mediaUpdatePlayhead` | SceneGraph-API för att skicka spelhuvuduppdateringar till MediaHeartslag under videouppföljning. |
|  | `mediaUpdateQoS` | SceneGraph API för att skicka QoS-uppdateringar till MediaHeartslag under videouppföljning. |
|  | Mer information finns i avsnittet MediaHeartslag i det äldre SDK. |  |

### SceneGraphConstants

| Konstant namn | Beskrivning |
|---|---|
| `API_RESPONSE` | Används för att hämta svarsobjektet från `adbmobileTask` nod `adbmobileApiResponse` fält |
| `DEBUG_LOGGING` | Används som `apiName` för `getDebugLogging` |
| `PRIVACY_STATUS` | Används som `apiName` för `getPrivacyStatus` |
| `TRACKING_IDENTIFIER` | Används som `apiName` för `trackingIdentifier` |
| `USER_IDENTIFIER` | Används som `apiName` för `userIdentifier` |
| `VISITOR_MARKETING_CLOUD_ID` | Används som `apiName` för `visitorMarketingCloudID` |
| `AUDIENCE_VISITOR_PROFILE` | Används som `apiName` för `audienceVisitorProfile` |
| `AUDIENCE_DPID` | Används som `apiName` för `audienceDpid` |
| `AUDIENCE_DPUUID` | Används som `apiName` för `audienceDpuuid` |

### adbmobileTask-nod

<table>
<thead>
<tr>
<td> Fält </td><td> Typ </td><td> Standard </td><td> Användning </td>
</tr>
</thead>
<tbody>
<tr>
<td> adbmobileApiCall </td>
<td> assokarisk </td>
<td> Ogiltig </td>
<td> Ändra INTE det här fältet eller låt det användas av programmet. Det här fältet används av ADBMobile SceneGraphConnector för att dirigera API-anrop via SceneGraph-noder och hämta svar. Därför är den här nyckeln/fältet reserverat för AdobeMobileSDK för SceneGraph-kompatibilitet. <b>Viktigt:</b> Om du ändrar det här fältet kan det leda till att AdobeMobileSDK inte fungerar korrekt.</td>
</tr>
<tr>
<td> adbmobileApiResponse </td>
<td> assokarisk </td>
<td> Ogiltig </td>
<td> Skrivskyddade Alla API:er som körs på AdobeMobileSDK returnerar svar i det här fältet. Registrera dig för ett återanrop om du vill lyssna efter uppdateringar till det här fältet för att ta emot svarsobjekt. Följande är formatet för svarsobjektet:  
<pre>
svar = { "apiName": &lt;scenegraphconstants.&gt;
               API_NAME&gt; "returnValue : &lt;api_response&gt; 
}</pre>
En instans av det här svarsobjektet skickas för alla API-anrop på AdobeMobileSDK som förväntas returnera ett värde enligt API-referenshandboken. Ett API-anrop för visitorMarketingCloudID() returnerar till exempel följande svarsobjekt: 
<pre>
svar = { "apiName": m. adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID "ReturnValue : "07050x25671x33760x72644x14" } 
</pre>
Svarsdata kan också vara ogiltiga. 
<pre>
svar = { "apiName": m. adbmobileConstants.
              VISITOR_MARKETING_CLOUD_ID "ReturnValue : ogiltig } 
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
Indata: Inga\
Returtyp: `SceneGraphConstants`

>[!NOTE]
>Se `ADBMobileConnector` API-referens för information.

### ADBMobile Constants

|  Funktion  | Konstant namn | Beskrivning   |
|---|---|---|
| Versionering | `version` | Konstant för att hämta versionsinformation för AdobeMobileLibrary |
| Sekretess/undantag | `PRIVACY_STATUS_OPT_IN` | Konstant för sekretesstatus som har valts i |
|  | `PRIVACY_STATUS_OPT_OUT` | Konstant för sekretessstatus har valts ut |
| MediaHeartslag-konstanter | Se konstanterna på den här sidan: <br/><br/>[Metoder för pulsslag i media.](/help/sdk-implement/track-av-playback/track-core/track-core-roku.md) | Använd dessa konstanter med MediaHeartslag API:er |
| Standardmetadata | Se konstanterna på den här sidan: <br/><br/>[Standardmetadataparametrar.](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md) | Använd dessa konstanter för att bifoga standardmetadata för video/ad i API:er för MediaHeartslag |

Globalt definierat verktyg `MediaHeartbeat` API:er på äldre AdobeMobileLibrary är tillgängliga *som* i SceneGraph-miljön eftersom de inte använder några bricktskriptkomponenter som inte är tillgängliga i SceneGraph-noder. Mer information om dessa metoder finns i tabellen nedan:

### Globala metoder för MediaHeartslag

| Metod | Beskrivning |
| --- | --- |
| `adb_media_init_mediainfo` | Den här metoden returnerar ett initierat medieinformationsobjekt `Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object` |
| `adb_media_init_adinfo` | Den här metoden returnerar initierat Ad Information-objekt `Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object` |
| `adb_media_init_chapterinfo` | Den här metoden returnerar det initierade kapitelinformationsobjektet.  `Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object` |
| `adb_media_init_adbreakinfo` | Den här metoden returnerar initierat AdBreak-informationsobjekt.  `Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object` |
| `adb_media_init_qosinfo` | Den här metoden returnerar ett initierat QoS-informationsobjekt.  `Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object` |

## Implementering {#implementation}

1. **Hämta Roku-biblioteket -** Hämta [det senaste Roku-biblioteket.](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.2)

1. **Konfigurera utvecklingsmiljön**

   1. Kopiera `adbmobile.brs` (AdobeMobileLibrary) i din `pkg:/source/` katalog.

   1. Om du vill ha stöd för scendiagram kopierar du `adbmobileTask.brs` och `adbMobileTask.xml` in i `pkg:/components/` katalog.

1. **Initiera**

   1. Importera `adbmobile.brs` in i scenen.

      ```
      <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
      ```

   1. Skapa en instans av `adbmobileTask` nod i scenen.

      ```
      m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
      ```

   1. Hämta en instans av `adbmobile` Koppling för SceneGraph med hjälp av `adbmobileTask` förekomst.

      ```
      m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
      ```

   1. Hämta `adbmobile` SG-konstanter.

      ```
      m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
      ```

   1. Registrera ett motringningsmeddelande för att ta emot svarsobjekt för alla `AdbMobile` API-anrop.

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

### Exempel på API-anrop på äldre SDK

```
'get an instance of SDK 
m.adbmobile = ADBMobile() 
   
'execute setter APIs 
m.adbmobile.setDebugLogging(true) 
   
'execute getter APIs 
debugLogging = m.adbmobile.getDebugLogging()
```

### Exempel-API anrop till SG SDK

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


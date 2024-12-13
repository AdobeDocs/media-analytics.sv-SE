---
title: Så här konfigurerar du Media SDK på Android
description: Följ de här stegen för att konfigurera Media SDK-programmet på Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 6%

---

# Konfigurera Android{#set-up-android}

Lär dig hur du konfigurerar Streaming Media Collection för Android-enheter.

>[!IMPORTANT]
>
>När stödet för version 4 Mobile SDK upphör den 31 augusti 2021 upphör även stödet för Media Analytics SDK för iOS och Android.  Mer information finns i [Vanliga frågor och svar om SDK End-of-Support i Media Analytics](/help/additional-resources/end-of-support-faqs.md).


## Förutsättningar

* **Hämta giltiga konfigurationsparametrar för Media SDK**
Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.
* **Implementera ADBMobil för Android i ditt program**
Mer information om Adobe Mobile SDK finns i [Android SDK 4.x for Experience Cloud Solutions.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html)

* **Tillhandahåll följande funktioner i din mediespelare:**
   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som tillhandahåller spelarinformation* - Den här informationen innehåller information som medienamnet och spelhuvudets position.

## SDK-implementering

1. Lägg till ditt nedladdade Media SDK i ditt projekt.

   1. Expandera zip-filen för Android (t.ex. `MediaSDK-android-v2.*.zip`).
   1. Kontrollera att filen `MediaSDK.jar` finns i katalogen `libs/`.

   1. Lägg till biblioteket i ditt projekt.

      **IntelliJ IDEA:**

      1. Högerklicka på projektet på panelen **[!UICONTROL Project navigation]**.
      1. Välj **[!UICONTROL Open Module Settings]**.
      1. Välj **[!UICONTROL Libraries]** under **[!UICONTROL Project Settings]**.

      1. Klicka på **[!UICONTROL +]** om du vill lägga till ett nytt bibliotek.
      1. Välj **[!UICONTROL Java]** och navigera till filen `MediaSDK.jar`.

      1. Välj de moduler där du vill använda det mobila biblioteket.
      1. Klicka på **[!UICONTROL Apply]** och sedan på **[!UICONTROL OK]** för att stänga fönstret Modulinställningar.

      **Eclipse:**

      1. Högerklicka på projektnamnet i Eclipse IDE.
      1. Klicka på **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Välj `MediaSDK.jar`.
      1. Klicka på **[!UICONTROL Open]**.
      1. Högerklicka på projektet igen och klicka på **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Klicka på flikarna **[!UICONTROL Order]** och **[!UICONTROL Export]**.

      1. Kontrollera att filen `MediaSDK.jar` är markerad.

1. Importera biblioteket.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. Skapa instansen `MediaHeartbeatConfig`.

   Här följer ett exempel på `MediaHeartbeatConfig`-initiering:

   ```java
   // Media Heartbeat Initialization
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_;
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>;
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>;
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>;
   config.playerName = <SAMPLE_PLAYER_NAME>;
   config.ssl = <true/false>;
   config.debugLogging = <true/false>;
   ```

1. Implementera gränssnittet `MediaHeartbeatDelegate`.

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override
   public MediaObject getQoSObject() {
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>);
   }
   
   //Replace <currentPlaybackTime> with the video player current playback time
   @Override
   public Double getCurrentPlaybackTime() {
       return <currentPlaybackTime>;
   }
   ```

1. Skapa instansen `MediaHeartbeat`.

   Använd instansen `MediaHeartbeatConfig` och instansen `MediaHertbeatDelegate` för att skapa instansen `MediaHeartbeat`.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Kontrollera att din `MediaHeartbeat`-instans är tillgänglig och att *inte frigörs förrän i slutet av sessionen*. Den här instansen kommer att användas för alla följande spårningshändelser.

**Lägger till programbehörigheter**

Ditt program som använder Media SDK kräver följande behörigheter för att skicka data i spårningsanrop:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Om du vill lägga till de här behörigheterna lägger du till följande rader i filen `AndroidManifest.xml` i programmets projektkatalog:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migrerar från version 1.x till 2.x i Android**

I version 2.x konsolideras alla publika metoder i klassen `com.adobe.primetime.va.simple.MediaHeartbeat` så att det blir enklare för utvecklare. Dessutom konsolideras nu alla konfigurationer i klassen `com.adobe.primetime.va.simple.MediaHeartbeatConfig`.

Mer information om hur du migrerar från 1.x till 2.x finns i dokumentationen för den äldre implementeringen.

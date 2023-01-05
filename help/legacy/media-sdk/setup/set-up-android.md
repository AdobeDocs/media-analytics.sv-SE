---
title: Konfigurera Media SDK på Android
description: Följ de här stegen för att konfigurera Media SDK-programmet på Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 8%

---

# Konfigurera Android{#set-up-android}

Lär dig hur du konfigurerar Streaming Media Analytics för Android-enheter.

>[!IMPORTANT]
>
>När stödet för version 4 Mobile SDK upphör den 31 augusti 2021 upphör även stödet för Media Analytics SDK för iOS och Android i Adobe.  Mer information finns i [Vanliga frågor om supporten för Media Analytics SDK](/help/additional-resources/end-of-support-faqs.md).


## Förutsättningar

* **Hämta giltiga konfigurationsparametrar för Media SDK**
Dessa parametrar kan hämtas från en Adobe-representant när du har konfigurerat ditt analyskonto.
* **Implementera ADBMobil för Android i ditt program**
Mer information om Adobe Mobile SDK-dokumentationen finns i [Android SDK 4.x för Experience Cloud Solutions.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html)

* **Tillhandahåll följande funktioner i din mediespelare:**
   * *Ett API för att prenumerera på spelarhändelser* - Media SDK kräver att du anropar en uppsättning enkla API:er när händelser inträffar i spelaren.
   * *Ett API som tillhandahåller spelarinformation* - Den här informationen innehåller information som medienamnet och spelhuvudets position.

## SDK-implementering

1. Lägg till din hämtade Media SDK i ditt projekt.

   1. Expandera zip-filen för Android (t.ex. `MediaSDK-android-v2.*.zip`).
   1. Verifiera att `MediaSDK.jar` filen finns i `libs/` katalog.

   1. Lägg till biblioteket i ditt projekt.

      **IntelliJ IDEA:**

      1. Högerklicka på projektet på panelen **[!UICONTROL Project navigation]**.
      1. Välj **[!UICONTROL Open Module Settings]**.
      1. Under **[!UICONTROL Project Settings]** väljer du **[!UICONTROL Libraries]**.

      1. Klicka **[!UICONTROL +]** för att lägga till ett nytt bibliotek.
      1. Välj **[!UICONTROL Java]** och navigera till `MediaSDK.jar` -fil.

      1. Välj de moduler där du vill använda det mobila biblioteket.
      1. Klicka på **[!UICONTROL Apply]** och sedan på **[!UICONTROL OK]** för att stänga fönstret Modulinställningar.

      **Eclipse:**

      1. Högerklicka på projektnamnet i Eclipse IDE.
      1. Klicka på  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Välj `MediaSDK.jar`.
      1. Klicka på **[!UICONTROL Open]**.
      1. Högerklicka på projektet igen och klicka på  **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Klicka på flikarna **[!UICONTROL Order]** och **[!UICONTROL Export]**.

      1. Se till att `MediaSDK.jar` filen är markerad.


1. Importera biblioteket.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. Skapa `MediaHeartbeatConfig` -instans.

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

1. Implementera `MediaHeartbeatDelegate` gränssnitt.

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

1. Skapa `MediaHeartbeat` -instans.

   Använd `MediaHeartbeatConfig` -instans och `MediaHertbeatDelegate` instans för att skapa `MediaHeartbeat` -instans.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Se till att `MediaHeartbeat` -instansen är tillgänglig och *avallokeras inte förrän sessionen är slut*. Den här instansen används för alla följande spårningshändelser.

**Lägga till programbehörigheter**

Ditt program som använder Media SDK kräver följande behörigheter för att skicka data i spårningsanrop:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Lägg till följande rader i `AndroidManifest.xml` i programprojektkatalogen:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migrera från version 1.x till 2.x i Android**

I version 2.x konsolideras alla publika metoder i `com.adobe.primetime.va.simple.MediaHeartbeat` för utvecklare. Dessutom konsolideras nu alla konfigurationer i `com.adobe.primetime.va.simple.MediaHeartbeatConfig` klassen.

Mer information om hur du migrerar från 1.x till 2.x finns i dokumentationen för den äldre implementeringen.
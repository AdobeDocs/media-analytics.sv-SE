---
title: Installera Media Analytics med Experience Platform Edge
description: Lär dig hur du implementerar direktuppspelningsmedia för Adobe med Experience Platform Edge.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: dfdb1415-105e-4c41-bedc-ecb85ed1b1d9
source-git-commit: 68710e8d68266c62ded94a14892ddc78a0807a49
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 0%

---

# Installera Media Analytics med Experience Platform Edge

Med Adobe Experience Platform Edge kan ni skicka data till flera produkter på en central plats. Experience Edge vidarebefordrar lämplig information till önskade produkter. Med det här konceptet kan ni konsolidera implementeringsinsatser, särskilt genom att sprida flera datalösningar.

Följande bild visar hur en Media Analytics-implementering kan använda Experience Platform Edge för att göra data tillgängliga i Analysis Workspace, antingen i Adobe Analytics eller Customer Journey Analytics:

![CJA-arbetsflöde](assets/cja-implementation.png)

En översikt över alla implementeringsalternativ, inklusive implementeringsmetoder som inte använder Experience Platform Edge, finns i [Implementera direktuppspelningsmedia för Adobe Analytics eller Customer Journey Analytics](/help/implementation/overview.md).

>[!IMPORTANT]
>
>Direktuppspelningsmedia är ännu inte integrerat med AEP Web SDK.

Oavsett om du använder Mobile SDK eller API:t för att implementera direktuppspelningsmedia med Experience Edge måste du först slutföra följande avsnitt:

## Konfigurera schemat i Adobe Experience Platform

För att standardisera datainsamlingen för användning i olika program som utnyttjar Adobe Experience Platform har Adobe skapat den öppna och offentligt dokumenterade standarden Experience Data Model (XDM).

Så här skapar och konfigurerar du ett schema:

1. Börja skapa schemat enligt beskrivningen i Adobe Experience Platform [Skapa och redigera scheman i användargränssnittet](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

   När du skapar schemat väljer du [!UICONTROL **XDM ExperienceEvent**] från [!UICONTROL **Skapa schema**] listruta.

1. I [!UICONTROL **Disposition**] området, i [!UICONTROL **Fältgrupper**] avsnitt, markera [!UICONTROL **Lägg till**] söker du efter och lägger till följande nya fältgrupper i schemat:
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   När du har lagt till fältgrupperna bör de visas i [!UICONTROL **Fältgrupper**] enligt följande:

   ![Tillagda fältgrupper](assets/schema-field-groups-added.png)

1. Välj [!UICONTROL **Bekräfta**] för att spara ändringarna.

1. (Valfritt) Du kan dölja vissa fält som inte används av API:t för mediekant. Om du döljer dessa fält blir schemat enklare att läsa och förstå, men det är inte nödvändigt. Dessa fält refererar endast till fälten i `MediaAnalytics Interaction Details` fältgrupp.

+++ Expandera här om du vill visa instruktioner för fält som du kan dölja.

   1. I [!UICONTROL **Struktur**] markerar du `Media Collection Details` fält och sedan markera [!UICONTROL **Hantera relaterade fält**].

      ![manage-related-fields](assets/manage-related-fields.png)

   1. Aktivera alternativet att [!UICONTROL **Visa visningsnamn för fält**] uppdaterar du sedan schemat enligt följande:

      * I `Media Collection Details` > `Advertising Details` fält, dölj följande rapporteringsfält: `Ad Completed`, `Ad Started`och `Ad Time Played`.

      * I `Media Collection Details` > `Advertising Pod Details` fält, dölj följande rapporteringsfält: `Ad Break ID`

      * I `Media Collection Details` > `Chapter Details` fält, dölj följande rapporteringsfält: `Chapter Completed`, `Chapter ID`, `Chapter Started`och `Chapter Time Played`.

      * I `Media Collection Details` fält, dölj `List Of States` fält.

        ![dölj mediesamlingslägen](assets/schema-hide-media-collection-states.png)

      * I `Media Collection Details` > `List Of States End` och `Media Collection Details` > `List Of States Start` fält, dölj följande rapporteringsfält: `Player State Count`, `Player State Set`och `Player State Time`.

        ![fält att dölja](assets/schema-hide-listofstates.png)

      * I `Media Collection Details` > `Qoe Data Details` fält, dölj följande rapporteringsfält: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Impacted Streams`, `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration`och `Total Stalling Duration`.

      * I `Media Collection Details` > `Session Details` fält, dölj följande rapporteringsfält: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID`, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3`, `Pccr`, `Total Pause Duration`, `Unique Time Played`och `Video Segment`.

   1. Välj [!UICONTROL **Bekräfta**] för att spara ändringarna.

   1. I [!UICONTROL **Struktur**] område, aktivera alternativet att [!UICONTROL **Visa visningsnamn för fält**] väljer du `List Of Media Collection Downloaded Content Events` fält.

   1. Välj [!UICONTROL **Hantera relaterade fält**] uppdaterar du sedan schemat enligt följande:


      * I `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` fält, dölj följande rapporteringsfält: `Ad Completed`, `Ad Started`och `Ad Time Played`.

      * I `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` fält, dölj följande rapporteringsfält: `Ad Break ID`

      * I `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` fält, dölj följande rapporteringsfält: `Chapter Completed`, `Chapter ID`, `Chapter Started`och `Chapter Time Played`.

      * I `List Of Media Collection Downloaded Content Events` > `Media Details` fält, dölj `List Of States` fält.

      * I `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` och `Media Collection Details` > `List Of States Start` fält, dölj följande rapporteringsfält: `Player State Count`, `Player State Set`och `Player State Time`.

      * I `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` fält, dölj följande rapporteringsfält: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration`och `Total Stalling Duration`.

      * I `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` fält, dölj följande rapporteringsfält: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID`, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pccr`, `Pev3`, `Total Pause Duration`, `Unique Time Played`och `Video Segment`.

      * I `List Of Media Collection Downloaded Content Events` > `Media Details`  fält, dölj `Media Session ID` fält.

   1. Välj [!UICONTROL **Bekräfta**] för att spara ändringarna.

   1. I [!UICONTROL **Struktur**] markerar du `Media Reporting Details` fält, markera [!UICONTROL **Hantera relaterade fält**].

   1. Aktivera alternativet att [!UICONTROL **Visa visningsnamn för fält**] uppdaterar du sedan schemat enligt följande:

      * I `Media Reporting Details` fält, dölj följande fält: `Error Details`, `List Of States End`, `List of States Start`och `Media Session ID`.

   1. Välj [!UICONTROL **Bekräfta**] > [!UICONTROL **Spara**]  för att spara ändringarna.

1. Fortsätt med [Skapa en datauppsättning i Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform).

## Skapa en datauppsättning i Adobe Experience Platform

1. Se till att du konfigurerar ett schema enligt beskrivningen i [Konfigurera schemat i Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

1. Börja skapa datauppsättningen enligt beskrivningen i Adobe Experience Platform [Användargränssnittshandbok för datauppsättningar](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en#create).

   När du väljer ett schema för datauppsättningen väljer du det schema som du skapade tidigare, vilket beskrivs i [Konfigurera schemat i Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

1. Fortsätt med [Konfigurera ett datastream i Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

## Konfigurera ett datastream i Adobe Experience Platform

1. Se till att du har skapat en datauppsättning enligt beskrivningen i [Skapa en datauppsättning i Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform).

1. Skapa ett nytt datastream enligt beskrivningen i [Konfigurera ett datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en).

   När du skapar dataströmmen måste du göra följande konfigurationsval:

   * I [!UICONTROL **Händelseschema**] när du skapar datastream måste du välja det schema som du skapade i [Konfigurera schemat i Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform). Välj [!UICONTROL **Spara**].

     >[!IMPORTANT]
     >
         > Markera inte [!UICONTROL **Save and Add Mapping**] därför att detta resulterar i mappningsfel för tidsstämpelfältet.
     
     ![Skapa datastream och välj schema](assets/datastream-create-schema.png)

   * Lägg till någon av följande tjänster i datastream, beroende på om du använder Adobe Analytics eller Customer Journey Analytics:

      * [!UICONTROL **Adobe Analytics**] (om Adobe Analytics används)

        Om du använder Adobe Analytics måste du definiera en rapportserie, enligt beskrivningen i avsnittet [Definiera en rapportsvit](#define-a-report-suite) i den här artikeln.

      * [!UICONTROL **Adobe Experience Platform**] (om Customer Journey Analytics används)

     Mer information om hur du lägger till en tjänst i ett datastream finns i avsnittet&quot;Lägg till tjänster i ett datastream&quot; i [Konfigurera ett datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

     ![Lägg till tjänsten Adobe Analytics](assets/datastream-add-service.png)

   * Expandera [!UICONTROL **Avancerade alternativ**] och sedan aktivera [!UICONTROL **Medieanalys**] alternativ.

     ![Media Analytics, alternativ](assets/datastream-media-check.png)

1. Nu kan du implementera [Media Edge API](/help/implementation/edge/implementation-edge-api.md) eller [Media Edge SDK](/help/implementation/edge/edge-mobile-sdk.md) för att börja samla in data från medieanalyser.

   När du har samlat in data kan du [Skapa en anslutning i Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

## Skapa en anslutning i Customer Journey Analytics

>[!NOTE]
>
>Följande procedur krävs bara om du använder Customer Journey Analytics.


1. Se till att du har skapat en datastream enligt beskrivningen i [Konfigurera ett datastream i Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

1. Skapa en anslutning enligt beskrivningen i Customer Journey Analytics [Skapa en anslutning](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=en).

   När du skapar anslutningen krävs följande konfigurationsval för implementering av direktuppspelningsmedia:

   1. Välj den datauppsättning som du skapade tidigare, enligt beskrivningen i [Skapa en datauppsättning i Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform).

   1. Se till att [!UICONTROL **Importera alla nya data**] inställningen är aktiverad.

1. Fortsätt med [Skapa en datavy i Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

## Skapa en datavy i Customer Journey Analytics

>[!NOTE]
>
>Följande procedur krävs bara om du använder Customer Journey Analytics.

1. Se till att du har skapat en anslutning i Customer Journey Analytics enligt beskrivningen i [Skapa en anslutning i Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

1. Skapa en datavy enligt beskrivningen i [Skapa eller redigera en datavy](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=en).

   När du skapar datavyn krävs följande konfigurationsval för implementering av direktuppspelningsmedia:

   1. I [!UICONTROL **Anslutning**] markerar du anslutningen som du skapade tidigare, enligt beskrivningen i [Skapa en anslutning i Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

      Det kan ta upp till 15 minuter innan anslutningen som du skapade är tillgänglig att välja.

   1. På [!UICONTROL **Komponenter**] -fliken, i [!UICONTROL **Schemafält**] söker du efter varje komponent i tabellen nedan och drar den till [!UICONTROL **Mått**] -panelen. Om det finns flera fält med samma namn använder du XDM-sökvägen för att se till att det är rätt fält.

      **Huvudinnehåll - Innehållsmått**

      | Komponentnamn | XDM-sökväg |
      |----------|---------|
      | Media börjar | mediaReporting.sessionDetails.isViewed |
      | Vyer för mediesegment | mediaReporting.sessionDetails.hasSegmentView |
      | Innehållet börjar | mediaReporting.sessionDetails.isPlayed |
      | Innehållet slutförs | mediaReporting.sessionDetails.isCompleted |
      | Innehållstid | mediaReporting.sessionDetails.timePlayed |
      | Medietid tillagd | mediaReporting.sessionDetails.totalTimePlayed |
      | Unik uppspelningstid | mediaReporting.sessionDetails.uniqueTimePlayed |
      | 10 % förloppsmärke | mediaReporting.sessionDetails.hasProgress10 |
      | Genomsnittlig målgrupp i minuter | mediaReporting.sessionDetails.averageMinuteAudience |


      **Kapitel och annonser - versaler och annonser**

      | Komponentnamn | XDM-sökväg |
      |----------|---------|
      | Kapitel startat | mediaReporting.chapterDetails.isStarted |
      | Kapitel slutfört | mediaReporting.chapterDetails.isCompleted |
      | Kapiteltid spelad | mediaReporting.chapterDetails.timePlayed |
      | Ad Started | mediaReporting.advertisingDetails.isStarted |
      | Annonsen har slutförts | mediaReporting.advertisingDetails.isCompleted |
      | Annonstid | mediaReporting.advertisingDetails.timePlayed |


      **QoE - QoE-mått**

      | Komponentnamn | XDM-sökväg |
      |----------|---------|
      | Tid att starta | mediaReporting.qoeDataDetails.timeToStart |
      | Drops Before Starts | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | Buffertpåverkade strömmar | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | Ändrade bithastighetsströmmar som påverkas | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | Bithastighetsändringar | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | Genomsnittlig bithastighet | mediaReporting.qoeDataDetails.bitrateAverage |
      | Släppta bildrutor | mediaReporting.qoeDataDetails.droppedFrames |
      | Fel | mediaReporting.qoeDataDetails.errorCount |
      | Felpåverkade strömmar | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | Ignorerade bildrutepåverkade strömmar | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |


      **Spelartillstånd - Mätvärden för spelartillstånd**

      | Komponentnamn | XDM-sökväg |
      |----------|---------|
      | Uppsättning med spelartillstånd | mediaReporting.states.isSet |
      | Antal spelartillstånd | mediaReporting.states.count |
      | Spelarlägestid | mediaReporting.states.time |


   1. Uppdatera etiketterna (i [!UICONTROL **Sammanhangsetiketter**] (nedrullningsbar meny) för komponenterna i följande tabell. Sök efter och dra komponenter som inte redan finns på mätpanelen till panelen.

      | Komponentnamn | Kontextetikett |
      |---------|----------|
      | Tidsgräns för mediessionsserver | Media: Sekunder sedan senaste samtalet |
      | Medietid tillagd | Media: Medietid tillagd |
      | Buffertvaraktighet totalt | Media: Total buffertvaraktighet |
      | Tid att starta | Media: Tid att starta |
      | Total pausvaraktighet | Media: Total paus |

   1. Om du vill lägga till uppdelningar i ditt Customer Journey Analytics-projekt lägger du till följande dimensioner i [!UICONTROL **Dimensioner**] panel:

      | XDM-sökväg | Komponentnamn |
      |---------|----------|
      | mediaReporting.states.name | Spelarlägesnamn |
      | mediaReporting.sessionDetails.ID | ID för mediesession |

      Förutom dimensionerna i den här tabellen kan du lägga till andra dimensioner som du vill göra tillgängliga för att filtrera data efter i Customer Journey Analytics-projekt.

1. Välj [!UICONTROL **Spara och fortsätt**] > [!UICONTROL **Spara och avsluta**] för att spara ändringarna.

1. Fortsätt med [Skapa och konfigurera ett projekt i Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## Skapa och konfigurera ett projekt i Customer Journey Analytics

1. Se till att du har skapat en datavy i Customer Journey Analytics enligt beskrivningen i [Skapa en datavy i Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

1. I Customer Journey Analytics, på [!UICONTROL **Arbetsyta**] -fliken, i [!UICONTROL **Projekt**] område, markera [!UICONTROL **Skapa projekt**].

1. Välj [!UICONTROL **Tomt projekt**] > [!UICONTROL **Skapa**].

1. I det nya projektet markerar du datavyn som du skapade tidigare.

   När du skapar paneler i ditt projekt kan du använda alla komponenter som du har lagt till i datavyn, enligt beskrivningen i [Skapa en datavy i Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

   Följande fyra paneler är exempel på paneler som du kan skapa:

   ![Panelen Huvudinnehåll](assets/main-content-panel.png)

   ![Panelen Kapitel och annonser](assets/chapter-and-ads-panel.png)

   ![QoE-panelen](assets/qoe-panel.png)

   ![Panelen Plattform](assets/player-state-panel.png)

1. Välj **Panel** ikonen i den vänstra listen och dra sedan i [!UICONTROL **Medievisningsprogram för samtidig användning**] och [!UICONTROL **Medieuppspelningstid**] -panelen.

   De två panelerna ska se ut så här:

   ![Panelen Medievisningsprogram för samtidig användning](assets/media-concurrent-viewers-panels.png)

   ![Medieuppspelningstid som använts på panelen](assets/media-playback-time-spent-panels.png)

1. Dela projektet enligt beskrivningen i [Dela projekt](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >   Om de användare du vill dela med inte är tillgängliga kontrollerar du att användarna har användar- och administratörsåtkomst till Customer Journey Analytics i Adobe Admin Console.

1. Fortsätt med [Skicka data till Experience Platform Edge](#send-data-to-experience-platform-edge).

## Skicka data till Experience Platform Edge med AEP Mobile SDK

Du kan använda Adobe Experience Platform mobil-SDK för att skicka mobildata till Experience Platform Edge.

Använd följande dokumentationsresurser för att slutföra implementeringen av både iOS och Android:

* [Kom igång](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [API-referens](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [Migrera till Adobe Streaming Media för Edge Network-tillägg](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

Du kan också använda en anpassad implementering av Edge-API:erna med följande resurser:

* [Översikt över API för Media Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [Komma igång med API för Media Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [Felsökningsguide för Media Edge API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [Använda Open API-specifikationsfilen för Media Edge API:er](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/swagger.html)

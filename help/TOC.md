---
audience: end-user
user-guide-title: Adobe Analytics for Audio and Video
product: adobe analytics
sub-product: media analytics
translation-type: tm+mt
source-git-commit: d9f6c99b26153ef81d4623c30361fc5b34385bf6

---


# Adobe Analytics för ljud och video {#using}

+ [Mäta ljud och video i Adobe Analytics](media-overview.md)
+ Mätningsalternativ {#measurement-options}
   + Spårning av milstolpe för mediemodulen {#mm-milestone-tracking}
      + [Översikt över milstolpe](measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrera milstolpe till Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migrera från milstolpe till anpassad länk](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Custom Link in Analytics {#cl-in-aa}
      + [Implementeringshandbok för anpassad länk](measurement-options/cl-in-aa/cl-impl-guide.md)
+ Introduktion till ljud- och videoanalys {#intro-to-ava}
   + [Förutsättningar](intro-to-ava/prereqs.md)
   + Implementeringssökvägar {#implementation-paths}
      + [Översikt](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Klientsidan](intro-to-ava/implementation-paths/client-side-path.md)
      + [Adobe Experience Platform Launch](intro-to-ava/implementation-paths/launch-path.md)
      + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
   + [Audience Manager - aktivering](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [Hämta SDK:er](sdk-implement/download-sdks.md)
   + Konfigurera {#setup}
      + [Översikt](sdk-implement/setup/setup-overview.md)
      + [Konfigurera Android](sdk-implement/setup/set-up-android.md)
      + [Konfigurera iOS](sdk-implement/setup/set-up-ios.md)
      + [Konfigurera JavaScript](sdk-implement/setup/set-up-js.md)
      + [Konfigurera kromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Konfigurera Roku](sdk-implement/setup/set-up-roku.md)
   + Spåra ljud- och videouppspelning {#track-av-playback}
      + [Översikt](sdk-implement/track-av-playback/track-core-overview.md)
      + Spåra grundläggande ljud- och videouppspelning {#track-core}
         + [Spåra kärnuppspelning på Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Spåra kärnuppspelning på iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + [Spåra kärnuppspelning i JavaScript](sdk-implement/track-av-playback/track-core/track-core-js.md)
         + [Spåra kärnuppspelning på Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Spåra kärnuppspelning på Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Track Buffering {#track-buffering}
         + [Track Buffering på Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Spåra buffring på iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + [Spåra buffring på JavaScript](sdk-implement/track-av-playback/track-buffering/track-buffering-js.md)
         + [Track Buffering on Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Track Buffering på Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Spåra sökning {#track-seeking}
         + [Spåra sökning på Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Spåra sökning på iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + [Spåra sökning i JavaScript](sdk-implement/track-av-playback/track-seeking/track-seeking-js.md)
         + [Spåra sökning på Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Spåra sökning på Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Implementera standardmetadata {#impl-std-metadata}
         + [Implementera standardmetadata på Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementera standardmetadata på iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS-metadatanycklar](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + [Implementera standardmetadata i JavaScript](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)
         + [Implementera standardmetadata på Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Standardmetadataparametrar - kromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Implementera standardmetadata på Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Standardmetadataparametrar - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Spåra annonser {#track-ads}
      + [Översikt](sdk-implement/track-ads/track-ads-overview.md)
      + [Spåra annonser på Android](sdk-implement/track-ads/track-ads-android.md)
      + [Spåra annonser på iOS](sdk-implement/track-ads/track-ads-ios.md)
      + [Spåra annonser på JavaScript](sdk-implement/track-ads/track-ads-js.md)
      + [Spåra annonser på Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Spåra annonser på Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Implementera standardannonsmetadata {#impl-std-ad-metadata}
         + [Implementera standardannonsmetadata på Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Implementera standardannonsmetadata på iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + [Implementera standardannonsmetadata i JavaScript](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
         + [Implementera standardannonsmetadata på Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Spåra kapitel och segment {#track-chapters}
      + [Översikt](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Spåra kapitel och segment på Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Spåra kapitel och segment på iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + [Spåra kapitel och segment i JavaScript](sdk-implement/track-chapters/track-chapters-js.md)
      + [Spåra kapitel och segment i Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Spåra kapitel och segment på Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Spåra upplevelsekvalitet {#track-qos}
      + [Översikt](sdk-implement/track-qos/track-qos-overview.md)
      + [Spåra upplevelsekvalitet på Android](sdk-implement/track-qos/track-qos-android.md)
      + [Spåra upplevelsekvalitet på iOS](sdk-implement/track-qos/track-qos-ios.md)
      + [Spåra upplevelsekvalitet i JavaScript](sdk-implement/track-qos/track-qos-js.md)
      + [Spåra upplevelsekvalitet på Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Spåra upplevelsekvalitet på Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Spåra fel {#track-errors}
      + [Översikt](sdk-implement/track-errors/track-errors-overview.md)
      + [Spåra fel på Android](sdk-implement/track-errors/track-errors-android.md)
      + [Spåra fel på iOS](sdk-implement/track-errors/track-errors-ios.md)
      + [Spåra fel i JavaScript](sdk-implement/track-errors/track-errors-js.md)
      + [Spåra fel i Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Spåra fel på Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Avanmäl dig och sekretess](sdk-implement/opt-out-privacy.md)
   + Spåra scenarier {#tracking-scenarios}
      + [VOD-uppspelning utan annonser](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [VOD-uppspelning med pre-roll-annonser](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [VOD-uppspelning med överhoppade annonser](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [VOD-uppspelning med ett kapitel](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [VOD-uppspelning med ett överhoppat kapitel](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [VOD-uppspelning med sökning i huvudinnehållet](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [VOD-uppspelning med buffring](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Flera VOD-spår parallellt](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [VOD - en spårare för flera sessioner](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Live-huvudinnehåll](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Live-huvudinnehåll med sekventiell spårning](sdk-implement/tracking-scenarios/live-sequential.md)
   + Validering {#validation}
      + [Valideringsöversikt](sdk-implement/validation/validation-overview.md)
      + [Test 1: Standarduppspelning](sdk-implement/validation/test1-standard-playback.md)
      + [Test 2: Medieavbrott](sdk-implement/validation/test2-media-interrupt.md)
      + [Information om provsamtal](sdk-implement/validation/test-call-details.md)
      + [Beskrivning av parametern Heartbeat](sdk-implement/validation/heartbeat-params.md)
      + Felsökning {#debugging}
         + [SDK-felsökning](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Konfigurera Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [Skapa en ny felsökningsrapport](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Felsöka instrumentpaneler och rapporter](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analyser i OTT-appar {#analytics-with-ott}
      + [Spåra applägen](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Spåra programåtgärder](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Ange användar-ID](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT och Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT och Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Cookbook {#cookbook}
      + [SDK Cookbook](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [Hantera programavbrott under uppspelning](sdk-implement/cookbook/app-interrupts.md)
      + [Lösa huvudspel:uppspelning mellan annonser](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Återupptar inaktiva sessioner](sdk-implement/cookbook/resuming-inactive.md)
      + [Spårning i SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Migrering av Media Analytics 1.x till 2.x {#va-1x-to-2x}
      + [Migreringsöversikt](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Kodjämförelse: 1.x till 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [1.x till 2.x API-konvertering](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Media Analytics SDK för att starta migrering {#sdk-to-launch}
      + [SDK för att starta migrering](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + SDK to Launch Migration Platform Guides {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Media Collection API (RESTful) {#media-collection-api}
   + [Översikt](media-collection-api/mc-api-overview.md)
   + API-referens {#mc-api-ref}
      + [Sessionsbegäran](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Händelsebegäran](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Begärandeparametrar](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Händelsetyper och beskrivningar](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [JSON-valideringsscheman](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + Implementera API {#mc-api-impl}
      + [Snabbstart](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Ange HTTP-begärandetyp i spelaren](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Hämta ett sessions-ID](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Implementera en händelsebegäran](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Validerar händelsebegäranden](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Skicka Ping-händelser](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [Skicka QoE-data](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Stöd för anpassade metadata](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Timeout-villkor](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [Kontrollera händelseordningen](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Köa händelser när sessionssvar är långsamma](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Tidslinjer för mediespårning {#mc-api-timelines}
      + [Tidslinje 1 - Visa till innehållets slut](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Tidslinje 2 - sessionen användaren avbryter](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Tidslinje 3 - kapitel](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
   + [Spåra hämtat innehåll](media-collection-api/track-downloaded-content.md)
+ Cookbook {#media-analytics-cookbook}
   + [Cookbook](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Attribut för medieström](media-analytics-cookbook/media-dimensions.md)
+ Metoder och metadata {#metrics-and-metadata}
   + [Parametrar för ljud och video](metrics-and-metadata/audio-video-parameters.md)
   + [Annonsparametrar](metrics-and-metadata/ad-parameters.md)
   + [Kapitelparametrar](metrics-and-metadata/chapter-parameters.md)
   + [Kvalitetsparametrar](metrics-and-metadata/quality-parameters.md)
   + [Segment](metrics-and-metadata/segments.md)
   + [Beräknade mått](metrics-and-metadata/calculated-metrics.md)
+ Rapportering och analys {#media-reports}
   + [Aktivera medierapporter](media-reports/media-reports-enable.md)
   + Standardrapporter för media {#media-default-reports}
      + [Översikt över standardrapporter](media-reports/media-default-reports/default-reports-overview.md)
      + [Medieöversikt](media-reports/media-default-reports/media-reports-overview.md)
      + [Medieinformation](media-reports/media-default-reports/media-reports-detail.md)
      + [Media Daypart](media-reports/media-default-reports/media-reports-daypart.md)
      + [Media Concurrent Viewers](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [Hämta JSON-rapportdata för samtidiga visningsprogram](media-reports/media-default-reports/get-concurrent-json.md)
   + [Mallar för arbetsytan Media](media-reports/media-workspace-templates.md)
+ [Federated Analytics](federated-analytics.md)
+ Ytterligare resurser {#additional-resources}
   + [Versionsinformation](additional-resources/doc-updates.md)

---
audience: end-user
user-guide-title: Adobe Analytics för ljud och video
user-guide-description: Implement Analytics on audio or video sources. Includes the Media SDK and the Media Collection API.
product: adobe analytics
sub-product: medieanalys
translation-type: tm+mt
source-git-commit: cb54b862a0d4a179c499e3a28ab49301121de1bf
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 98%

---


# Adobe Analytics för ljud och video {#using}

+ [Mäta ljud och video i Adobe Analytics](media-overview.md)
+ [Enheter och plattformar som stöds](measurement-options/supported-devices.md)
+ Introduktion till ljud- och videoanalys {#intro-to-ava}
   + [Förutsättningar](intro-to-ava/prereqs.md)
   + Implementeringsvägar {#implementation-paths}
      + [Översikt](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Klientsida](intro-to-ava/implementation-paths/client-side-path.md)
      + Andra implementeringssökvägar {#other-paths}
         + Spårning av milstolpar för mediemodul {#mm-milestone-tracking}
            + [Översikt över milstolpar](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [Migrera milstolpe till Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [Migrera från milstolpe till anpassad länk](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Anpassad länk i Analytics {#cl-in-aa}
            + [Implementeringshandbok för anpassade länkar](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [Aktivera Audience Manager](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [Vanliga frågor om upphörande av stöd för Media Analytics SDK](sdk-implement/end-of-support-faqs.md)
   + [Hämta SDK:er](sdk-implement/download-sdks.md)
   + Installera och konfigurera {#setup}
      + [Översikt](sdk-implement/setup/setup-overview.md)
      + [Konfigurera Android](sdk-implement/setup/set-up-android.md)
      + [Konfigurera iOS](sdk-implement/setup/set-up-ios.md)
      + Konfigurera JavaScript {#setup-javascript}
         + [Konfigurera JavaScript 2.x](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [Konfigurera JavaScript 3.x](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [Konfigurera Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Konfigurera Roku](sdk-implement/setup/set-up-roku.md)
   + Spåra ljud- och videouppspelning {#track-av-playback}
      + [Översikt](sdk-implement/track-av-playback/track-core-overview.md)
      + Spåra grundläggande ljud- och videouppspelning {#track-core}
         + [Spåra grundläggande uppspelning i Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Spåra grundläggande uppspelning i iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + Spåra grundläggande uppspelning i JavaScript {#track-core-javascript}
            + [Spåra grundläggande uppspelning i JavaScript 2.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [Spåra grundläggande uppspelning i JavaScript 3.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Spåra grundläggande uppspelning i Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Spåra grundläggande uppspelning i Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Spåra buffring {#track-buffering}
         + [Spåra buffring i Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Spåra buffring i iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + Spåra buffring i JavaScript {#track-buffering-js}
            + [Spåra buffring i JavaScript 2.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [Spåra buffring i JavaScript 3.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Spåra buffring i Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Spåra buffring i Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Spåra sökning {#track-seeking}
         + [Spåra sökning i Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Spåra sökning i iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + Spåra sökning i JavaScript {#track-seeking-js}
            + [Spåra sökning i JavaScript 2.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [Spåra sökning i JavaScript 3.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Spåra sökning i Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Spåra sökning i Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Implementera standardmetadata {#impl-std-metadata}
         + [Implementera standardmetadata i Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementera standardmetadata i iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS-metadatanycklar](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Implementera standardmetadata i JavaScript {#impl-std-md-js}
            + [Implementera standardmetadata i JavaScript 2.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [Implementera standardmetadata i JavaScript 3.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Implementera standardmetadata i Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Standardmetadataparametrar – Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Implementera standardmetadata i Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Standardmetadataparametrar – Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Spåra annonser {#track-ads}
      + [Översikt](sdk-implement/track-ads/track-ads-overview.md)
      + [Spåra annonser i Android](sdk-implement/track-ads/track-ads-android.md)
      + [Spåra annonser i iOS](sdk-implement/track-ads/track-ads-ios.md)
      + Spåra annonser i JavaScript {#track-ads-js}
         + [Spåra annonser i JavaScript 2.x](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [Spåra annonser i JavaScript 3.x](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [Spåra annonser i Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Spåra annonser i Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Implementera standardmetadata för annonser {#impl-std-ad-metadata}
         + [Implementera standardmetadata för annonser i Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Implementera standardmetadata för annonser i iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + Implementera standardmetadata för annonser i JavaScript {#impl-std-ad-md-js}
            + [Implementera standardmetadata för annonser i JavaScript 2.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [Implementera standardmetadata för annonser i JavaScript 3.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Implementera standardmetadata för annonser i Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Spåra kapitel och segment {#track-chapters}
      + [Översikt](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Spåra kapitel och segment i Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Spåra kapitel och segment i iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + Spåra kapitel och segment i JavaScript {#track-chapters-js}
         + [Spåra kapitel och segment i JavaScript 2.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Spåra kapitel och segment i JavaScript 3.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Spåra kapitel och segment i Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Spåra kapitel och segment i Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Spåra upplevelsekvalitet {#track-qos}
      + [Översikt](sdk-implement/track-qos/track-qos-overview.md)
      + [Spåra upplevelsekvalitet i Android](sdk-implement/track-qos/track-qos-android.md)
      + [Spåra upplevelsekvalitet i iOS](sdk-implement/track-qos/track-qos-ios.md)
      + Spåra upplevelsekvalitet i JavaScript {#track-qos-js}
         + [Spåra upplevelsekvalitet i JavaScript 2.x](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [Spåra upplevelsekvalitet i JavaScript 3.x](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [Spåra upplevelsekvalitet i Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Spåra upplevelsekvalitet i Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Spåra fel {#track-errors}
      + [Översikt](sdk-implement/track-errors/track-errors-overview.md)
      + [Spåra fel i Android](sdk-implement/track-errors/track-errors-android.md)
      + [Spåra fel i iOS](sdk-implement/track-errors/track-errors-ios.md)
      + Spåra fel i JavaScript {#track-errors-js}
         + [Spåra fel i JavaScript 2.x](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [Spåra fel i JavaScript 3.x](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [Spåra fel i Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Spåra fel i Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Avregistrering och sekretess](sdk-implement/opt-out-privacy.md)
   + Spåra scenarier {#tracking-scenarios}
      + [VOD-uppspelning utan annonser](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [VOD-uppspelning med inledande annonser](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [VOD-uppspelning med överhoppade annonser](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [VOD-uppspelning med ett kapitel](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [VOD-uppspelning med ett överhoppat kapitel](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [VOD-uppspelning med sökning i huvudinnehåll](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [VOD-uppspelning med buffring](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Flera parallella VOD-spårare](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [VOD – en spårare för flera sessioner](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
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
   + Analytics i OTT-appar {#analytics-with-ott}
      + [Spåra applägen](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Spåra appåtgärder](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Ange användar-ID](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT och Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT och Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Kokbok {#cookbook}
      + [SDK-kokbok](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [Hantera programavbrott under uppspelning](sdk-implement/cookbook/app-interrupts.md)
      + [Lösa main:play mellan annonser](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Återuppta inaktiva sessioner](sdk-implement/cookbook/resuming-inactive.md)
      + [Spårning i SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Migrering av Media Analytics 1.x till 2.x {#va-1x-to-2x}
      + [Migreringsöversikt](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Kodjämförelse: 1.x till 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [1.x till 2.x API-konvertering](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Migrering från Media Analytics SDK till Launch {#sdk-to-launch}
      + [Migrering från SDK till Launch](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + Plattformsguider för migrering från SDK till Launch {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Medieinsamlings-API (RESTful) {#media-collection-api}
   + [Översikt](media-collection-api/mc-api-overview.md)
   + API-referens {#mc-api-ref}
      + [Sessionsbegäran](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Händelsebegäran](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Parametrar för begäran](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Händelsetyper och beskrivningar](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [JSON-valideringsscheman](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + Implementera API {#mc-api-impl}
      + [Snabbstart](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Ange typ av HTTP-begäran i spelaren](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Hämta ett sessions-ID](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Implementera en händelsebegäran](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Validera en händelsebegäran](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Skicka pinghändelser](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [Skicka QoE-data](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Stöd för anpassade metadata](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Timeoutvillkor](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [Styra händelseförloppet](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Köa händelser när sessioner svarar långsamt](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Tidslinjer för mediespårning {#mc-api-timelines}
      + [Tidslinje 1 – Visa till innehållets slut](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Tidslinje 2 – Användaren avbryter sessionen](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Tidslinje 3 – Kapitel](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ Kokbok {#media-analytics-cookbook}
   + [Kokbok](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Attribution för medieström](media-analytics-cookbook/media-dimensions.md)
+ Mätvärden och metadata {#metrics-and-metadata}
   + [Parametrar för ljud och video](metrics-and-metadata/audio-video-parameters.md)
   + [Annonsparametrar](metrics-and-metadata/ad-parameters.md)
   + [Kapitelparametrar](metrics-and-metadata/chapter-parameters.md)
   + [Parametrar för spelarens tillstånd](metrics-and-metadata/player-state-parameters.md)
   + [Kvalitetsparametrar](metrics-and-metadata/quality-parameters.md)
   + [Segment](metrics-and-metadata/segments.md)
   + [Beräknade mätvärden](metrics-and-metadata/calculated-metrics.md)
+ Rapportering och analys {#media-reports}
   + [Aktivera medierapporter](media-reports/media-reports-enable.md)
   + Standardrapporter för media {#media-default-reports}
      + [Översikt över standardrapporter](media-reports/media-default-reports/default-reports-overview.md)
      + [Medieöversikt](media-reports/media-default-reports/media-reports-overview.md)
      + [Medieinformation](media-reports/media-default-reports/media-reports-detail.md)
      + [Media Daypart-rapport](media-reports/media-default-reports/media-reports-daypart.md)
      + [Rapport över samtidiga visningsprogram för media](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [Hämta JSON-rapportdata för samtidiga medieanvändare](media-reports/media-default-reports/get-concurrent-json20.md)
   + Paneler för mediearbetsyta {#media-workspace-panels}
      + [Panelen för samtidiga medieanvändare](media-reports/media-workspace-panels/media-concurrent-viewers.md)
   + [Mallar för mediearbetsyta](media-reports/media-workspace-templates.md)
   + [Hämta data för samtidiga visningsprogram via API](https://www.adobe.io/apis/experiencecloud/analytics/docs.html)
+ [Spåra nedladdat innehåll](media-collection-api/track-downloaded-content.md)
+ [Federated Analytics](federated-analytics.md)
+ Spårning av spelarens tillstånd {#player-state-tracking}
   + [Översikt](sdk-implement/player-state-tracking/player-state-overview.md)
   + [Standardtillstånd och anpassade tillstånd](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [Implementering och rapportering](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [Exempel på spårning av spelarens tillstånd](sdk-implement/player-state-tracking/player-state-examples.md)
+ Ytterligare resurser {#additional-resources}
   + [Versionsinformation](additional-resources/doc-updates.md)

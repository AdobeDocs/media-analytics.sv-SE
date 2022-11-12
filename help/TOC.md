---
product: adobe analytics
audience: end-user
user-guide-title: Adobe Analytics for Streaming Media
breadcrumb-title: Media Analytics Guide
user-guide-description: Implementera Adobe Analytics för direktuppspelningsmedia. Innehåller Media SDK och Media Collection API.
sub-product: media analytics
source-git-commit: 1d30415b0874c1e0f35045026cb341bab1833d98
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 69%

---


# Adobe Analytics for Streaming Media {#using}

+ [Streaming Media Analytics Guide](media-overview.md)
+ Versionsinformation {#release-notes}
   + [Versionsinformation för direktuppspelande media](additional-resources/release-notes.md)
+ Komma igång {#getting-started}
   + [Översikt](getting-started/getting-started.md)
   + [SDK, Libraries och Extensions](getting-started/download-sdks.md)
   + [Enheter som stöds](getting-started/supported-devices.md)
   + [Förutsättningar](getting-started/prereqs.md)
   + [Supportslut](additional-resources/end-of-support-faqs.md)
   + [Dokumentation för direktuppspelande media](getting-started/implementation-documentation.md)
+ Implementering {#implementation}
   + [Implementeringsöversikt](implementation/overview.md)
   + Media SDKs - implementering {#media-sdk}
      + [Översikt över Media SDK](implementation/media-sdk/media-sdk-overview.md)
      + Installera och konfigurera {#setup}
         + [Installera web SDK:er](implementation/media-sdk/setup/web-implementation.md)
         + [Installera mobil-SDK](implementation/media-sdk/setup/mobile-implementation.md)
         + Installera OTT SDK:er {#ott-setup}
            + [Installera Chromecast SDK](implementation/media-sdk/setup/set-up-chromecast.md)
            + [Installera Roku SDK](implementation/media-sdk/setup/set-up-roku.md)
   + Media Collection APIs - implementering {#streaming-media-apis}
      + [Media Collection](implementation/media-collection-api/mc-api-overview.md)
      + [API - snabbstart](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Sessionsbegäran](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Händelsebegäran](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Parametrar för begäran](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Händelsetyper och beskrivningar](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
      + Implementera API {#mc-api-impl}
         + [Ange typ av HTTP-begäran i spelaren](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
         + [Hämta ett sessions-ID](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
         + [Implementera en händelsebegäran](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
         + [JSON-valideringsscheman](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
         + [Validera en händelsebegäran](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
         + [Skicka pinghändelser](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
         + [Skicka QoE-data](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
         + [Stöd för anpassade metadata](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
         + [Timeoutvillkor](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
         + [Styra händelseförloppet](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
         + [Köa händelser när sessioner svarar långsamt](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Variabler {#variables}
      + [Parametrar för direktuppspelande media](implementation/variables/audio-video-parameters.md)
      + [Annonsparametrar](implementation/variables/ad-parameters.md)
      + [Kapitelparametrar](implementation/variables/chapter-parameters.md)
      + [Parametrar för spelarens tillstånd](implementation/variables/player-state-parameters.md)
      + [Kvalitetsparametrar](implementation/variables/quality-parameters.md)
      + [Beräknade mätvärden](implementation/variables/calculated-metrics.md)
+ Spårning {#track-av-playback}
   + [Översikt](use-cases/track-av-playback/track-core-overview.md)
   + Spåra direktuppspelning av media {#track-core}
      + [Spåra grundläggande uppspelning i Android](use-cases/track-av-playback/track-core/track-core-android.md)
      + [Spåra grundläggande uppspelning i iOS](use-cases/track-av-playback/track-core/track-core-ios.md)
      + Spåra grundläggande uppspelning i JavaScript {#track-core-javascript}
         + [Spåra grundläggande uppspelning i JavaScript 2.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [Spåra grundläggande uppspelning i JavaScript 3.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
      + [Spåra grundläggande uppspelning i Chromecast](use-cases/track-av-playback/track-core/track-core-chromecast.md)
      + [Spåra grundläggande uppspelning i Roku](use-cases/track-av-playback/track-core/track-core-roku.md)
   + Spåra buffring {#track-buffering}
      + [Spåra buffring i Android](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
      + [Spåra buffring i iOS](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
      + Spåra buffring i JavaScript {#track-buffering-js}
         + [Spåra buffring i JavaScript 2.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [Spåra buffring i JavaScript 3.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
      + [Spåra buffring i Chromecast](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
      + [Spåra buffring i Roku](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
   + Spåra sökning {#track-seeking}
      + [Spåra sökning i Android](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
      + [Spåra sökning i iOS](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
      + Spåra sökning i JavaScript {#track-seeking-js}
         + [Spåra sökning i JavaScript 2.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [Spåra sökning i JavaScript 3.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
      + [Spåra sökning i Chromecast](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
      + [Spåra sökning i Roku](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
   + Implementera standardmetadata {#impl-std-metadata}
      + [Implementera standardmetadata i Android](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
      + [Implementera standardmetadata i iOS](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      + [iOS-metadatanycklar](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
      + Implementera standardmetadata i JavaScript {#impl-std-md-js}
         + [Implementera standardmetadata i JavaScript 2.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
         + [Implementera standardmetadata i JavaScript 3.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
      + [Implementera standardmetadata i Chromecast](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
      + [Standardmetadataparametrar – Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
      + [Implementera standardmetadata i Roku](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
      + [Standardmetadataparametrar – Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Spåra annonser {#track-ads}
      + [Översikt](use-cases/track-ads/track-ads-overview.md)
      + [Spåra annonser i Android](use-cases/track-ads/track-ads-android.md)
      + [Spåra annonser i iOS](use-cases/track-ads/track-ads-ios.md)
      + Spåra annonser i JavaScript {#track-ads-js}
         + [Spåra annonser i JavaScript 2.x](use-cases/track-ads/track-ads-js/track-ads-js.md)
         + [Spåra annonser i JavaScript 3.x](use-cases/track-ads/track-ads-js/track-ads-js3.md)
      + [Spåra annonser i Chromecast](use-cases/track-ads/track-ads-chromecast.md)
      + [Spåra annonser i Roku](use-cases/track-ads/track-ads-roku.md)
      + Implementera standardmetadata för annonser {#impl-std-ad-metadata}
         + [Implementera standardmetadata för annonser i Android](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Implementera standardmetadata för annonser i iOS](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + Implementera standardmetadata för annonser i JavaScript {#impl-std-ad-md-js}
            + [Implementera standardmetadata för annonser i JavaScript 2.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [Implementera standardmetadata för annonser i JavaScript 3.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Implementera standardmetadata för annonser i Roku](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Spåra kapitel och segment {#track-chapters}
      + [Översikt](use-cases/track-chapters/track-chapters-overview.md)
      + [Spåra kapitel och segment i Android](use-cases/track-chapters/track-chapters-android.md)
      + [Spåra kapitel och segment i iOS](use-cases/track-chapters/track-chapters-ios.md)
      + Spåra kapitel och segment i JavaScript {#track-chapters-js}
         + [Spåra kapitel och segment i JavaScript 2.x](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Spåra kapitel och segment i JavaScript 3.x](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Spåra kapitel och segment i Chromecast](use-cases/track-chapters/track-chapters-chromecast.md)
      + [Spåra kapitel och segment i Roku](use-cases/track-chapters/track-chapters-roku.md)
   + Spåra upplevelsekvalitet {#track-qos}
      + [Översikt](use-cases/track-qos/track-qos-overview.md)
      + [Spåra upplevelsekvalitet i Android](use-cases/track-qos/track-qos-android.md)
      + [Spåra upplevelsekvalitet i iOS](use-cases/track-qos/track-qos-ios.md)
      + Spåra upplevelsekvalitet i JavaScript {#track-qos-js}
         + [Spåra upplevelsekvalitet i JavaScript 2.x](use-cases/track-qos/track-qos-js/track-qos-js.md)
         + [Spåra upplevelsekvalitet i JavaScript 3.x](use-cases/track-qos/track-qos-js/track-qos-js3.md)
      + [Spåra upplevelsekvalitet i Chromecast](use-cases/track-qos/track-qos-chromecast.md)
      + [Spåra upplevelsekvalitet i Roku](use-cases/track-qos/track-qos-roku.md)
   + Spåra fel {#track-errors}
      + [Översikt](use-cases/track-errors/track-errors-overview.md)
      + [Spåra fel i Android](use-cases/track-errors/track-errors-android.md)
      + [Spåra fel i iOS](use-cases/track-errors/track-errors-ios.md)
      + Spåra fel i JavaScript {#track-errors-js}
         + [Spåra fel i JavaScript 2.x](use-cases/track-errors/track-errors-js/track-errors-js.md)
         + [Spåra fel i JavaScript 3.x](use-cases/track-errors/track-errors-js/track-errors-js3.md)
      + [Spåra fel i Chromecast](use-cases/track-errors/track-errors-chromecast.md)
      + [Spåra fel i Roku](use-cases/track-errors/track-errors-roku.md)
   + Spåra scenarier {#tracking-scenarios}
      + [VOD-uppspelning utan annonser](use-cases/tracking-scenarios/vod-no-intrs-details.md)
      + [VOD-uppspelning med inledande annonser](use-cases/tracking-scenarios/vod-preroll-ads.md)
      + [VOD-uppspelning med överhoppade annonser](use-cases/tracking-scenarios/vod-skipped-ads.md)
      + [VOD-uppspelning med ett kapitel](use-cases/tracking-scenarios/vod-one-chapter.md)
      + [VOD-uppspelning med ett överhoppat kapitel](use-cases/tracking-scenarios/vod-skipped-chapter.md)
      + [VOD-uppspelning med sökning i huvudinnehåll](use-cases/tracking-scenarios/vod-seeking.md)
      + [VOD-uppspelning med buffring](use-cases/tracking-scenarios/vod-buffering.md)
      + [Flera parallella VOD-spårare](use-cases/tracking-scenarios/vod-multi-trackers.md)
      + [VOD – en spårare för flera sessioner](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
      + [Live-huvudinnehåll](use-cases/tracking-scenarios/live-main-content.md)
      + [Live-huvudinnehåll med sekventiell spårning](use-cases/tracking-scenarios/live-sequential.md)
+ Rapportering {#media-reports}
   + [Aktivera medierapporter](reporting/media-reports-enable.md)
   + [Om segment](reporting/segments.md)
   + Standardrapporter för media {#media-default-reports}
      + [Översikt över standardrapporter](reporting/reports-and-analytics/default-reports-overview.md)
      + [Medieöversikt](reporting/reports-and-analytics/media-reports-overview.md)
      + [Medieinformation](reporting/reports-and-analytics/media-reports-detail.md)
      + [Media Daypart-rapport](reporting/reports-and-analytics/media-reports-daypart.md)
      + [Rapport över samtidiga visningsprogram för media](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + Paneler för mediearbetsyta {#media-workspace-panels}
      + [Panelen Mediegenomsnitt för miniatyrmålgrupp](reporting/workspace/average-minute-audience.md)
      + [Panelen för samtidiga medieanvändare](reporting/workspace/media-concurrent-viewers-overview.md)
      + [Medieuppspelningstid spenderad panel](reporting/workspace/media-playback-time-spent.md)
   + [Mallar för mediearbetsyta](reporting/workspace/media-workspace-templates.md)
   + [Hämta data för samtidiga visningsprogram via API](reporting/reports-and-analytics/get-concurrent-json20.md)
   + [Hämta mediespelningstid för spenderade data via API](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ Användningsexempel {#media-use-cases}
   + Spårning av spelarens tillstånd {#player-state-tracking}
      + [Översikt](use-cases/player-state-tracking/player-state-overview.md)
      + [Standardtillstånd och anpassade tillstånd](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [Implementering och rapportering](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [Spårning av flera spelarlägen](use-cases/player-state-tracking/multiple-player-states.md)
      + [Exempel på spårning av spelarens tillstånd](use-cases/player-state-tracking/player-state-examples.md)
   + [Spåra nedladdat innehåll offline](use-cases/track-downloaded-content.md)
   + [Federated Analytics](use-cases/federated-analytics.md)
   + [Hantera programavbrott under uppspelning](use-cases/cookbook/app-interrupts.md)
   + [Översikt över äldre SDK-kokbok](use-cases/cookbook/sdk-cookbook-overview.md)
   + [Äldre - Media Analytics Cookbook](use-cases/media-analytics-cookbook/media-analytics-cookbook.md)
   + [Attribution för medieström](use-cases/media-analytics-cookbook/media-dimensions.md)
   + [Återuppta inaktiva sessioner](use-cases/cookbook/resuming-inactive.md)
   + [Roku-spårning i SceneGraph](use-cases/cookbook/sdk-track-scenegraph.md)
   + [Hantera mellanrum mellan annonser](use-cases/cookbook/fix-ad-play-ad.md)
   + Tidslinjer {#timelines}
      + [Kapitelstart och -slut](use-cases/timelines/chapter-start-end.md)
      + [Visa till innehållsslut](use-cases/timelines/view-to-end-of-content.md)
      + [Avbrottssession](use-cases/timelines/user-abandons-session.md)
   + Använd analyser i OTT-appar {#analytics-with-ott}
      + [Spåra applägen](use-cases/analytics-with-ott/track-app-states.md)
      + [Spåra appåtgärder](use-cases/analytics-with-ott/track-app-actions.md)
      + [Ange användar-ID](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT och Audience Manager](use-cases/analytics-with-ott/ott-am.md)
      + [OTT och Experience Cloud](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ Integritet och säkerhet {#streaming-media-privacy}
   + [Inställningar för avanmälan och sekretess](privacy/opt-out-privacy.md)
   + [Säkerhet](privacy/security.md)
+ Äldre implementeringar {#legacy-implementations}
   + [Äldre - översikt](legacy/setup/legacy-setup-overview.md)
   + [Äldre - Ladda ned SDK:er](legacy/legacy-download-sdks.md)
   + Äldre - Media SDKs {#legacy-media-sdks}
      + [Äldre - Översikt över Media SDK](legacy/media-sdk/setup/setup-overview.md)
      + [Konfigurera Android](legacy/media-sdk/setup/set-up-android.md)
      + [Konfigurera iOS](legacy/media-sdk/setup/set-up-ios.md)
      + Konfigurera JavaScript {#setup-javascript}
         + [Konfigurera JavaScript 3.x](legacy/media-sdk/setup/setup-javascript/set-up-js-3.md)
   + Äldre - Media SDK för att starta migrering {#sdk-to-launch}
      + [Översikt](legacy/sdk-to-launch/sdk-to-launch-migration.md)
      + [Android - Media SDK to Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
      + [iOS - Media SDK to Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
      + [JavaScript - Media SDK to Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
   + [Om mätning av pulsslag](legacy/heartbeat-measurement.md)
   + [Adobe Primetime och Streaming Media Analytics](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Adobe Audience Management Enabled](legacy/intro-to-ava/am-enablement.md)
   + [Implementering av anpassad länk](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + Spårning av äldre milstolpe {#legacy-milestone-tracking}
      + [Spårning av äldre milstolpe](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrera milstolpe till VA](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migrera milstolpe till CL](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Validering {#validation}
      + [Valideringsöversikt](legacy/validation/validation-overview.md)
      + [Test 1: Standarduppspelning](legacy/validation/test1-standard-playback.md)
      + [Test 2: Medieavbrott](legacy/validation/test2-media-interrupt.md)
      + [Information om provsamtal](legacy/validation/test-call-details.md)
      + [Beskrivning av parametern Heartbeat](legacy/validation/heartbeat-params.md)
      + Felsökning {#debugging}
         + [SDK-felsökning](legacy/validation/debugging/sdk-debugging.md)
   + [Äldre migrering: VHL 1.x till VHL 2.x](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [Konfigurera JavaScript 2.x](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [Kodjämförelse v1.x till v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [Spårnings-API:er 1x till 2x](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [Äldre - Introduktion till AVA](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [Klientsidans sökväg](legacy/intro-to-ava/implementation-paths/client-side-path.md)

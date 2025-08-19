---
product: adobe analytics
audience: end-user
user-guide-title: Guide för direktuppspelande medietjänster
breadcrumb-title: Guide för direktuppspelande medietjänster
user-guide-description: Implementera tjänster för direktuppspelning av media. Innehåller Media SDK och Media Collection API.
sub-product: media analytics
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 3%

---


# Guide för direktuppspelande medietjänster {#using}

+ [Guide för Adobe direktuppspelande medietjänster](media-overview.md)
+ Versionsinformation {#release-notes}
   + [Versionsinformation för direktuppspelande medietjänster](additional-resources/release-notes.md)
+ Kom igång {#getting-started}
   + [Förutsättningar](getting-started/prereqs.md)
   + [Enheter som stöds](getting-started/supported-devices.md)
   + [Implementeringsdokumentation för direktuppspelande medietjänster](getting-started/implementation-documentation.md)
   + [SDK:er, bibliotek och tillägg](getting-started/download-sdks.md)
   + Supportslut {#end-of-support}
      + [Media Analytics Mobile SDK End of Support](additional-resources/end-of-support-faqs.md)
      + Äldre - Fristående media-SDK för att starta migrering {#sdk-to-launch}
         + [Översikt](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android - Media SDK to Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS - Media SDK to Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript - Media SDK to Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Implementering {#implementation}
   + [Implementeringsöversikt](implementation/overview.md)
   + Edge-implementeringar (rekommenderas) {#edge-recommended}
      + [Förutsättningar](/help/implementation/edge/prerequisites-edge.md)
      + Media Edge SDKs/Extension {#media-edge-sdk}
         + [Media Edge SDK:er/installationsprogram för tillägg](/help/implementation/edge/implementation-edge.md)
         + [Media Edge Web SDK](/help/implementation/edge/edge-web-sdk.md)
         + [Media Edge Mobile SDK](/help/implementation/edge/edge-mobile-sdk.md)
      + [Media Edge API](/help/implementation/edge/implementation-edge-api.md)
   + Implementeringar endast för Adobe Analytics {#analytics-only}
      + [Förutsättningar](/help/implementation/media-sdk/setup/prerequisites-analytics.md)
      + Media SDK:er/tillägg {#media-sdk}
         + [JavaScript Web SDK](implementation/media-sdk/setup/web-implementation.md)
         + [Media Analytics-tillägg](implementation/media-sdk/setup/web-implementation-tags.md)
         + [SDK för mobiler](implementation/media-sdk/setup/mobile-implementation.md)
         + OTT SDKs {#ott-setup}
            + [Installera Chromecast SDK](implementation/media-sdk/setup/set-up-chromecast.md)
            + [Installera Roku SDK](implementation/media-sdk/setup/set-up-roku.md)
      + Media Collection APIs - implementering {#streaming-media-apis}
         + [Media Collection](implementation/media-collection-api/mc-api-overview.md)
         + [API - snabbstart](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
         + [Sessionsbegäran](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
         + [Händelsebegäran](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
         + [Begärandeparametrar](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
         + [Händelsetyper och beskrivningar](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
         + Implementera API {#mc-api-impl}
            + [Ange HTTP-begärandetyp i spelaren](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
            + [Hämta ett sessions-ID](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
            + [Implementera en händelsebegäran](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
            + [JSON-valideringsscheman](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
            + [Validerar händelsebegäranden](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
            + [Skicka Ping-händelser](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
            + [Skicka QoE-data](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
            + [Stöd för anpassade metadata](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
            + [Timeout-villkor](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
            + [Kontrollera händelseordningen](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
            + [Köa händelser när sessionssvar är långsamma](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Variabler {#variables}
      + [Parametrar för direktuppspelande media](implementation/variables/audio-video-parameters.md)
      + [Annonsparametrar](implementation/variables/ad-parameters.md)
      + [Kapitelparametrar](implementation/variables/chapter-parameters.md)
      + [Parametrar för spelartillstånd](implementation/variables/player-state-parameters.md)
      + [Kvalitetsparametrar](implementation/variables/quality-parameters.md)
      + [Beräknade mätvärden](implementation/variables/calculated-metrics.md)
+ Rapportering {#media-reports}
   + [Aktivera medierapporter](reporting/media-reports-enable.md)
   + Mediepaneler i Workspace {#media-workspace-panels}
      + [Panelen Mediegenomsnitt för miniatyrmålgrupp](reporting/workspace/average-minute-audience.md)
      + [Media Concurrent Viewers panel](reporting/workspace/media-concurrent-viewers-overview.md)
      + [Medieuppspelningstid spenderad panel](reporting/workspace/media-playback-time-spent.md)
   + [Medierapporter i Workspace](reporting/workspace/media-workspace-templates.md)
   + [Mediesegment](reporting/segments.md)
   + Standardmedierapporter {#media-default-reports}
      + [Översikt över standardrapporter](reporting/reports-and-analytics/default-reports-overview.md)
      + [Medieöversikt](reporting/reports-and-analytics/media-reports-overview.md)
      + [Medieinformation](reporting/reports-and-analytics/media-reports-detail.md)
      + [Media DayPart-rapport](reporting/reports-and-analytics/media-reports-daypart.md)
      + [Rapport över visningsprogram för parallella medier](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + Media-API {#media-api}
      + [Hämta data från samtidiga visningsprogram](reporting/reports-and-analytics/get-concurrent-json20.md)
      + [Hämta tid för mediauppspelning för spenderade data](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ Användningsfall {#media-use-cases}
   + [Användningsexempel för Media SDK](use-cases/cookbook/sdk-cookbook-overview.md)
   + Spårning av spelartillstånd {#player-state-tracking}
      + [Översikt](use-cases/player-state-tracking/player-state-overview.md)
      + [Standard och anpassade lägen](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [Implementering och rapportering](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [Spårning av flera spelarlägen](use-cases/player-state-tracking/multiple-player-states.md)
      + [Exempel på spårning av spelartillstånd](use-cases/player-state-tracking/player-state-examples.md)
   + [Spåra hämtat innehåll](use-cases/track-downloaded-content.md)
   + [Federated Media](use-cases/federated-media.md)
   + [Hantera programavbrott under uppspelning](use-cases/cookbook/app-interrupts.md)
   + [Attribut för medieström](use-cases/media-analytics-cookbook/media-dimensions.md)
   + Migrera XDM-fält för Analytics-källkoppling {#xdm-updates}
      + [Uppdatera källanslutning till nya XDM Streaming Media-fält](/help/use-cases/xdm-updates/updated-xdm-fields.md)
      + [Migrera målgrupper](/help/use-cases/xdm-updates/migrate-audiences.md)
      + [Migrera CJA-konfiguration](/help/use-cases/xdm-updates/migrate-cja-setup.md)
      + [Förbered data för migrering](/help/use-cases/xdm-updates/migrate-dataprep.md)
      + [Migrera profiler](/help/use-cases/xdm-updates/migrate-profiles.md)
      + [Mappning av mediaparametrar](/help/use-cases/xdm-updates/parameters-mapping.md)
   + [Återuppta inaktiva sessioner](use-cases/cookbook/resuming-inactive.md)
   + [Roku-spårning i SceneGraph](use-cases/cookbook/sdk-track-scenegraph.md)
   + [Hantera mellanrum mellan annonser](use-cases/cookbook/fix-ad-play-ad.md)
   + Tidslinjer {#timelines}
      + [Kapitelstart och -slut](use-cases/timelines/chapter-start-end.md)
      + [Visa till innehållsslut](use-cases/timelines/view-to-end-of-content.md)
      + [Avbrottssession](use-cases/timelines/user-abandons-session.md)
   + Använd analyser i OTT-appar {#analytics-with-ott}
      + [Spåra applägen](use-cases/analytics-with-ott/track-app-states.md)
      + [Spåra programåtgärder](use-cases/analytics-with-ott/track-app-actions.md)
      + [Ange användar-ID](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT och Audience Manager](use-cases/analytics-with-ott/ott-am.md)
      + [OTT och Experience Cloud](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ Spårning {#tracking}
   + [Översikt](use-cases/track-av-playback/track-core-overview.md)
   + Spåra direktuppspelning av media {#track-core}
      + [Spåra kärnuppspelning på JavaScript 3.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
      + [Spåra kärnuppspelning på Chromecast](use-cases/track-av-playback/track-core/track-core-chromecast.md)
      + [Spåra kärnuppspelning på Roku](use-cases/track-av-playback/track-core/track-core-roku.md)
   + Track Buffering {#track-buffering}
      + [Track Buffering på JavaScript 3.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
      + [Track Buffering on Chromecast](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
      + [Track Buffering på Roku](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
   + Spåra sökning {#track-seeking}
      + [Spåra sökning på JavaScript 3.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
      + [Spåra sökning på Chromecast](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
      + [Spåra sökning på Roku](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
   + Implementera standardmetadata {#impl-std-metadata}
      + [Implementera standardmetadata i JavaScript 3.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
      + [Implementera standardmetadata på Chromecast](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
      + [Standardmetadataparametrar - kromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
      + [Implementera standardmetadata på Roku](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
      + [Standardmetadataparametrar - Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Spåra annonser {#track-ads}
      + [Översikt](use-cases/track-ads/track-ads-overview.md)
      + [Spåra annonser på JavaScript 3.x](use-cases/track-ads/track-ads-js/track-ads-js3.md)
      + [Spåra annonser på Chromecast](use-cases/track-ads/track-ads-chromecast.md)
      + [Spåra annonser på Roku](use-cases/track-ads/track-ads-roku.md)
      + Implementera standard och metadata {#impl-std-ad-metadata}
         + [Lägg in standardmetadata i JavaScript 3.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Implementera standardannonsmetadata på Roku](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Spåra kapitel och segment {#track-chapters}
      + [Översikt](use-cases/track-chapters/track-chapters-overview.md)
      + [Spåra kapitel och segment i JavaScript 3.x](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Spåra kapitel och segment i Chromecast](use-cases/track-chapters/track-chapters-chromecast.md)
      + [Spåra kapitel och segment på Roku](use-cases/track-chapters/track-chapters-roku.md)
   + Spåra upplevelsekvalitet {#track-qos}
      + [Översikt](use-cases/track-qos/track-qos-overview.md)
      + [Spåra upplevelsekvalitet på JavaScript 3.x](use-cases/track-qos/track-qos-js/track-qos-js3.md)
      + [Spåra upplevelsekvalitet på Chromecast](use-cases/track-qos/track-qos-chromecast.md)
      + [Spåra upplevelsekvalitet på Roku](use-cases/track-qos/track-qos-roku.md)
   + Spåra fel {#track-errors}
      + [Översikt](use-cases/track-errors/track-errors-overview.md)
      + [Spåra fel i JavaScript 3.x](use-cases/track-errors/track-errors-js/track-errors-js3.md)
      + [Spåra fel i Chromecast](use-cases/track-errors/track-errors-chromecast.md)
      + [Spåra fel på Roku](use-cases/track-errors/track-errors-roku.md)
+ Integritet och säkerhet {#streaming-media-privacy}
   + [Inställningar för avanmälan och sekretess](privacy/opt-out-privacy.md)
   + [Säkerhet](privacy/security.md)
+ Äldre implementeringar {#legacy-implementations}
   + [Äldre - översikt](legacy/setup/legacy-setup-overview.md)
   + [Äldre - Ladda ned SDK:er](legacy/legacy-download-sdks.md)
   + Äldre - Media SDKs {#legacy-media-sdks}
      + [Äldre - Media SDK - översikt](legacy/media-sdk/setup/setup-overview.md)
      + [Konfigurera Android](legacy/media-sdk/setup/set-up-android.md)
      + [Konfigurera iOS](legacy/media-sdk/setup/set-up-ios.md)
      + Konfigurera JavaScript {#setup-javascript}
         + [Konfigurera JavaScript 2.x](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [Om mätning av pulsslag](legacy/heartbeat-measurement.md)
   + [Adobe Primetime](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Aktivera Adobe Audience Management](legacy/intro-to-ava/am-enablement.md)
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
         + [SDK Debugging](legacy/validation/debugging/sdk-debugging.md)
   + [Äldre migrering: VHL 1.x till VHL 2.x](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [Kodjämförelse v1.x till v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [Spårnings-API:er 1x till 2x](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [Äldre - Introduktion till AVA](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [Klientsidans sökväg](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + Äldre spårning {#track-av-playback}
      + [Spåra kärnuppspelning på Android](use-cases/track-av-playback/track-core/track-core-android.md)
      + [Spåra kärnuppspelning på iOS](use-cases/track-av-playback/track-core/track-core-ios.md)
      + Spåra kärnuppspelning på JavaScript {#track-core-javascript}
         + [Spåra kärnuppspelning på JavaScript 2.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [Track Buffering på Android](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
         + [Track Buffering på iOS](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
         + Track Buffering på JavaScript {#track-buffering-js}
            + [Track Buffering på JavaScript 2.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [Spåra sökning på Android](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
         + [Spåra sökning på iOS](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
         + Spåra sökning på JavaScript {#track-seeking-js}
            + [Spåra sökning på JavaScript 2.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [Implementera standardmetadata på Android](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementera standardmetadata på iOS](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS-metadatanycklar](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Implementera standardmetadata på JavaScript {#impl-std-md-js}
            + [Implementera standardmetadata i JavaScript 2.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + Spåra annonser {#track-ads}
         + [Spåra annonser på Android](use-cases/track-ads/track-ads-android.md)
         + [Spåra annonser på iOS](use-cases/track-ads/track-ads-ios.md)
         + Spåra annonser på JavaScript {#track-ads-js}
            + [Spåra annonser på JavaScript 2.x](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [Implementera standardannonsmetadata på Android](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [Implementera standardannonsmetadata på iOS](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + Implementera standardvärden och metadata på JavaScript {#impl-std-ad-md-js}
               + [Lägg in standardmetadata i JavaScript 2.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + Spåra kapitel och segment {#track-chapters}
         + [Spåra kapitel och segment på Android](use-cases/track-chapters/track-chapters-android.md)
         + [Spåra kapitel och segment på iOS](use-cases/track-chapters/track-chapters-ios.md)
         + Spåra kapitel och segment på JavaScript {#track-chapters-js}
            + [Spåra kapitel och segment i JavaScript 2.x](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Spåra upplevelsekvalitet på Android](use-cases/track-qos/track-qos-android.md)
         + [Spåra upplevelsekvalitet på iOS](use-cases/track-qos/track-qos-ios.md)
         + Spåra upplevelsekvalitet på JavaScript {#track-qos-js}
            + [Spåra upplevelsekvalitet på JavaScript 2.x](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + Spåra fel {#track-errors}
         + [Spåra fel i Android](use-cases/track-errors/track-errors-android.md)
         + [Spåra fel i iOS](use-cases/track-errors/track-errors-ios.md)
         + Spåra fel i JavaScript {#track-errors-js}
            + [Spåra fel i JavaScript 2.x](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + Spåra scenarier {#tracking-scenarios}
         + [VOD utan annonser](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [Uppspelning av VOD med förrollningsannonser](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [VOD-uppspelning med överhoppade annonser](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [VOD uppspelning med ett kapitel](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [VOD-uppspelning med ett överhoppat kapitel](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [VOD uppspelning med sökning i huvudinnehållet](use-cases/tracking-scenarios/vod-seeking.md)
         + [VOD-uppspelning med buffring](use-cases/tracking-scenarios/vod-buffering.md)
         + [VOD flera spårare parallellt](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [VOD en spårningsfunktion för flera sessioner](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [Live-huvudinnehåll](use-cases/tracking-scenarios/live-main-content.md)
         + [Live-huvudinnehåll med sekventiell spårning](use-cases/tracking-scenarios/live-sequential.md)

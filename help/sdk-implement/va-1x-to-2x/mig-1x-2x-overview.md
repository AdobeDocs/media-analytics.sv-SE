---
title: Migreringsöversikt
description: Lär dig hur du migrerar från 1.x till 2.x-versioner av Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 8%

---

# Migreringsöversikt{#migration-overview}

Migreringen från VHL 1.x till VHL 2.x är enkel, med den nya versionen med förenklade API:er för initiering, konfiguration och spelardelegater.

Här är de primära skillnaderna mellan 1.x och 2.x:

* **Plugins, delegater -** Du behöver inte längre implementera plugin-program och delegater för Analytics, VideoPlayer och Heartbeat.
* **Konfiguration -** Du behöver inte längre instansiera konfigurationer för 1.x-plugin-program.

## Fördelar med 2.x {#benefits-of-two-x}

* Alla publika metoder konsolideras i klassen `MediaHeartbeat` för att underlätta implementeringen för utvecklare.
* Alla konfigurationer konsolideras nu i klassen `MediaHeartbeatConfig`.
* Du behöver inte längre instansiera konfigurationer för plugin-programmen Analytics, VideoPlayer och Heartbeat. Du behöver bara instansiera klassen `MediaHeartbeat` med instanserna `MediaHeartbeatDelegate` och `MediaHeartbeatConfig`. Detta är den enda implementering som krävs för att initiera Media Analytics.

   Med initieringen av `MediaHeartbeat` kan du ta bort all implementering för Analytics-plugin, VideoPlayer-plugin och Heartbeat-plugin. Ta även bort all befintlig implementering för initiering som tar in en array med plugin-program som indata. Jämförelser sida vid sida av implementeringarna av 1.x och 2.x visas här: [Kodjämförelse: 1.x till 2.x.](./code-comparison-1x-2x.md)

De nya API:erna i 2.x beskrivs närmare här: [Konvertering av API 1.x till 2.x.](./1x-2x-api-change.md)

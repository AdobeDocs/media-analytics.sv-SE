---
title: Migreringsöversikt
description: Lär dig hur du migrerar från 1.x till 2.x-versioner av Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 7%

---

# Överblick över äldre versioner av VHL 1.x till VHL 2.x {#migration-overview}

Migreringen från VHL 1.x till VHL 2.x är enkel, med den nya versionen med förenklade API:er för initiering, konfiguration och delegering av spelare.i

Här är de primära skillnaderna mellan 1.x och 2.x:

* **Plugins, ombud -** Du behöver inte längre implementera plugin-program och delegater för Analytics, VideoPlayer och Heartbeat.
* **Konfiguration -** Du behöver inte längre instansiera konfigurationer för 1.x-plugin-program.

## Fördelar med 2.x {#benefits-of-two-x}

* Alla offentliga metoder samlas i `MediaHeartbeat` för att underlätta implementeringen för utvecklare.
* Alla konfigurationer konsolideras nu i `MediaHeartbeatConfig` klassen.
* Du behöver inte längre instansiera konfigurationer för plugin-programmen Analytics, VideoPlayer och Heartbeat. Du behöver bara skapa en instans av `MediaHeartbeat` klass med `MediaHeartbeatDelegate` och `MediaHeartbeatConfig` -instanser. Detta är den enda implementering som krävs för att initiera Media Analytics.

   Med initieringen av `MediaHeartbeat`kan du ta bort all implementering för Analytics Plugin, VideoPlayer Plugin och Heartbeat Plugin. Ta även bort all befintlig implementering för initiering som tar in en array med plugin-program som indata. Jämförelser sida vid sida av implementeringarna av 1.x och 2.x visas här: [Kodjämförelse: 1.x till 2.x](./code-comparison-1x-2x.md)

De nya API:erna i 2.x beskrivs närmare här: [Konvertering av API 1.x till 2.x.](./1x-2x-api-change.md)

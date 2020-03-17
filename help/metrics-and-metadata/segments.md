---
title: Segment
description: null
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Segment{#segments}

>[!NOTE]
>
>Dessa rapporteringssegment som är kopplade till Media Stream Type introducerades den 13 mars 2018 tillsammans med `streamType` parametern.

| Segment | Beskrivning | Regel |
|---|---|---|
| Medieströmtyp: Alla | Segmentera alla *medieströmdata* | &quot;Innehåll (ID) finns&quot; |
| Medieströmtyp: Ljud | Segmentera alla *ljudströmsdata* | &quot;Innehåll (ID) finns&quot; AND &quot;Media Stream Type = `audio`&quot; |
| Medieströmtyp: Video | Segmentera alla *videoströmdata* | &quot;Innehåll (ID) finns&quot; AND &quot;Media Stream Type != `audio`&quot; |
| Medieinnehållstyp: VoD | Segmentera allt VoD-innehåll | &quot;Innehållstyp = `vod`&quot; |
| Medieinnehållstyp: Live | Segmentera allt Live-innehåll | &quot;Innehållstyp = `live`&quot; |
| Medieinnehållstyp: Linjär | Segmentera allt linjärt innehåll | &quot;Innehållstyp = `linear`&quot; |
| Medieinnehållstyp: Podcast | Segmentera allt innehåll i poddsändning | &quot;Innehållstyp = `podcast`&quot; |
| Medieinnehållstyp: Ljudbok | Segmentera allt innehåll i ljudboken | &quot;Innehållstyp = `audiobook`&quot; |
| Medieinnehållstyp: AoD | Segmentera allt AoD-innehåll | &quot;Innehållstyp = `aod`&quot; |


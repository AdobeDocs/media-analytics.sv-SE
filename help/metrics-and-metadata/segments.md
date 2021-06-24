---
title: Segment
description: '"Lär dig mer om de rapporteringssegment som är associerade med mediaströmstyp, inklusive segment, beskrivning och regel för mediaströmstyp."'
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: '"Medieanalys, segmentering"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 10%

---

# Segment{#segments}

>[!NOTE]
>
>Dessa rapporteringssegment som är associerade med mediaströmstyp introducerades den 18 mars 18 tillsammans med parametern `streamType`.

| Segment | Beskrivning | Regel |
|---|---|---|
| Medieströmtyp: Alla | Segmentera alla *media* strömdata | &quot;Innehåll (ID) finns&quot; |
| Medieströmtyp: Ljud | Segmentera alla *ljudströmdata* | &quot;Innehåll (ID) finns&quot; AND &quot;Media Stream Type = `audio`&quot; |
| Medieströmtyp: Video | Segmentera alla *video* strömdata | &quot;Innehåll (ID) finns&quot; AND &quot;Media Stream Type != `audio`&quot; |
| Medieinnehållstyp: VoD | Segmentera allt VoD-innehåll | &quot;Innehållstyp = `vod`&quot; |
| Medieinnehållstyp: Live | Segmentera allt Live-innehåll | &quot;Innehållstyp = `live`&quot; |
| Medieinnehållstyp: Linjär | Segmentera allt linjärt innehåll | &quot;Innehållstyp = `linear`&quot; |
| Medieinnehållstyp: Podcast | Segmentera allt innehåll i poddsändning | &quot;Innehållstyp = `podcast`&quot; |
| Medieinnehållstyp: Ljudbok | Segmentera allt innehåll i ljudboken | &quot;Innehållstyp = `audiobook`&quot; |
| Medieinnehållstyp: AoD | Segmentera allt AoD-innehåll | &quot;Innehållstyp = `aod`&quot; |

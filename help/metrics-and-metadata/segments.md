---
title: Beskrivning av medieströmningssegment
description: '"Lär dig mer om de rapporteringssegment som är associerade med mediaströmstyp, inklusive segment, beskrivning och regel för mediaströmstyp."'
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: '"Medieanalys, segmentering"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: 2d9d4352b0fd71710a9952ba4a77f6796ea9f5cc
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 6%

---

# Segment{#segments}

Med segment kan du identifiera undergrupper av besökare baserat på egenskaper eller webbplatsinteraktioner. Med direktuppspelade mediesegment kan du identifiera typ av besöksström, till exempel ljud-, live- eller poddsändningsströmmar. Mer information om Adobe Analytics-segment finns i [Om segment och behållare](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=en) i Adobe Analytics Components Guide.

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

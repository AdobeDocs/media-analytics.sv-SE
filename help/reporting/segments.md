---
title: Beskrivning av medieströmningssegment
description: Lär dig mer om de rapporteringssegment som är associerade med mediaströmstyp, inklusive segment, beskrivning och regel för mediaströmstyp.
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: "Streaming Media, Segmentation"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Mediesegment{#segments}

Med segment kan du identifiera undergrupper av besökare baserat på egenskaper eller webbplatsinteraktioner. Med direktuppspelade mediesegment kan du identifiera typ av besöksström, till exempel ljud-, live- eller poddsändningsströmmar. Mer information om Adobe Analytics-segment finns i [Om segment och behållare](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=sv-SE) i Adobe Analytics Components Guide.

>[!NOTE]
>
>Dessa rapporteringssegment som är associerade med mediaströmstypen introducerades den 18 mars 2018 tillsammans med parametern `streamType`.

| Segment | Beskrivning | Regel |
|---|---|---|
| Medieströmtyp: Alla | Segmentera alla *media*-strömdata | &quot;Innehåll (ID) finns&quot; |
| Typ av medieström: Ljud | Segmentera alla *ljud*-strömdata | &quot;Innehåll (ID) finns&quot; OCH &quot;Typ av medieström = `audio`&quot; |
| Medieströmtyp: Video | Segmentera alla *video*-strömdata | &quot;Innehåll (ID) finns&quot; OCH &quot;Typ av medieström != `audio`&quot; |
| Medieinnehållstyp: VoD | Segmentera allt VoD-innehåll | &quot;Innehållstyp = `vod`&quot; |
| Medieinnehållstyp: Live | Segmentera allt Live-innehåll | &quot;Innehållstyp = `live`&quot; |
| Medieinnehållstyp: Linjär | Segmentera allt linjärt innehåll | &quot;Innehållstyp = `linear`&quot; |
| Medieinnehållstyp: poddsändning | Segmentera allt innehåll i poddsändning | &quot;Innehållstyp = `podcast`&quot; |
| Medieinnehållstyp: Ljudbok | Segmentera allt innehåll i ljudboken | &quot;Innehållstyp = `audiobook`&quot; |
| Medieinnehållstyp: AoD | Segmentera allt AoD-innehåll | &quot;Innehållstyp = `aod`&quot; |

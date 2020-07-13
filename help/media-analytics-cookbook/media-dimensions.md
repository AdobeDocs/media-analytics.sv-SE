---
title: Attribution för medieström
description: null
translation-type: tm+mt
source-git-commit: cab9724476f7864ac23c4293e402e0443771cb1e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---


# Attribution för medieström

Med den här funktionen kan du länka programåtgärder till mediespårningsdata utan att behöva använda ytterligare bearbetningsregler och anpassade variabler.

## Mediedimensioner utanför mediespårning

Med Media Stream Attribution kan kunderna nu lägga till alla mediedimensioner till alla andra analysanrop, som sidvyer och anpassade länkar. Under implementeringen måste du lägga till parametrar för mediekontextdata i Analytics-spårningsanropen. Den fullständiga listan över parametrar för kontextdata som används för media finns här: [Parametrar för ljud och video.](/help/metrics-and-metadata/audio-video-parameters.md)

Du måste även aktivera mediespårningskonfigurationen på nytt från Admin Console för varje rapport som du vill aktivera den här funktionen för.

>[!NOTE]
>
>Mediemätningarna är _inte_ tillgängliga för användning utanför mediespårning eftersom de flesta av dessa beräknas av Media Analytics utifrån hjärtslagshändelser. Det är också viktigt att mediemätningarna inte påverkas av olika implementeringar.

## Använda

JavaScript-exemplet nedan genererar ett anrop för spårning av anpassade länkar som har namnet inställt på&quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

I Analytics-rapporter kan du använda `Show` eVar för att dela upp data, och du kan räkna antalet instanser av spårlänkar. Rapporteringen skulle se ut ungefär så här:

![](/assets/myShow-rpt-1.png)

## Användningsexempel

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)


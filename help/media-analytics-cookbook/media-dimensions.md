---
title: Vad är Media Stream Attribution?
description: Lär dig hur du länkar programåtgärder till mediespårningsdata utan att behöva använda ytterligare bearbetningsregler och anpassade variabler.
translation-type: tm+mt
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---


# Attribution för medieström

Med den här funktionen kan du länka programåtgärder till mediespårningsdata utan att behöva använda ytterligare bearbetningsregler och anpassade variabler.

## Media Dimensions Outside Media Tracking

Med Media Stream Attribution kan kunderna nu lägga till alla mediedimensioner
till alla andra analysanrop, som sidvyer och anpassade länkar. Under genomförandet
du måste lägga till parametrar för mediekontextdata i Analytics-spårningsanropen. Den fullständiga listan
De kontextdataparametrar som används för media finns här: [Parametrar för ljud och video.](/help/metrics-and-metadata/audio-video-parameters.md)

Du måste även aktivera mediespårningskonfigurationen på nytt från Admin Console för varje rapport som du vill aktivera den här funktionen för.

>[!NOTE]
>
>Mediemätningarna är _inte_ tillgängliga för användning utanför mediespårning eftersom de flesta av dessa beräknas i Media Analytics utifrån hjärtslagshändelser. Det är också viktigt att mediemätningarna inte påverkas av olika implementeringar.

## Använda

JavaScript-exemplet nedan genererar ett anrop för spårning av anpassade länkar som har namnet inställt på&quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

I analysrapporter kan du använda eVar `Show` för att dela upp data, och du kan räkna instanserna av spårlänken. Rapporteringen skulle se ut ungefär så här:

![](/assets/myShow-rpt-1.png)

## Användningsexempel

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

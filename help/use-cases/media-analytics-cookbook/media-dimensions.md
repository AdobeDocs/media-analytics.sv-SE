---
title: Vad är medieströmsattribuering?
description: Lär dig hur du länkar programåtgärder till mediespårningsdata utan att behöva använda ytterligare bearbetningsregler och anpassade variabler.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# Attribut för medieström {#media-stream-attribution}

Med Media Stream Attribution kan ni länka programåtgärder till mediaspårningsdata utan att behöva använda ytterligare bearbetningsregler och anpassade variabler.

## Media Dimensions Outside Media Tracking

Du kan lägga till mediedimensioner till analyssamtal som sidvyer och anpassade länkar. Under implementeringen måste du lägga till parametrar för mediekontextdata i Analytics-spårningsanropen. En fullständig lista över tillgängliga parametrar för kontextdata som används för media finns i [Parametrar för ljud och video.](/help/implementation/variables/audio-video-parameters.md)

Om du vill aktivera den här funktionen för en viss rapport aktiverar du mediespårningskonfigurationen på nytt från Admin Console.

>[!NOTE]
>
>Mediemätningarna är _not_ som kan användas utanför mediespårning eftersom de flesta av dessa beräknas av tillägget Streaming Media Collection baserat på pulsslagshändelser. Det är också viktigt att mediemätningarna inte påverkas av olika implementeringar.

## Använda attribut för medieström

I JavaScript-exemplet nedan genereras ett anrop för spårning av anpassade länkar med namnet&quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

I Analytics-rapporter kan ni använda `Show` eVar för att dela upp data, så kan du räkna instanserna av spårlänken. Rapporteringen skulle se ut ungefär så här:

![](/assets/myShow-rpt-1.png)

## Användningsfall

I följande exempel visas användningsexempel för följande:

* Kategoriplacering
* Hero Placement
* Engagemang
* Prenumerationer

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

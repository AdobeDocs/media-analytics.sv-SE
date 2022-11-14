---
title: Vad är Media Stream Attribution?
description: Lär dig hur du länkar programåtgärder till mediespårningsdata utan att behöva använda ytterligare bearbetningsregler och anpassade variabler.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Attribution för medieström {#media-stream-attribution}

Med Media Stream Attribution kan ni länka programåtgärder till mediaspårningsdata utan att behöva använda ytterligare bearbetningsregler och anpassade variabler.

## Media Dimensions Outside Media Tracking

Du kan lägga till mediedimensioner till analyssamtal som sidvyer och anpassade länkar. Under implementeringen måste du lägga till parametrar för mediekontextdata i Analytics-spårningsanropen. En fullständig lista över tillgängliga parametrar för kontextdata som används för media finns i [Parametrar för ljud och video.](/help/implementation/variables/audio-video-parameters.md)

Om du vill aktivera den här funktionen för en viss rapport aktiverar du mediespårningskonfigurationen på nytt från Admin Console.

>[!NOTE]
>
>Mediemätningarna är _not_ som kan användas utanför mediespårning eftersom de flesta av dessa beräknas med Streaming Media Analytics baserat på pulsslagshändelser. Det är också viktigt att mediemätningarna inte påverkas av olika implementeringar.

## Använda attribut för medieström

I JavaScript-exemplet nedan genereras ett anpassat länkspårningsanrop som har namnet inställt på&quot;Hero Banner&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

I Analytics-rapporter kan ni använda `Show` eVar för att dela upp data, så kan du räkna instanserna av spårlänken. Rapporteringen skulle se ut ungefär så här:

![](/assets/myShow-rpt-1.png)

## Användningsexempel

I följande exempel visas användningsexempel för följande:

* Kategoriplacering
* Hero Placement
* Engagemang
* Prenumerationer

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

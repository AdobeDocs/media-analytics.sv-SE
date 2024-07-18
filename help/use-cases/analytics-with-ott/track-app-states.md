---
title: Spåra applägen
description: Applägena är de olika skärmarna eller vyerna i ditt program. Lär dig hur du spårar appens tillstånd i ditt program med hjälp av trackState-anropet.
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Spåra programtillstånd{#track-app-states}

Lägen är de olika skärmarna eller vyerna i ditt program. Varje gång ett nytt läge visas i ditt program bör du skicka ett `trackState`-samtal. Om en användare till exempel navigerar från hemsidan till skärmen med videoinformation skickar du ett `trackState`-samtal. Lägen visas vanligtvis med hjälp av en panelrapport, så att du kan se hur användare navigerar i appen och vilka lägen som visas oftast.

## trackState-anrop

Du anropar vanligtvis `trackState` varje gång appen läser in en ny skärm.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Kromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

Lägesnamnet rapporteras i variabeln Visa läge i Adobe Mobile-tjänster och en vy registreras för varje `trackState`-anrop. I andra Analytics-gränssnitt rapporteras &quot;View State&quot; som &quot;Page Name&quot;; &quot;State Views&quot; som &quot;Page Views&quot;.

## Skicka kontextdata

Utöver&quot;Lägesnamn&quot; kan du skicka ytterligare kontextdata för varje spårningslägesanrop.

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Kromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>Kontextdatavärden måste mappas till anpassade variabler i Adobe Mobile-tjänster.

---
title: Spåra programtillstånd
description: 'Apptillstånd är de olika skärmarna eller vyerna i ditt program, som när de visas bör resultera i ett trackState-anrop. '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra programtillstånd{#track-app-states}

Lägen är de olika skärmarna eller vyerna i ditt program. Varje gång ett nytt läge visas i programmet bör du ringa ett `trackState` samtal. Om en användare t.ex. navigerar från hemsidan till skärmen med videoinformation skickar du ett `trackState` samtal. Lägen visas vanligtvis med hjälp av en panelrapport, så att du kan se hur användare navigerar i appen och vilka lägen som visas oftast.

## trackState-anrop

Du brukar ringa `trackState` varje gång appen läser in en ny skärm.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Kromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

Lägesnamnet rapporteras i variabeln Visa läge i Adobe Mobile Services och en vy registreras för varje `trackState` anrop. I andra analysgränssnitt rapporteras&quot;Visa läge&quot; som&quot;Sidnamn&quot;. &quot;Lägesvyer&quot; rapporteras som &quot;Sidvyer&quot;.

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
>Kontextdatavärden måste mappas till anpassade variabler i Adobe Mobile Services.


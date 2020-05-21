---
title: Exempel på spårning av spelartillstånd
description: Det här avsnittet innehåller exempel på funktionen Spårning av spelartillstånd.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Exempel på spårning av spelartillstånd

Lägg till exempel


## Exempel på lång paus

När en videosession har en paus som är längre än 30 minuter krävs en ny session för API:t. När detta inträffar bör klienten generera ett nytt sessions-ID. För båda videosessionerna bör klienten behålla alla lägen som spelaren är i och skicka all information som en `stateStart` händelse direkt efter `sessionStart` anropet.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

När `sessionEnd` meddelandet har skickats måste en ny videosession startas och de första API-händelserna blir:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

Exemplet med lång paus visar att spelaren också lagrar sina lägen, så att de kan skickas till den nya videosessionen.

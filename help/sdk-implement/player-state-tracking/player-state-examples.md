---
title: Exempel på spårning av spelartillstånd
description: Det här avsnittet innehåller exempel på funktionen Spårning av spelartillstånd.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: 8a421ee4ee5d2e61126fc6ac8f10f326427e78a7
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Exempel på spårning av spelartillstånd


## Exempel på lång paus

När en videosession har en paus som är längre än 30 minuter krävs en ny session för API:t. När detta inträffar bör klienten generera ett nytt sessions-ID. För båda videosessionerna bör klienten behålla alla lägen som spelaren är i och skicka all information som en `stateStart`-händelse direkt efter `sessionStart`-anropet.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

När `sessionEnd` har skickats måste en ny videosession startas och de första API-händelserna blir:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

Exemplet med lång paus visar att spelaren också lagrar sina lägen, så att de kan skickas till den nya videosessionen.

---
title: Exempel på spårning av spelartillstånd
description: Det här avsnittet innehåller exempel på funktionen Spårning av spelartillstånd.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Exempel på spårning av spelartillstånd


## Exempel på lång paus

När en videosession har en paus som är längre än 30 minuter krävs en ny session för API:t. När detta inträffar bör klienten generera ett nytt sessions-ID. För båda videosessionerna bör klienten behålla alla lägen som spelaren är i och skicka all information som en `stateStart` -händelsen direkt efter `sessionStart` ring.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Efter `sessionEnd` skickas, en ny videosession måste startas och de första API-händelserna blir:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

Exemplet med lång paus visar att spelaren också lagrar sina lägen, så att de kan skickas till den nya videosessionen.

---
title: Timeout-villkor
description: Lär dig mer om timeoutvillkoren för Media Collection API.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Timeoutvillkor{#timeout-conditions}

**API-timeoutvillkor för mediainsamling**

Media Collection API har inte samma funktion som Media SDK för att utfärda ett nytt sessions-ID när timeoutförhållanden inträffar. När ett timeout-villkor inträffar kommer serverdelen att stänga sessionen och alla efterföljande anrop som görs med detta sessions-ID kommer att tas bort. Logiken som hanterar en timeout för session måste hanteras i klienten. Det innebär att spelaren måste övervaka timeoutvillkoren och hämta ett nytt sessions-ID om en timeout inträffar.

* **10 minuter: Inga API-händelser**

  Om serverdelen inte tar emot några API-händelser kommer den att stänga sessionen.
* **30 minuter: Ingen ändring av spelhuvudet**

  Om spelhuvudet inte flyttas på 30 minuter (användaren till exempel träffar Paus och går bort), kommer serverdelen att stänga sessionen.

>[!NOTE]
>
>Du kan också tvinga fram ett sessionsslut genom att skicka en `events`-begäran med händelsetypen `sessionEnd`.

---
title: Kontrollera händelseordningen
description: Kontrollera händelseordningen
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: 27694ec83de89980404df7a7cc77fa42b3d1a751
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Kontrollera ordningen för händelser{#controlling-the-order-of-events}

Spårning av direktuppspelad video är en mycket tidsberoende åtgärd och ibland kommer API-spårningsanrop för Media Collection i fel ordning. I det här fallet försöker backend placera händelser i kö och ordna om dem baserat på den angivna tidsstämpeln i `playerTime`-objektet.  Detta sker med vissa begränsningar. För närvarande kan det hända att ordningen inte fungerar om fördröjningarna mellan telefonsamtal som inte är i ordning är mer än en sekund. I framtida uppdateringar kan den&quot;godtagbara fördröjningstiden&quot; optimeras och konfigureras.

## Exempel på en händelse som inte är i ordning

Oordnade händelser inträffar när händelser passerar genom nätverket, vilket ibland orsakar en fördröjning.

Du kan till exempel skicka en `adBreakStart`-händelse följt av en `adStart`-händelse. Detta är ett vanligt användningsexempel eftersom det krävs att en annons börjar inuti en annonsbrytning.

Om annonsen är klar och ingen buffert behövs inträffar båda händelserna nästan omedelbart och `playerTime.ts` för båda händelserna är mycket nära varandra, men de ska aldrig vara lika.

> Händelsens &quot;playerTime.ts&quot; ska aldrig vara lika för någon händelse, eftersom sorteringsalgoritmen inte skulle veta vilken händelse som hände först. Det ska finnas minst 1 millisekunds skillnad i tidsstämpling för varannan efterföljande händelse.

Eftersom båda händelserna inträffar mycket nära varandra när nätverksanrop utlöses, är det möjligt att de inte kommer i rätt ordning. I det här exemplet inträffar händelsen `adStart` före händelsen `adBreakStart`.


Det finns ett tidsfönster med händelser: 5 sekunder eller maximalt 10 händelser. Händelserna buffras innan de skickas till bearbetningsflödet. När villkoren är uppfyllda - 5 sekunder har passerat eller fler än 10 händelser har tagits emot, ordnas händelserna om baserat på `playerTime.ts` och skickas sedan i den nya ordningen till bearbetningsflödet.

>[!IMPORTANT]
>
>Det finns en undantagshändelse som skickas direkt till bearbetningsflödet och det är händelsen `sessionStart`.

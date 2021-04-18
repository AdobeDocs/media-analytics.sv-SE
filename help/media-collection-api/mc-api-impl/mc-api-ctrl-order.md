---
title: Kontrollera händelseordningen
description: Kontrollera händelseordningen
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Kontrollera ordningen för händelser{#controlling-the-order-of-events}

Eftersom API:t för Media Collection är RESTful och videospårning är en mycket tidsberoende åtgärd kan en implementerare vara orolig för API-spårningsanrop för Media Collection som kommer i fel ordning. Baksidan *försöker* placera händelser i kö och ordna om dem baserat på den angivna tidsstämpeln i `playerTime`-objektet. Det finns dock en gräns för denna kapacitet. För närvarande kan ordningsföljden misslyckas om fördröjningarna mellan ej beställda samtal är mer än en sekund. Denna&quot;godtagbara fördröjningstid&quot; kan optimeras och/eller kunna konfigureras i framtida uppdateringar.

---
title: Kontrollera händelseordningen
description: null
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Kontrollera händelseordningen{#controlling-the-order-of-events}

Eftersom API:t för Media Collection är RESTful och videospårning är en mycket tidsberoende åtgärd kan en implementerare vara orolig för API-spårningsanrop för Media Collection som kommer i fel ordning. Baksidan *försöker* köa och ordna om händelser baserat på den angivna tidsstämpeln i `playerTime` objektet. Det finns dock en gräns för denna kapacitet. För närvarande kan ordningsföljden misslyckas om fördröjningarna mellan ej beställda samtal är mer än en sekund. Denna&quot;godtagbara fördröjningstid&quot; kan optimeras och/eller kunna konfigureras i framtida uppdateringar.

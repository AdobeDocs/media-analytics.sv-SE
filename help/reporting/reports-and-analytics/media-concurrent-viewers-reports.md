---
title: Medievisningsprogram för samtidig användning
description: "Lär dig mer om Media Concurrent Viewer som används för att visa samtidiga visningsprogram under en dag. Data kan filtreras efter innehåll, enhetstyp eller land."
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: "Media Analytics, Reports & Analytics Basics"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# Rapport om samtidiga visningsprogram för media {#media-concurrent-viewers}

Kontrollpanelen för samtidiga visningsprogram i Media visar samtidiga visningsprogram under en dag. Data kan filtreras efter innehåll, enhetstyp eller land.

>[!TIP]
>
> Den här rapporten baseras på samtidiga aktiva mediesessioner.  Använd [Media Concurrent Viewers panel i Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html).

![](assets/video-concurrent-viewers.png)

## Rapportfunktioner {#report-features}

Här är några funktioner i den här rapporten:

* Detta är inte i realtid. Den har normal Adobe Analytics latens.
* Rapporten omfattar en 24-timmarsram. X-axeln baseras på tidszonen för rapportsviten.
* Detta visar samtidiga visningsprogram vid minutgranularitet.
* Det finns en *Rapport över samtidiga visningsprogram för media* som visar hur många tittare som tittar på eller lyssnar på allt innehåll.
* Det finns en Concurrent Viewer-rapport i *Medieinformation* som visar hur många tittare som tittar på eller lyssnar på ett visst medieobjekt.
* Rapporten fungerar bara över en dag.
* Kunden kan se historiska rapporter om samtidig användning (begränsat till en enstaka dag).

## Begränsningar {#limitations}

Här följer några begränsningar för den här rapporten:

* Inga data visas om det valda intervallet inte är en hel dag.
* Du kan inte exportera data, till exempel ReportBuilder.
* Du kan inte presentera data i ett tabellformat.
* Du kan inte skicka en rapport via e-post.
* Även om du inte spårar annonser måste du aktivera mediespårning igen och välja modulen Medieannonsering.
* Den här funktionen ger korrekta data när du använder ett hjärtslagsbibliotek som har funktioner för att pausa spårning.

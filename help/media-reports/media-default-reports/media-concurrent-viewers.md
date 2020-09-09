---
title: Medievisningsprogram för samtidig användning
description: null
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
translation-type: tm+mt
source-git-commit: cb54b862a0d4a179c499e3a28ab49301121de1bf
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---


# Medievisningsprogram för samtidig användning{#media-concurrent-viewers}

Kontrollpanelen för samtidiga visningsprogram i Media visar samtidiga visningsprogram under en dag. Data kan filtreras efter innehåll, enhetstyp eller land.

>[!TIP]
>
> Den här rapporten baseras på samtidiga aktiva mediesessioner.  Använd [Media Concurrent Viewers panel i Analysis Workspace](https://docs.adobe.com/content/help/sv-SE/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html).


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

---
title: Beskrivning av parametern Heartbeat
description: Utforska de hjärtslagsparametrar som Adobe samlar in och bearbetar på Media Analytics-servern (hjärtslag).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: '"Media Analytics, Variables"'
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 5%

---

# Parameterbeskrivningar för Media Analytics (hjärtslag){#heartbeat-parameter-descriptions}

Lista med Media Analytics-parametrar som Adobe samlar in och bearbetar på Media Analytics-servern (hjärtslag):

## Alla händelser

| Namn | Datakälla |  Beskrivning  |
| ---  | --- | --- |
| s:event:typ | Media SDK | (Obligatoriskt)<br/><br/>Typen av händelse som spåras. Händelsetyper: <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=kapitel_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | Media SDK | (Obligatoriskt)<br/><br/>Tidsstämpeln för den senaste händelsen av samma typ i den här sessionen. Värdet är -1. |
| l:event:ts | Media SDK | (Obligatoriskt)<br/><br/>Tidsstämpeln för händelsen. |
| l:event:varaktighet | Media SDK | (Obligatoriskt)<br/><br/>Detta värde anges internt (i millisekunder) av Media SDK, inte av spelaren. Den används för att beräkna hur lång tid som har ägnats åt backend-data. Exempel: a.media.totalTimePlayed beräknas som en summa av varaktigheten för alla uppspelningshjärtslag (type=play) som genereras. <br/>*Obs!* Den här parametern är inställd på 0 för vissa händelser eftersom de är &quot;state change events&quot; (t.ex. type=complete, type=chapter_complete eller type=bitrate_change.) |
| l:event:spelhuvud | VideoInfo | (Obligatoriskt)<br/><br/>Spelhuvudet fanns inuti den aktiva resursen (huvud eller ad) när händelsen spelades in. |
| s:event:sid | Media SDK | (Obligatoriskt)<br/><br/>Sessions-ID (en slumpmässigt genererad sträng). Alla händelser i en viss session (video + annonser) bör vara desamma. |
| l:asset:duration / l:asset:length <br/>(ändrat namn från längd) | VideoInfo | (Obligatoriskt)<br/><br/>Huvudresursens videolängd. |
| s:asset:utgivare | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Utgivaren av resursen. |
| s:asset:video_id | VideoInfo | (Obligatoriskt)<br/><br/>Ett ID som unikt identifierar videon i utgivarens katalog. |
| s:asset:typ | Media SDK | (Obligatoriskt)<br/><br/>Resurstypen (huvud eller ad). |
| s:stream:typ | VideoInfo | (Obligatoriskt)<br/><br/>Strömtypen. Kan vara något av följande: <ul> <li> live </li> <li> vod </li> <li> linjär </li> </ul> |
| s:user:id | Konfigurera objekt för mobil, appmätning VisitorID | (Valfritt)<br/><br/>Användarens särskilda inställning för besökar-ID. |
| s:user:hjälp | Experience Cloud Org | (Valfritt)<br/><br/>Användarens ID-värde för Analytics Visitor. |
| s:user:mitt | Experience Cloud Org | (Obligatoriskt)<br/><br/>Användarens Experience Cloud-besökar-ID-värde. |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | (Valfritt)<br/><br/>Alla användar-ID:n för kund har angetts för Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>AAM data som skickas på varje nyttolast efter a_start |
| s:aam:blob | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>AAM data som skickas på varje nyttolast efter a_start |
| s:sc:rsid | Report Suit ID (eller ID) | (Obligatoriskt)<br/><br/>Adobe Analytics RSID, dit rapporter ska skickas. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Adobe Analytics spårningsserver. |
| h:sc:ssl | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Om trafiken sker via HTTPS (om värdet är 1) eller över HTTP (är 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Valfritt)<br/><br/>Ange som&quot;primetime&quot; för Primetime-spelare eller den verkliga OVP:n för andra spelare. |
| s:sp:sdk | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Versionssträngen OVP. |
| s:sp:player_name | VideoInfo | (Obligatoriskt)<br/><br/>Namn på videospelare (den faktiska spelarprogramvara som används för att identifiera spelaren). |
| s:sp:kanal | MediaHeartbeatConfig | (Valfritt)<br/><br/>Den kanal där användaren tittar på innehållet. Appnamnet för en mobilapp. Domännamnet för en webbplats. |
| s:sp:hb_version | Media SDK | (Obligatoriskt)<br/><br/>Versionsnumret för det Media SDK-bibliotek som utfärdar samtalet. |
| l:stream:bithastighet | QoSInfo | (Obligatoriskt)<br/><br/>Aktuellt värde för strömmens bithastighet (i bps). |

## Felhändelser

| Namn | Datakälla | Beskrivning   |
| ---  | --- | --- |
| s:event:källa | Media SDK | (Obligatoriskt)<br/><br/>Felets källa, antingen spelarintern eller programnivå. |
| s:event:id | Media SDK | (Obligatoriskt)<br/><br/>Fel-ID, identifierar felet unikt. |

## Annonshändelser

| Namn | Datakälla | Beskrivning   |
| ---  | --- | --- |
| s:asset:ad_id | AdInfo | (Obligatoriskt)<br/><br/>Annonsens namn. |
| s:asset:ad_sid | Media SDK | (Obligatoriskt)<br/><br/>En unik identifierare som genereras av Media SDK, som läggs till i alla annonsrelaterade pingar. |
| s:asset:pod_id | Media SDK | (Obligatoriskt)<br/><br/>Pod ID inuti videon. Detta värde beräknas automatiskt utifrån följande formel: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | AdBreakInfo | (Obligatoriskt)<br/><br/>Index för annonsen i rutan (den första annonsen har index 0, den andra annonsen har index 1 osv.). |
| s:asset:lösare | AdBreakInfo | (Obligatoriskt)<br/><br/>Annonslösaren. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Valfritt)<br/><br/>Anpassade annonsmetadata. |

## Kapitelhändelser

| Namn | Datakälla | Beskrivning   |
| ---  | --- | --- |
| s:stream:kapitel_sid | Media SDK | (Obligatoriskt)<br/><br/>Den unika identifierare som är associerad med kapitlets uppspelningsinstans.  <br/> **Obs!** Ett kapitel kan spelas upp flera gånger på grund av åtgärder som användaren utför vid sökning. |
| s:stream:kapitelnamn | ChapterInfo | (Valfritt)<br/><br/>Kapitelets namn (dvs. läsbart för människor). |
| s:stream:kapitel_id | Media SDK | (Obligatoriskt)<br/><br/>Unikt ID för kapitlet. Detta värde beräknas automatiskt utifrån följande formel: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:kapitel_pos | ChapterInfo | (Obligatoriskt)<br/><br/>Kapitelns index i kapitellistan (med början från 1). |
| l:stream:kapitelförskjutning | ChapterInfo | (Obligatoriskt)<br/><br/>Kapitlets förskjutning (uttryckt i sekunder) inuti huvudinnehållet, exklusive annonser. |
| l:stream:kapitellängd | ChapterInfo | (Obligatoriskt)<br/><br/>Kapitlets längd (uttryckt i sekunder). |
| s:meta:custom_chapter_metadata.x | ChapterInfo | (Valfritt)<br/><br/>Anpassade kapitelmetadata. |

## Sessionsslutshändelse

| Namn | Datakälla | Beskrivning   |
| ---  | --- | --- |
| s:event:type=end | Media SDK | (Obligatoriskt)<br/><br/> `end` `close` |

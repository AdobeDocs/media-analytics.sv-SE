---
title: Beskrivning av parametern Heartbeat
description: Utforska de hjärtslagsparametrar som Adobe samlar in och bearbetar på Media Analytics-servern (hjärtslag).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: "Media Analytics, Variables"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 5%

---

# Parameterbeskrivningar för Media Analytics (hjärtslag){#heartbeat-parameter-descriptions}

Lista med Media Analytics-parametrar som Adobe samlar in och bearbetar på Media Analytics-servern (hjärtslag):

## Alla händelser

| Namn | Datakälla |  Beskrivning  |
| ---  | --- | --- |
| s:event:type | Media SDK | (Obligatoriskt)<br/><br/>Typ av händelse som spåras. Händelsetyper: <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=chapter_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | Media SDK | (Obligatoriskt)<br/><br/>Tidsstämpeln för den senaste händelsen av samma typ i den här sessionen. Värdet är -1. |
| l:event:ts | Media SDK | (Obligatoriskt)<br/><br/>Tidsstämpeln för händelsen. |
| l:event:varaktighet | Media SDK | (Obligatoriskt)<br/><br/>Värdet anges internt (i millisekunder) av Media SDK, inte av spelaren. Den används för att beräkna hur lång tid som har ägnats åt backend-data. Exempel: a.media.totalTimePlayed beräknas som en summa av varaktigheten för alla uppspelningshjärtslag (type=play) som genereras. <br/>*Obs!* Den här parametern är inställd på 0 för vissa händelser eftersom de är &quot;state change events&quot; (t.ex. type=complete, type=chapter_complete eller type=bitrate_change.) |
| l:event:spelhuvud | VideoInfo | (Obligatoriskt)<br/><br/>Spelhuvudet fanns inuti den aktiva resursen (huvud eller annons) när händelsen spelades in. |
| s:event:sid | Media SDK | (Obligatoriskt)<br/><br/>Sessions-ID (en slumpmässigt genererad sträng). Alla händelser i en viss session (video + annonser) bör vara desamma. |
| l:asset:duration / l:asset:length <br/>(Namnet har ändrats från längd) | VideoInfo | (Obligatoriskt)<br/><br/>Huvudresursens videolängd. |
| s:asset:utgivare | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Utgivaren av resursen. |
| s:asset:video_id | VideoInfo | (Obligatoriskt)<br/><br/>Ett ID som unikt identifierar videon i utgivarens katalog. |
| s:asset:type | Media SDK | (Obligatoriskt)<br/><br/>Tillgångstypen (huvud eller annons). |
| s:stream:type | VideoInfo | (Obligatoriskt)<br/><br/>Strömtypen. Kan vara något av följande: <ul> <li> live </li> <li> vod </li> <li> linjär </li> </ul> |
| s:user:id | Konfigurera objekt för mobil, appmätning VisitorID | (Valfritt)<br/><br/>Användaren anger specifikt besökar-ID. |
| s:user:stöd | Experience Cloud Org | (Valfritt)<br/><br/>Användarens ID-värde för Analytics Visitor. |
| s:user:mitten | Experience Cloud Org | (Obligatoriskt)<br/><br/>Användarens Experience Cloud-besökar-ID-värde. |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | (Valfritt)<br/><br/>Alla användar-ID:n för kund har angetts i Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>AAM data som skickas för varje nyttolast efter a_start |
| s:aam:blob | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>AAM data som skickas för varje nyttolast efter a_start |
| s:sc:rsid | Report Suit ID (eller ID) | (Obligatoriskt)<br/><br/>Adobe Analytics RSID, dit rapporter ska skickas. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Adobe Analytics spårningsserver. |
| h:sc:ssl | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Anger om trafiken sker via HTTPS (om värdet är 1) eller via HTTP (är inställt på 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Valfritt)<br/><br/>Ange som&quot;primetime&quot; för Primetime-spelare eller som OVP för andra spelare. |
| s:sp:sdk | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>OVP-versionssträngen. |
| s:sp:player_name | VideoInfo | (Obligatoriskt)<br/><br/>Videospelarens namn (det faktiska spelarprogrammet som används för att identifiera spelaren). |
| s:sp:kanal | MediaHeartbeatConfig | (Valfritt)<br/><br/>Den kanal där användaren tittar på innehållet. Appnamnet för en mobilapp. Domännamnet för en webbplats. |
| s:sp:hb_version | Media SDK | (Obligatoriskt)<br/><br/>Versionsnumret för det Media SDK-bibliotek som utfärdar samtalet. |
| l:stream:bithastighet | QoSInfo | (Obligatoriskt)<br/><br/>Det aktuella värdet för strömmens bithastighet (i bps). |

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
| s:asset:pod_position | AdBreakInfo | (Obligatoriskt)<br/><br/>Index för annonsen i rutan (den första annonsen har index 0, den andra annonsen har index 1, osv.). |
| s:asset:lösare | AdBreakInfo | (Obligatoriskt)<br/><br/>Annonslösaren. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Valfritt)<br/><br/>Anpassade annonsmetadata. |

## Kapitelhändelser

| Namn | Datakälla | Beskrivning   |
| ---  | --- | --- |
| s:stream:kapitel_sid | Media SDK | (Obligatoriskt)<br/><br/>Den unika identifierare som är associerad med kapitlets uppspelningsinstans.  <br/> **Obs!** Ett kapitel kan spelas upp flera gånger på grund av åtgärder som användaren utför vid sökning. |
| s:stream:kapitel_namn | ChapterInfo | (Valfritt)<br/><br/>Kapitelns eget namn (dvs. läsbart för människor). |
| s:stream:kapitel_id | Media SDK | (Obligatoriskt)<br/><br/>Unikt ID för kapitlet. Detta värde beräknas automatiskt utifrån följande formel: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:kapitel_pos | ChapterInfo | (Obligatoriskt)<br/><br/>Kapitlets index i kapitellistan (med början från 1). |
| l:stream:kapitel_offset | ChapterInfo | (Obligatoriskt)<br/><br/>Kapitlets förskjutning (uttryckt i sekunder) inuti huvudinnehållet, exklusive annonser. |
| l:stream:chapter_length | ChapterInfo | (Obligatoriskt)<br/><br/>Kapitlets längd (uttryckt i sekunder). |
| s:meta:custom_chapter_metadata.x | ChapterInfo | (Valfritt)<br/><br/>Anpassade kapitelmetadata. |

## Sessionsslutshändelse

| Namn | Datakälla | Beskrivning   |
| ---  | --- | --- |
| s:event:type=end | Media SDK | (Obligatoriskt)<br/><br/> The `end` `close` |

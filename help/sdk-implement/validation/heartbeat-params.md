---
title: Beskrivningar av pulsslagsparametrar
description: En lista över de hjärtslagsparametrar som Adobe samlar in och bearbetar på Media Analytics-servern (hjärtslag).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Parameterbeskrivningar för Media Analytics (hjärtslag){#heartbeat-parameter-descriptions}

Lista med Media Analytics-parametrar som Adobe samlar in och bearbetar på Media Analytics-servern (hjärtslag):

## Alla händelser

| Namn | Datakälla |  Beskrivning |
| ---  | --- | --- |
| s:event:type | Media SDK | (Obligatoriskt)<br/><br/>Den typ av händelse som spåras. Händelsetyper: <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=chapter_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:händelse:prev_ts | Media SDK | (Obligatoriskt)<br/><br/>Tidsstämpeln för den senaste händelsen av samma typ i den här sessionen. Värdet är -1. |
| l:event:ts | Media SDK | (Obligatoriskt)<br/><br/>Tidsstämpeln för händelsen. |
| l:händelse:varaktighet | Media SDK | (Obligatoriskt)<br/><br/>Det här värdet anges internt (i millisekunder) av Media SDK, inte av spelaren. Den används för att beräkna hur lång tid som har ägnats åt backend-data. Exempel: a.media.totalTimePlayed beräknas som en summa av varaktigheten för alla uppspelningshjärtslag (type=play) som genereras. <br/>*Obs!*Den här parametern är inställd på 0 för vissa händelser eftersom de är &quot;state change events&quot; (t.ex. type=complete, type=chapter_complete eller type=bitrate_change.) |
| l:händelse:spelhuvud | VideoInfo | (Obligatoriskt)<br/><br/>Spelhuvudet fanns inuti den aktiva resursen (huvud eller annons) när händelsen spelades in. |
| s:händelse:sid | Media SDK | (Obligatoriskt)<br/><br/>Sessions-ID (en slumpmässigt genererad sträng). Alla händelser i en viss session (video + annonser) bör vara desamma. |
| l:asset:duration / l:asset:length <br/>(ändrat namn från längd) | VideoInfo | (Obligatoriskt)<br/><br/>Huvudresursens videolängd. |
| s:resurs:utgivare | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Utgivaren av resursen. |
| s:resurs:video_id | VideoInfo | (Obligatoriskt)<br/><br/>Ett ID som unikt identifierar videon i utgivarens katalog. |
| s:resurs:typ | Media SDK | (Obligatoriskt)<br/><br/>Tillgångstypen (huvud eller annons). |
| s:ström:typ | VideoInfo | (Obligatoriskt)<br/><br/>Strömtypen. Kan vara något av följande: <ul> <li> live </li> <li> vod </li> <li> linjär </li> </ul> |
| s:användare:id | Konfigurera objekt för mobil, appmätning VisitorID | (Valfritt)<br/><br/>Användarens särskilda inställning för besökar-ID. |
| s:user:aid | Experience Cloud-organisation | (Valfritt)<br/><br/>Användarens ID-värde för Analytics Visitor. |
| s:användare:mitt | Experience Cloud-organisation | (Obligatoriskt)<br/><br/>Användarens Experience Cloud-besökar-ID-värde. |
| s:customer:customer_user_ids_x | MediaHeartbeatConfig | (Valfritt)<br/><br/>Alla användar-ID:n för kunder har angetts för Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>AAM-data skickas för varje nyttolast efter a_start |
| s:aam:blob | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>AAM-data skickas för varje nyttolast efter a_start |
| s:sc:rsid | Report Suit ID (eller ID) | (Obligatoriskt)<br/><br/>Adobe Analytics RSID, dit rapporter ska skickas. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Adobe Analytics-spårningsserver. |
| h:sc:ssl | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Om trafiken sker via HTTPS (om värdet är 1) eller via HTTP (är inställt på 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Valfritt)<br/><br/>Ange som&quot;primetime&quot; för Primetime-spelare eller det verkliga OVP-värdet för andra spelare. |
| s:sp:sdk | MediaHeartbeatConfig | (Obligatoriskt)<br/><br/>Versionssträngen OVP. |
| s:sp:player_name | VideoInfo | (Obligatoriskt)<br/><br/>Videospelarens namn (spelarprogramvaran som används för att identifiera spelaren). |
| s:sp:kanal | MediaHeartbeatConfig | (Valfritt)<br/><br/>Den kanal där användaren tittar på innehållet. Appnamnet för en mobilapp. Domännamnet för en webbplats. |
| s:sp:hb_version | Media SDK | (Obligatoriskt)<br/><br/>Versionsnumret för det Media SDK-bibliotek som utlyste samtalet. |
| l:ström:bithastighet | QoSInfo | (Obligatoriskt)<br/><br/>Strömmens aktuella bithastighet (i bps). |

## Felhändelser

| Namn | Datakälla | Beskrivning |
| ---  | --- | --- |
| s:händelse:källa | Media SDK | (Obligatoriskt)<br/><br/>Felkällan, antingen spelarintern eller programnivå. |
| s:event:id | Media SDK | (Obligatoriskt)<br/><br/>Fel-ID, identifierar felet unikt. |

## Annonshändelser

| Namn | Datakälla | Beskrivning |
| ---  | --- | --- |
| s:asset:ad_id | AdInfo | (Obligatoriskt)<br/><br/>Annonsens namn. |
| s:asset:ad_sid | Media SDK | (Obligatoriskt)<br/><br/>En unik identifierare som genereras av Media SDK, som läggs till i alla annonsrelaterade pingar. |
| s:asset:pod_id | Media SDK | (Obligatoriskt)<br/><br/>Pod ID inuti videon. Detta värde beräknas automatiskt utifrån följande formel: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | AdBreakInfo | (Obligatoriskt)<br/><br/>Index för annonsen i rutan (den första annonsen har index 0, den andra annonsen har index 1 osv.). |
| s:resurs:lösare | AdBreakInfo | (Obligatoriskt)<br/><br/>Annonslösaren. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Valfritt)<br/><br/>Anpassade annonsmetadata. |

## Kapitelhändelser

| Namn | Datakälla | Beskrivning |
| ---  | --- | --- |
| s:ström:kapitel_sid | Media SDK | (Obligatoriskt)<br/><br/>Den unika identifierare som är associerad med kapitlets uppspelningsinstans.  <br/> **Obs!** Ett kapitel kan spelas upp flera gånger på grund av åtgärder som användaren utför vid sökning. |
| s:ström:kapitel_namn | ChapterInfo | (Valfritt)<br/><br/>Kapitelets eget namn (dvs. läsbart för människor). |
| s:ström:kapitel_id | Media SDK | (Obligatoriskt)<br/><br/>Kapitlets unika ID. Detta värde beräknas automatiskt utifrån följande formel: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:ström:kapitel_pos | ChapterInfo | (Obligatoriskt)<br/><br/>Kapitlets index i listan med kapitel (med början från 1). |
| l:ström:kapitelförskjutning | ChapterInfo | (Obligatoriskt)<br/><br/>Kapitlets förskjutning (uttryckt i sekunder) inuti huvudinnehållet, exklusive annonser. |
| l:ström:kapitellängd | ChapterInfo | (Obligatoriskt)<br/><br/>Kapitlets längd (uttryckt i sekunder). |
| s:meta:custom_chapter_metadata.x | ChapterInfo | (Valfritt)<br/><br/>Anpassade kapitelmetadata. |

## Sessionsslutshändelse

| Namn | Datakälla | Beskrivning |
| ---  | --- | --- |
| s:event:type=end | Media SDK | (Obligatoriskt)<br/><br/> `end``close` |


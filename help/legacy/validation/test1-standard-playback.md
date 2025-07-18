---
title: Test 1 Standard Playback
description: Lär dig mer om standarduppspelningstestet som används vid validering.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Test 1: Standarduppspelning{#test-standard-playback}

Det här testfallet validerar allmän uppspelning och sekvensering.

Implementeringar av Media Analytics omfattar två typer av spårningsanrop:
* Anrop som görs direkt till din Adobe Analytics-server (AppMeasurement) - Dessa anrop sker i händelserna &quot;Media Start&quot; och &quot;Ad Start&quot;.
* Anrop till Media Analytics-servern (hjärtslag) - dessa omfattar in-band- och out-of-band-anrop:
   * In-band - SDK skickar uppspelningsanrop eller&quot;pings&quot; med tio sekunders mellanrum under uppspelningen av innehållet och med en sekund i annonserna.
   * Out-of-band - Dessa samtal kan äga rum när som helst, t.ex. paus, buffring, fel, fullständigt innehåll och slutfört innehåll.

>[!NOTE]
>Mediespårning fungerar likadant på alla plattformar.

## Provningsförfarande

Fyll i och registrera följande åtgärder (i ordning):

1. **Läs in sidan eller appen**

   **Spåra servrar** (för alla webbplatser och mobilappar):

   * **Adobe Analytics-server (AppMeasurement) -** En RDC-spårningsserver eller CNAME som kan matchas till en RDC-spårningsserver krävs för Experience Cloud Visitor ID-tjänsten. Adobe Analytics-spårningsservern ska avslutas med `.sc.omtrdc.net` eller vara en CNAME.

   * **Media Analytics-server (Heartbeats) -** Den här servern har alltid formatet `[namespace].hb.omtrdc.net`, där `[namespace]` anger ditt företagsnamn. Det här namnet tillhandahålls av Adobe.

   Du måste validera vissa nyckelvariabler som är universella för alla spårningsanrop:

   **Adobe Visitor-ID (`mid`):** Variabeln `mid` används för att hämta värdeuppsättningen i AMCV-cookien. Variabeln `mid` är det primära ID-värdet för både webbplatser och mobilappar och anger även att tjänsten Experience Cloud Visitor ID är korrekt konfigurerad. Den finns både i samtal från Adobe Analytics (AppMeasurement) och Media Analytics (hjärtslag).

   * **Adobe Analytics Starta samtal**

     | Parameter | Värde (exempel) |
     |---|---|
     | `pev2` | ms_s |
     | `mid` | 30250035503789876473484580554595324209 |

   * **Anrop till webbsida**

     | Parameter | Värde (exempel) |
     |---|---|
     | `mid` | 30250035503789876473484580554595324209 |

   * **Livscykelanrop**

     | Parameter | Värde (exempel) |
     |---|---|
     | `pev2` | ADBINTERNAL:Lifecycle |
     | `mid` | 30250035503789876473484580554595324209 |

   * **Start-anrop för medieanalys**

     | Parameter | Värde (exempel) |
     |---|---|
     | `s:event:type` | start |

     >[!NOTE]
     >
     >I startsanrop för Media Analytics (`s:event:type=start`) kanske `mid`-värdena inte finns. Det här är okej. De kanske inte visas förrän Media Analytics Play-anropen ( `s:event:type=play`).

   * **Media Analytics Play-anrop**

     | Parameter | Värde (exempel) |
     |---|---|
     | `s:event:type` | play |
     | `s:user:mid` | 30250035503789876473484580554595324209 |

1. **Starta mediespelaren**

   När mediespelaren startas skickar Media SDK nyckelanrop till de två servrarna i följande ordning:

   1. Adobe Analytics-server - Starta samtal
   1. Media Analytics-server - Starta samtal
   1. Media Analytics-server -&quot;Adobe Analytics Start Call requested&quot;

   De två första anropen ovan innehåller ytterligare metadata och variabler. Information om samtalsparametrar och metadata finns i [Testa samtalsinformation.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   Det tredje anropet ovan talar om för Media Analytics-servern att Media SDK har begärt att Adobe Analytics Start-anropet (`pev2=ms_s`) ska skickas till Adobe Analytics-servern.

1. **Visa och bryt om tillgängligt**

   * **Lägg till början**

   När annonsen startar skickas följande nyckelanrop i följande ordning:

   1. Adobe Analytics server - Ad Start-samtal
   1. Media Analytics-server - Ad Start call
   1. Media Analytics-server -&quot;Adobe Analytics Ad Start call requested&quot;

   De första två anropen innehåller ytterligare metadata och variabler. Information om samtalsparametrar och metadata finns i [Testa samtalsinformation.](/help/legacy/validation/test-call-details.md#view-ad-playback)

   Det tredje anropet meddelar Media Analytics-servern att Media SDK har begärt att Adobe Analytics Ad Start-anropet (`pev2=msa_s`) ska skickas till Adobe Analytics-servern.

   * **Lägg till uppspelning**

     Under annonsuppspelning skickar Media Analytics SDK uppspelningshändelser av typen&quot;ad&quot; till Media Analytics-servern varje sekund.

   * **Ad Complete**

     Vid 100 %-poängen i en annons ska ett fullständigt anrop till Media Analytics skickas.

1. **Pausa och spela upp i 30 sekunder, om tillgängligt.**  **Lägg till paus**

   Under Ad Pause skickas samtal från SDK till Media Analytics-servern varje sekund med pulsslag eller &quot;ping&quot;.

   >[!NOTE]
   >
   >Spelhuvudets värde ska vara konstant under paus.

   Information om samtalsparametrar och metadata finns i [Testa samtalsinformation.](/help/legacy/validation/test-call-details.md#ma-ad-pause-call)

1. **Spela upp huvudinnehåll i 10 sekunder utan avbrott.**  **Innehållsuppspelning**

   Under uppspelningen av huvudinnehållet skickar Media SDK hjärtslag (uppspelningsanrop) till Media Analytics-servern var 10:e sekund.

   Anteckningar:

   * Spelhuvudets position ska ökas med 10 vid varje uppspelningsanrop.
   * Värdet `l:event:duration` representerar antalet millisekunder sedan det senaste spårningsanropet och bör vara ungefär lika stort för varje 10-sekundersanrop.

     Information om samtalsparametrar och metadata finns i [Testa samtalsinformation.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Pausa under uppspelning i minst 30 sekunder.** När mediespelaren pausas skickas händelseanrop från SDK till Media Analytics-servern var tionde sekund. När pausen är slut bör uppspelningshändelserna återupptas.

   Information om samtalsparametrar och metadata finns i [Testa samtalsinformation.](/help/legacy/validation/test-call-details.md#pause-main-content)

1. **Sök/bläddra bland media.** Vid rensning av mediespelare skickas inga särskilda spårningsanrop, men när medieuppspelningen återupptas efter rensning bör spelhuvudet återspegla den nya positionen i huvudinnehållet.

1. **Spela upp media (endast VOD).** När media spelas upp ska en ny uppsättning med mediestart skickas (som om det var en ny start).

1. **Visa nästa media i spellistan.** Vid mediestart för nästa media i en spellista ska en ny uppsättning mediestart skickas.

1. **Växla media eller ström.** Vid växling av liveströmmar ska ett fullständigt anrop från Media Analytics för den första strömmen inte skickas. Media Start-anropen och Play-anropen ska börja med det nya show- och stream-namnet och med rätt spelhuvud- och varaktighetsvärden för det nya programmet.

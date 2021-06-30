---
title: Test 1 Standard Playback
description: Lär dig mer om standarduppspelningstestet som används vid validering.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Medieanalys
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: 9fc75eb94603238aa85779b5f26f7b7de049dc8f
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Test 1: Standarduppspelning{#test-standard-playback}

Det här testfallet validerar allmän uppspelning och sekvensering.

Implementeringar av Media Analytics omfattar två typer av spårningsanrop:
* Anrop som görs direkt till din Adobe Analytics-server (AppMeasurement) - dessa anrop sker i händelserna &quot;Media Start&quot; och &quot;Ad Start&quot;.
* Anrop till Media Analytics-servern (hjärtslag) - dessa omfattar in-band- och out-of-band-anrop:
   * In-band - SDK skickar uppspelningsanrop eller&quot;pings&quot; med 10 sekunders mellanrum under uppspelning av innehåll och med 1 sekunders mellanrum under annonser.
   * Out-of-band - Dessa samtal kan äga rum när som helst, t.ex. paus, buffring, fel, fullständigt innehåll och slutfört innehåll.

>[!NOTE]
>Mediespårning fungerar likadant på alla plattformar.

## Provningsförfarande

Fyll i och registrera följande åtgärder (i ordning):

1. **Läs in sidan eller appen**

   **Spåra servrar**  (för alla webbplatser och mobilappar):

   * **Adobe Analytics-server (AppMeasurement) -** En RDC-spårningsserver eller CNAME som kan matchas till en RDC-spårningsserver krävs för Experience Cloud Visitor ID-tjänsten. Adobe Analytics-spårningsservern ska avslutas med `.sc.omtrdc.net` eller vara en CNAME.

   * **Media Analytics-server (Heartbeats) -** Den här servern har alltid formatet&quot;`[namespace].hb.omtrdc.net`&quot;, där  `[namespace]` företagsnamnet anges. Det här namnet tillhandahålls av Adobe.

   Du måste validera vissa nyckelvariabler som är universella för alla spårningsanrop:

   **Adobe Visitor-ID (`mid`):** Variabeln  `mid` används för att hämta det värde som angetts i AMCV-cookien. Variabeln `mid` är det primära ID-värdet för både webbplatser och mobilappar och anger även att Experience Cloud Visitor ID-tjänsten är korrekt konfigurerad. Den finns i både Adobe Analytics-anrop (AppMeasurement) och Media Analytics-anrop (hjärtslag).

   * **Adobe Analytics Start Call**

      | Parameter | Värde (exempel) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 3025003503789876473484580554595324209 |

   * **Webbplatsens sidsamtal**

      | Parameter | Värde (exempel) |
      |---|---|
      | `mid` | 3025003503789876473484580554595324209 |

   * **Livscykelanrop**

      | Parameter | Värde (exempel) |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 3025003503789876473484580554595324209 |

   * **Starta samtal med Media Analytics**

      | Parameter | Värde (exempel) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >I startsanrop för Media Analytics (`s:event:type=start`) kanske inte `mid`-värdena finns. Det här är okej. De kanske inte visas förrän Media Analytics Play-anropet ( `s:event:type=play`).

   * **Media Analytics Play-samtal**

      | Parameter | Värde (exempel) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 3025003503789876473484580554595324209 |


1. **Starta mediespelaren**

   När mediespelaren startas skickar Media SDK nyckelanropen till de två servrarna i följande ordning:

   1. Adobe Analytics-server - Starta samtal
   1. Media Analytics-server - Starta samtal
   1. Media Analytics-server -&quot;Adobe Analytics Start Call requested&quot;

   De två första anropen ovan innehåller ytterligare metadata och variabler. Information om anropsparametrar och metadata finns i [Testa samtalsinformation.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Det tredje anropet ovan talar om för Media Analytics-servern att Media SDK har begärt att Adobe Analytics Start-anropet (`pev2=ms_s`) ska skickas till Adobe Analytics-servern.

1. **Visa och bryt om det finns**

   * **Annonsstart**

   När annonsen startar skickas följande nyckelanrop i följande ordning:

   1. Adobe Analytics server - Ad Start-samtal
   1. Media Analytics-server - Ad Start-anrop
   1. Media Analytics-server -&quot;Adobe Analytics Ad Start call requested&quot;

   De första två anropen innehåller ytterligare metadata och variabler. Information om anropsparametrar och metadata finns i [Testa samtalsinformation.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   Det tredje anropet meddelar Media Analytics-servern att Media SDK har begärt att Adobe Analytics Ad Start-anropet (`pev2=msa_s`) ska skickas till Adobe Analytics-servern.

   * **Annonsuppspelning**

      Under annonsuppspelning skickar Media Analytics SDK uppspelningshändelser av typen&quot;ad&quot; till Media Analytics-servern varje sekund.

   * **Ad Complete**

      Vid 100 %-poängen i en annons ska ett fullständigt anrop till Media Analytics skickas.



1. **Pausa och spela upp i 30 sekunder, om tillgängligt.**   **Annonspaus**

   Under en paus i annonsen skickas anrop till pulsslag eller &quot;ping&quot; från Media Analytics av SDK till Media Analytics-servern varje sekund.

   >[!NOTE]
   >
   >Spelhuvudets värde ska vara konstant under paus.

   Information om anropsparametrar och metadata finns i [Testa samtalsinformation.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Spela upp huvudinnehållet i 10 sekunder utan avbrott.**   **Innehållsuppspelning**

   Under uppspelningen av huvudinnehållet skickar Media SDK hjärtslag (uppspelningsanrop) till Media Analytics-servern var 10:e sekund.

   Anteckningar:

   * Spelhuvudets position ska ökas med 10 vid varje uppspelningsanrop.
   * Värdet `l:event:duration` representerar antalet millisekunder sedan det senaste spårningsanropet och bör vara ungefär samma värde för varje 10-sekundersanrop.

      Information om anropsparametrar och metadata finns i [Testa samtalsinformation.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Pausa under uppspelning i minst 30 sekunder.** När mediespelaren pausas skickas händelseanrop från SDK till Media Analytics-servern var 10:e sekund. När pausen är slut bör uppspelningshändelserna återupptas.

   Information om anropsparametrar och metadata finns i [Testa samtalsinformation.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Sök/bläddra i media.** Vid rensning av mediespelare skickas inga särskilda spårningsanrop, men när mediespelningen återupptas efter rensning bör spelhuvudets värde återspegla den nya positionen i huvudinnehållet.

1. **Spela upp media (endast VOD).** När media spelas upp ska en ny uppsättning med mediestart skickas (som om det var en ny start).

1. **Visa nästa media i spellistan.** När media börjar på nästa media i en spellista, ska en ny uppsättning med Media Start-anrop skickas.

1. **Växla media eller ström.** När direktuppspelningar byts ut ska ett fullständigt anrop från Media Analytics för den första strömmen inte skickas. Media Start-anropen och Play-anropen ska börja med det nya show- och stream-namnet och med rätt spelhuvud- och varaktighetsvärden för det nya programmet.

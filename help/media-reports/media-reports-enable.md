---
title: Aktivera medierapporter
description: Läs mer om medierapportsviten som samlar in mediestatistik.  Följ de här stegen för att konfigurera medierapporter innan mediedata skickas.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 1682a10a1d24e55854a77a8f44b43f92893adaa2
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 1%

---

# Aktivera medierapporter{#media-reports-enablement}

Varje rapportsvit som samlar in mediemätningar måste konfigureras innan mediedata skickas.

Avancerade kunder kan bara använda mediepanelerna i Analysis Workspace efter att Media Core har aktiverats och spårning har aktiverats för [Upplevelsekvalitet](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/track-qos/track-qos-overview.html?lang=en).

>[!TIP]
>
>För att kunna utnyttja de nya funktionerna bör befintliga Media Analytics-kunder återaktivera mediespårning för sina RSID.

1. I [Rapporter och analyser](https://my.omniture.com/login/) klicka **[!UICONTROL Admin > Report Suites].**
1. Markera de rapportsviter där du samlar in mediedata och klicka på **[!UICONTROL Edit Settings > Media Management > Media Reporting].**

   ![](assets/media-reporting.png){width="400px"}

1. På **[!UICONTROL Media Reporting]** sida, aktivera **[!UICONTROL Media Core],** och aktivera **[!UICONTROL Media Ads],** **[!UICONTROL Media Chapters],** och **[!UICONTROL Media Quality].**

   Mediemätningen innehåller följande moduler:

   * **Media Core**

      Huvudmediemätning används för medieinnehåll. Detta använder Solution (eller Custom) eVars för att hålla reda på innehåll, innehållstyp, innehållspelarens namn och innehållskanal. Lösningshändelser (eller anpassade händelser) kommer att användas för Media Starts, Content Starts, Content Completes och Content Time Spent.

   * **Media Ads**

      Mätning av mediereklam används för mätning av annonser i medieinnehållet. Här används Solution Vvars för att mäta Ad, Ad Player Name, Ad Pod och Ad i Pod Position. Lösningshändelser kommer att användas för annonsstart, Ad Completes, Ad Time Spent och Video Time Spent.

   * **Mediekretsar**

      Mätning av videokapitel används för mätning av kapitel. Ett kapitel är en underindelning av innehållet i ett enda medium. Detta använder en Solution-eVar för att lagra kapitel-ID:t. Lösningshändelser används för kapitelstart, kapitelslutföranden och kapiteltid som används. Ytterligare kapitelmetadata för kapitelnamn och kapitelposition kommer att tillhandahållas som klassificeringar av kapitel-ID.

   * **Mediekvalitet**

      Videokvalitetsmätning används för att mäta innehållets kvalitet vid uppspelning. Detta använder Solution eVars för att lagra tid för start, bufferthändelser, total buffertvaraktighet, växlar för bithastighet, genomsnittlig bithastighet, fel och uteslutna bildrutor. Lösningshändelser kommer att användas för Tid att starta, Drops före start, Buffer-påverkade strömmar, Buffer Events, Total Buffer Duration, Bitrate Change Impached Streams, Bitrate Changes, Meg Bitrate, Error Impact Streams, Error Events, Dropped Frame Impached Streams och Dropped Frames.

   * **Video- och videoredigeringsmetadata**

      Metadata kan bifogas till ett medium och/eller en annons för att ytterligare beskriva och kategorisera mediet/annonsen. Standardiserade medier och annonseringsmetadata samlas in via lösningens variabler och klassificeringar. Värden som ska inkluderas: Visa, Säsong, Episod, Tillgångs-ID, Generera, Första AIR-datum, Första digitala datum, Innehållsklassificering, Originator, Nätverk, Visa typ, Annonsinläsningar, MVPD, Auktoriserad, Dag-del, Media Session ID, Advertiser, Campaign-ID och Creative-ID.

   * **Metadata för ljud- och ljudannonsering**

      Metadata kan bifogas till ljud och/eller en annons för att ytterligare beskriva och kategorisera ljudet/annonsen. Standardiserade ljud- och annonsmetadata samlas in via lösningsvariabler och -klassificeringar. Värden som ska inkluderas: Artist, Album, Etikett, Författare, Utgivare, Station, Show, Season, Episod, Asset ID, Genre, First Air Date, First Digital Date, Content Rating, Originator, Show Type, Ad Loads, Day Part, Media Session ID, Advertiser, Campaign ID och Creative ID.
   När du aktiverar varje modul reserveras en uppsättning variabler och en ny uppsättning rapporter skapas. Med undantag för Kvalitet finns det inga data i rapporter såvida inte motsvarande implementering har slutförts. När du implementerar kärnmodulen implementeras även kvalitetsmodulen om du aktiverar den.

   Om du ännu inte håller på att spåra annonser, kapitel eller uppspelningskvalitet kan du när som helst aktivera ytterligare alternativ.

1. Klicka på **[!UICONTROL Save].**

   Om den här rapportsviten redan har konfigurerats för att samla in mediedata klickar du på **[!UICONTROL Save]** visas ytterligare en konfigurationssida. Om du ser **[!UICONTROL Media Core measurement]** fortsätter du till nästa steg.

1. (Villkorligt) På **[!UICONTROL Media Core measurement]** väljer du att fortsätta använda anpassade variabler eller väljer att använda lösningsvariabler.

   | Alternativ | Anteckningar |
   | --- | --- |
   | Fortsätt använda anpassade variabler | Pros and Cons:<ul> <li> **Pros:** Innehållstrendningen fortsätter att fungera efter migreringen. </li> <li> **Kon:** Kräver att du behåller två anpassade eVars-variabler och tre anpassade händelser som tilldelats media. Du återanvänder en anpassad eVar och en anpassad händelse. </li> </ul> Så här fortsätter du använda anpassade variabler: <ol> <li>Välj **[!UICONTROL Use Custom Variables,]** sedan klicka **[!UICONTROL Save.]** </li> <li>Mappa aktuella anpassade e-variabler och händelser när du uppmanas till det och klicka sedan på **[!UICONTROL Save:]** </li> </ol> |
   | Migrera till lösningsvariabler | Pros and Cons:<ul> <li> **Pros:** Du återanvänder tre anpassade eVars-variabler och fyra anpassade händelser. </li> <li> **Kon:** Du förlorar **alla** historisk trender och jämförelse för medierapporter. Det innebär att du inte kan trenda innehållsvyer eller den innehållstid som spelas upp för datum innan du migrerar till pulsslag. </li> </ul> **Begränsning:**  Migrera inte till lösningsvariabler om du inte är säker på att du inte vill bevara trendningen. Alla kunder bör använda lösningens variabler och bearbetningsregler för att lägga in mediedata i befintliga props och eVars endast om de behöver bevara den historiska kontinuiteten. Så här migrerar du till lösningsvariabler: Välj **[!UICONTROL Use Solution Variables]** och klicka **[!UICONTROL Save].** <br><br> VIKTIGT! Om du migrerar till lösningens variabler förlorar du **alla** historisk trender och jämförelse för medierapporter. |

>[!IMPORTANT]
>
>Ändra inte klassificeringsnamnen för variabler som listas i Metrics and metadata tables (t.ex. [Parametrar för ljud och video](/help/metrics-and-metadata/audio-video-parameters.md)) som beskrivs där under Rapportering/Reserverad variabel som&quot;klassificering&quot;. Medieklassificeringarna definieras när en rapportsserie aktiveras för mediespårning. Ibland lägger Adobe till nya egenskaper, och när detta inträffar måste kunderna aktivera sina rapporteringsprogram på nytt för att få tillgång till de nya medieegenskaperna. Under uppdateringsprocessen avgör Adobe om klassificeringarna är aktiverade genom att kontrollera namnen på variablerna. Om någon av dem saknas lägger Adobe till de saknade igen.

---
title: Uppdatera en implementering av en anslutning till en Analytics-källa till nya XDM-fält för direktuppspelande medietjänster
description: Lär dig hur du migrerar en implementering av en Analytics-källanslutning till uppdaterade XDM Streaming Media-fält
feature: Streaming Media
role: User, Admin, Developer
exl-id: d239b203-71ce-4307-884f-9d11cc623d04
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Uppdatera en implementering av en anslutning till en Analytics-källa till nya XDM-fält för direktuppspelande medietjänster

>[!NOTE]
>
>Den här informationen är avsedd för organisationer som använder [Analytics-källkopplingen](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/adobe-applications/analytics) för att överföra direktuppspelade mediedata från Adobe Analytics till Adobe Experience Platform för användning med Customer Journey Analytics-rapportering eller någon annan plattformstjänst.
>
>Ändringarna påverkar inte Adobe Analytics som ett fristående program, inklusive datainsamling, bearbetning och rapportering. Verktyg som Dataflöden och Bearbetningsregler påverkas inte, så inga uppdateringar av Analytics-implementeringen krävs.

Nu finns en ny implementering av Adobe Data Collection (Analytics Source Connector) för tjänsten för direktuppspelande media som migrerar från en uppsättning XDM-fält till en annan.

## Ny sökväg till XDM-fält

Som en del av den här migreringen lades sökvägen `mediaReporting` till i XDM-scheman som används i Adobe Data Collection-flöden (Analytics-källkoppling). Alla befintliga och nyligen genererade Adobe Data Collection-scheman kommer automatiskt att inkludera det nya fältet.

## Ersättning av den gamla XDM-fältsökvägen

Alla flöden för Adobe Data Collection (källanslutning för analys) som överför strömmande mediedata från Adobe Analytics till Adobe Experience Platform skickar för närvarande data både på den nya `mediaReporting` XDM-fältsökvägen och den gamla `media.mediaTimed` XDM-fältsökvägen. Båda dessa fältsökvägar kommer att vara tillgängliga i tre månader fram till slutet av oktober 2025. Efter oktober kommer fälten `media.mediaTimed` att vara helt inaktuella och data som hämtas efter oktober kommer endast att innehålla `mediaReporting`. Efter borttagning kommer `media.mediaTimed`-fälten inte längre att vara synliga i Adobe Experience Platform-schemagränssnittet och datainmatningen för dessa fält kommer att stoppas. Därför kommer dessa fält inte längre att vara tillgängliga för användning i någon Adobe Experience Platform-tjänst.

Data som har importerats före detta datum är fortfarande tillgängliga för rapportering.

## Ytterligare skillnader med den nya sökvägen för XDM-fältet

I och med den nya implementeringen av Adobe källanslutning för direktuppspelande media, hämtas samtal från Adobe Analytics till Adobe Experience Platform.

Tidigare reflekterades inte dessa samtal i plattformsappar som Customer Journey Analytics. Som ett resultat av detta kan din organisation observera följande skillnader i rapporteringen:

* **Korrekt antal sessioner**: I vissa fall kan det betyda tömning av antalet sessioner, eftersom samtal som hålls aktiva hjälper till att upprätthålla aktiva användarsessioner även utan direktmediainteraktioner. Dessa samtal genereras var 20:e minut efter den senaste händelsen, per mediauppspelning, med avsikten att hålla besöket öppet. För att säkerställa optimal sessionsspårning i Customer Journey Analytics rekommenderar vi att du konfigurerar besökets förfallotid till 30 minuter i datavyn.

* **En ökning av antalet händelser**: Eftersom samtal som är aktiva vid uppehåll nu räknas i Customer Journey Analytics-händelsemätaren. Om du vill utesluta samtal som håller sig aktiva från rapporteringen kan du skapa ett filter som utesluter händelser som har händelsetypen `media.keepalive`.

Den här förändringen säkerställer bättre överensstämmelse mellan analyser och CJA-rapporter.

## Migrera din befintliga konfiguration

För att övergången ska bli smidig måste alla kunder migrera befintliga inställningar från `media.mediaTimed`-fält till `mediaReporting`-fält före utgången av oktober 2025. De berörda områdena är de som är beroende av `media.mediaTimed`-användning och bör migreras enligt anvisningarna i följande avsnitt.

### Customer Journey Analytics**

Det finns två sätt att migrera CJA-rapporter:

>[!NOTE]
>
>När du har valt något av följande alternativ måste du manuellt ersätta varje `media.mediaTimed`-fält som används i Customer Journey Analytics-rapporter med motsvarande härlett fält eller rapportens XDM-fältsökväg.

* **För att bevara historiska data**: Adobe-team har utvecklat en fördefinierad Customer Journey Analytics-mall som innehåller en uppsättning härledda fält som kombinerar gamla och nya XDM-fält till ett enda fält. Den här mallen kan aktiveras per Customer Journey Analytics-anslutning på begäran. Kontakta Adobe supportteam för att få hjälp med att aktivera de nya fälten. Dessa härledda fält räknas inte med i organisationens härledda fältgräns.

  En lista över mappningar finns i [Parametermappning för Media Analytics för Adobe Experience Platform och Customer Journey Analytics](/help/use-cases/xdm-updates/parameters-mapping.md).

* **Om historiska data inte krävs**: Det räcker att använda rapportens XDM-fältsökväg vid rapporttidpunkten. Mer information finns i [Migrera Customer Journey Analytics för att använda de nya direktuppspelningsmediefälten](/help/use-cases/xdm-updates/migrate-cja-setup.md).

### Real-Time CDP

Alla publiker och profiler måste baseras på `mediaReporting`. Mer information finns i [Migrera profiler till nya fält för direktuppspelande media](/help/use-cases/xdm-updates/migrate-profiles.md).

### Dataström och datainsamling

Dynamiska konfigurationer och datamappning måste använda `mediaReporting`. Mer information finns i [Migrera dataförberedelse för anpassade fält till de nya direktuppspelningsmediefälten](/help/use-cases/xdm-updates/migrate-dataprep.md).

### Andra tjänster som måste migreras

* Adobe Journey Optimizer: Kampanjkonfigurationer och resekonfigurationer måste innehålla `mediaReporting`.

* Händelsevidarebefordran: Endast `mediaReporting` fält ska inkluderas i konfigurationer.

* Frågetjänster: Frågor måste referera till `mediaReporting` fält.

* Tagginställningar: Alla tagginställningar ska referera till `mediaReporting` fält.

* Anslutningar och mål: Importera och exportera dataflöden ska struktureras runt `mediaReporting` fält.

Observera att alla andra flöden som är beroende av `media.mediaTimed`-fält påverkas och kräver logiska uppdateringar.

## Nästa steg och support

Alla kunder som använder Adobe Data Collection för Streaming Media måste slutföra migreringen inom den angivna övergångsperioden.

Om du har några frågor eller behöver support går du inte miste om chansen att kontakta Adobe supportteam.

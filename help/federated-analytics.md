---
title: Federated Analytics
description: 'Tjänsten Federated Analytics är ett system för att dela Adobe Media Analytics-data (ljud och video) mellan två partner. '
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Federated Analytics{#federated-analytics}

Tjänsten Federated Analytics är ett system för att dela Adobe Media Analytics-data (ljud och video) mellan två partner.
De standardiserade mätdata som skapas med Media Analytics är ett kännetecken för Federated Analytics, vilket gör att samma data kan flöda in i en enda rapport från flera olika källor.
Tack vare de regler och den logik som styr Federated Analytics kan data enkelt styras och personaliseras för att uppfylla behoven i varje partnerskap.
Med Federated Analytics blir ljud- och videomätningarna effektivare, smidigare och mer användbara.

## Fördelar {#benefits}

* **Genomskinlig:** Ta bort den svarta rutan med data som skapats med samma logik i olika företag
* **Bred:** Förstå den fulla räckvidden och effekten av ljud- och videokonsumtion i partnerskap, plattformar och enheter
* **Säker:** Styr datadelning på serversidan med hjälp av regler och logik
* **Standardiserad:** Tala samma dataspråk som era partners
* **Användbar:** Mät ljud- och videodata för att testa spelare, övervaka trender och upptäcka avvikelser med Adobe Analytics
* **Centraliserad:** Samla in ljud- och videomätningsdata på en och samma Adobe-plats
* **Contractual:** Uppfyll enkelt kraven på datautbyte inom juridik
* **Lämplig:** Skicka och ta emot data i nära realtid
* **Enkelt:** Tagga spelare en gång med Adobe SDK:er, dela data med många partners

## Definitioner {#definitions}

* **Avsändare:** Kunden genererar ljud- och videoanalysdata för egna spelare
* **Mottagare:** Kunden tar emot ljud- och videoanalysdata från avsändaren

## Krav {#requirements}

* **Medieströmskontrakt:** Mottagaren och avsändaren måste ha ingått avtal med Adobe Analytics för medieströmmar innan de får tillgång till ljud- och videodata i Adobe Analytics. Kontakta ditt kontoteam om du vill ha mer information.
* **Federated Addendum:** Varje avsändare och mottagare måste ha ett signerat tillägg till Adobe innan data skickas eller tas emot. Ett tillägg per kund krävs, inte ett tillägg per partnerskap. Kontakta ditt kontoteam om du vill ha mer information.
* **Implementering av medieanalys:** Avsändaren måste ha Media Analytics implementerat för alla spelare som ska ingå i den federerade datauppsättningen. Endast Media Analytics-data är tillgängliga för federation. Se dokumentationen: Mäta [ljud och video i Adobe Analytics](/help/media-overview.md)

* **Adobe Consulting Contract:** För den första konfigurationen av federerade regler mellan mottagare och avsändare är det värdefullt att arbeta med konsulttjänster för att granska data och skapa datadelningsavtalet.

## Hämta Federated Analytics-formuläret

Hämta den aktuella versionen av det här formuläret här: [Federationsregelavtal](https://github.com/AdobeDocs/media-analytics.en/blob/master/help/federated-analytics-form.pdf)

## Process {#process}

1. Avsändare och mottagare arbetar tillsammans för att fylla i formuläret för federationsregelavtal. Formuläret för Federated Rules Agreement innehåller specialfält för våra tekniker och ska ENDAST redigeras med Adobe Acrobat. [Ladda ned Acrobat utan kostnad.](https://get.adobe.com/reader/)
1. Konsulttjänster tillhandahåller en exempeldatafil till mottagaren med faktiska data från avsändarspelare för att ytterligare bekräfta att korrekta regler för datadelning har definierats, förutsatt att datafiler finns tillgängliga.
1. Avsändaren och mottagaren ser till att datadelningsavtalet uppfyller alla avtalsmässiga krav mellan de båda parterna.
1. Konsulttjänster skickar det ifyllda formuläret till Adobe Engineering för att skapa regler för datadelning.
1. Data delas med utvecklingsrapportsviten där mottagaren granskar och validerar data.
1. När mottagaren har bekräftat att data är korrekta uppdaterar Adobe Engineering reglerna till att peka på en produktionsrapportsvit.
1. Mottagaren granskar och validerar data i produktionsrapportsviten.
1. Om datauppsättningen ändras i framtiden kan avsändaren eller mottagaren skicka in en kundtjänstanmälan för support.


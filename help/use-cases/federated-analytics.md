---
title: Federated Analytics
description: Federated Analytics-tjänsten tillhandahåller ett system för delning av strömmande mediedata mellan två partners.
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
exl-id: 81970370-663c-49d5-b13c-628d294be178
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 77%

---

# Federated Analytics{#federated-analytics}

Federated Analytics-tjänsten tillhandahåller ett system för delning av strömmande mediedata (ljud och video) mellan två partners.
De standardiserade mätdata som skapas av tillägget Streaming Media Collection är ett kännetecken för Federated Analytics, vilket gör att samma data kan flöda in i en enda rapport från flera olika källor.
Tack vare de regler och den logik som styr Federated Analytics kan data enkelt styras och personaliseras för att uppfylla behoven för varje partner.
Med Federated Analytics blir ljud- och videomätningarna effektivare, smidigare och mer användbara.

## Fördelar {#benefits}

* **Genomskinligt:** Avmystifiera dataskapande genom att använda samma logik i flera företag
* **Bredd:** Förstå den fulla räckvidden och effekten av ljud- och videokonsumtion för olika partnerskap, plattformar och enheter
* **Säkert:** Styr datadelning på serversidan med hjälp av regler och logik
* **Standardiserat:** Tala samma dataspråk som era partners
* **Verkställbart:** Mät ljud- och videodata för att testa spelare, övervaka trender och upptäcka avvikelser med Adobe Analytics
* **Centraliserat:** Samla in ljud- och videomätningsdata på en och samma Adobe-plats
* **Avtalsenligt:** Uppfyll enkelt de juridiska kraven på datadelning
* **Tidsanpassat:** Skicka och ta emot data i nära realtid
* **Enkelt:** Tagga spelare en gång med Adobes SDK:er och dela data med flera partners

## Definitioner {#definitions}

* **Avsändare:** Kunden som genererar ljud- och videoanalysdata för egna spelare
* **Mottagare:** Kunden som tar emot ljud- och videoanalysdata från avsändaren

## Krav {#requirements}

* **Avtal om medieströmmar:** Mottagaren och avsändaren måste ha ingått avtal med Adobe Analytics för medieströmmar innan de får tillgång till ljud- och videodata i Adobe Analytics. Kontakta ditt kontoteam om du vill ha mer information.
* **Federationstillägg:** Varje avsändare och mottagare måste ha undertecknat ett tillägg med Adobe innan data skickas eller tas emot. Ett tillägg per kund krävs, inte ett tillägg per partnerskap. Kontakta ditt kontoteam om du vill ha mer information.

* **Implementering av tillägget för direktuppspelad mediainsamling:** Avsändaren måste ha tillägget Streaming Media Collection implementerat på alla spelare som ska ingå i den federerade datauppsättningen. Endast direktuppspelande mediedata är tillgängliga för federation. Mer information finns i [Adobe Streaming Media Collection - översikt](/help/media-overview.md).

* **Konsultavtal med Adobe:** Vid den inledande konfigureringen av regler för federering är det praktiskt att samarbeta med våra konsulter för att granska data och skapa datadelningsavtalet.

## Hämta Federated Analytics-formuläret

Om du vill delta i Federated Analytics hämtar och fyller du i [Federationsregelavtal](assets/federated_analytics_form.pdf) formulär.

## Process {#process}

1. Avsändare och mottagare arbetar tillsammans för att slutföra avtalet om regler för federering. Avtalsformuläret om regler för federering innehåller specialfält för våra tekniker och ska ENDAST redigeras med Adobe Acrobat. [Ladda ned Acrobat utan kostnad.](https://get.adobe.com/se/reader/)
1. Mottagaren får en exempeldatafil från konsulttjänsten som innehåller faktiska data från avsändarens spelare för att bekräfta att rätt regler för datadelning har definierats, förutsatt att datafiler finns tillgängliga.
1. Avsändaren och mottagaren ser till att datadelningsavtalet uppfyller alla avtalsmässiga krav mellan de båda parterna.
1. Konsulttjänsten skickar det ifyllda formuläret till Adobes tekniker som skapar regler för datadelning.
1. Data delas i utvecklingsrapportsviten där mottagaren granskar och validerar data.
1. När mottagaren har bekräftat att data är korrekta uppdaterar Adobes tekniker reglerna till att peka på en produktionsrapportsvit.
1. Mottagaren granskar och validerar data i produktionsrapportsviten.
1. Om datauppsättningen ändras i framtiden kan avsändaren eller mottagaren kontakta supporten genom att skicka en supportbegäran.

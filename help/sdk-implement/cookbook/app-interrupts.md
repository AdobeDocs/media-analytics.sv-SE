---
title: Hantera programavbrott under uppspelning
description: Hur du hanterar avbrott för spårning under uppspelning av media.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: 29b0d38e904a561d467ba0432b255fdb17d6b829
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---


# Hantera programavbrott under uppspelning{#handling-application-interrupts-during-playback}

Uppspelning i ett medieprogram kan avbrytas på flera olika sätt: en användare uttryckligen trycker på paus eller när en användare placerar programmet i bakgrunden. Oavsett vad som orsakar ett avbrott i uppspelningen av media är spårningsinstruktionerna desamma:

1. Ring **`trackPause`** när programmet avbryts (går till bakgrund, mediepaus osv.).
1. Ring **`trackPlay`** när programmet återgår till förgrunden och/eller mediet återupptar uppspelningen.

>[!NOTE]
>
>Media Analytics-teamet har sett fall där kunder har ringt `trackSessionStart` när deras app returnerades från bakgrunden. Om du gör det kommer uppspelningen fram till den punkten inte att räknas med i den totala uppspelningstiden, samtidigt som tidigare förloppsmarkörer, segment och så vidare går förlorade. Ring i stället `trackPlay` när appen returnerar och/eller mediet återupptar uppspelningen.

## Vanliga frågor och svar om hantering av programavbrott: {#faq-about-handling-application-interrupts}

* _Hur lång tid ska en app vara tillbaka innan sessionen stängs?_

   Om programmet tillåter uppspelning av bakgrunden kan det fortsätta spåra genom att anropa våra API:er, och vi skickar alla våra vanliga spårningspapper. Det är inte många videoappar som tillåter uppspelning av bakgrunden förutom YouTube Red, men det är tillåtet för alla ljudappar. Om programmet inte tillåter uppspelning av bakgrunden bör du stanna i pausläge i en minut och sedan avsluta spårningssessionen. Programmet kan inte fortsätta att skicka pausmeddelanden eftersom det i de flesta fall inte går att avgöra om användaren ska återgå till att fortsätta visa mediet eller avgöra när det ska avlivas. Det är också en dålig upplevelse att fortsätta skicka saker i bakgrunden.

* _Vilket är det rätta sättet att hantera återstart av spårning efter att appen har legat i bakgrunden under lång tid?_

   Ansökan bör anropa `trackSessionEnd` för att avsluta spårningssessionen. Från version 2.1 skickar SDK en &quot;end&quot;-ping för att meddela backend att spårningssessionen är stängd.

* _Hur är det med att starta om samma session?_

   Mer information om hur du startar om en spårningssession finns på den här sidan: [Återuppta en tidigare stängd session manuellt](/help/sdk-implement/cookbook/resuming-inactive.md). SDK skickar en återupptagningsping för att meddela backend att användaren återupptar sessionen manuellt.


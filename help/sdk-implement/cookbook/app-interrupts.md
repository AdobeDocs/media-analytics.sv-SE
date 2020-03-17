---
title: Hantera programavbrott under uppspelning
description: Hantera avbrott i spårningen under uppspelning av media.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Hantera programavbrott under uppspelning{#handling-application-interrupts-during-playback}

Uppspelning i ett medieprogram kan avbrytas på flera olika sätt: en användare uttryckligen trycker på paus eller när en användare placerar programmet i bakgrunden. Oavsett vad som orsakar avbrott i medieuppspelningen är spårningsinstruktionerna samma:

1. Anropa **`trackPause`** när programmet avbryts (går till bakgrunden, mediapaus osv.).
1. Anropa **`trackPlay`** när programmet återgår till förgrunden och/eller mediet återupptar uppspelningen.

>[!NOTE]
>
>Medieanalysteamet har sett instanser där kunderna ringde `trackSessionStart` när deras app returnerades från bakgrunden. Detta resulterar i att uppspelningen fram till den punkten inte räknas med i den totala uppspelningstiden, samtidigt som tidigare förloppsindikatorer, segment osv. går förlorade. Ring i stället `trackPlay` när appen returnerar och/eller mediet återupptar uppspelningen.

## Vanliga frågor om hantering av programavbrott: {#faq-about-handling-application-interrupts}

* _Hur länge ska en app vara bakgrundsbelagd innan sessionen stängs?_

   Om programmet tillåter uppspelning i bakgrunden kan det fortsätta spåra genom att anropa våra API:er, och vi skickar alla våra vanliga spårningsmeddelanden. Det är inte många videoprogram som tillåter bakgrundsuppspelning förutom YouTube Red, men detta tillåts i alla ljudappar. Om programmet inte tillåter uppspelning i bakgrunden bör du stanna i pausläget i en minut och sedan avsluta spårningssessionen. Programmet kan inte fortsätta skicka pausade pingar eftersom det i de flesta fall inte går att avgöra om användaren kommer att fortsätta att visa mediet eller avgöra när det kommer att tas bort. Det är också en dålig upplevelse att fortsätta skicka ping i bakgrunden.

* _Vilket är det rätta sättet att hantera omstartsspårning efter att appen har funnits i bakgrunden länge?_

   Programmet bör anropa `trackSessionEnd` för att avsluta spårningssessionen. Från och med version 2.1 skickar SDK en&quot;end&quot;-pinga för att meddela back-end-servern att spårningssessionen är stängd.

* _Hur är det med att starta om samma session?_

   Detaljerade instruktioner om hur du startar om en spårningssession finns på den här sidan: Återuppta en tidigare stängd session [manuellt.](/help/sdk-implement/cookbook/resuming-inactive.md) SDK skickar ett återupptagningsförsök för att meddela backend-servern att användaren återtar sessionen manuellt.


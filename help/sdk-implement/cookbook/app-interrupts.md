---
title: Hantera programavbrott under uppspelning
description: Lär dig hur du hanterar avbrott i spårning under uppspelning av media.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---

# Hantera programavbrott under uppspelning{#handling-application-interrupts-during-playback}

Uppspelning i ett medieprogram kan avbrytas på flera olika sätt: en användare uttryckligen trycker på paus eller när en användare placerar programmet i bakgrunden. Oavsett vad som orsakar avbrott i medieuppspelningen är spårningsinstruktionerna samma:

1. Anropa **`trackPause`** när programmet avbryts (går till bakgrunden, mediapaus osv.).
1. Anropa **`trackPlay`** när programmet återgår till förgrunden och/eller mediet återupptar uppspelningen.

>[!NOTE]
>
>Medieanalysteamet har sett instanser där kunderna ringde `trackSessionStart` när deras app returnerades från bakgrunden. Detta resulterar i att uppspelningen fram till den punkten inte räknas med i den totala uppspelningstiden, tillsammans med att tidigare förloppsindikatorer, segment osv. går förlorade. Ring i stället `trackPlay` när appen returnerar och/eller mediet återupptar uppspelningen.

## Vanliga frågor om hantering av programavbrott: {#faq-about-handling-application-interrupts}

* _Hur länge ska en app vara bakgrundsbelagd innan sessionen stängs?_

   Om programmet tillåter uppspelning i bakgrunden kan det fortsätta spåra genom att anropa våra API:er, och vi skickar alla våra vanliga spårningsmeddelanden. Det är inte många videoprogram som tillåter bakgrundsuppspelning förutom YouTube Red, men det kan alla ljudappar göra. Om programmet inte tillåter uppspelning i bakgrunden bör du stanna i pausläget i en minut och sedan avsluta spårningssessionen. Programmet kan inte fortsätta skicka pausade pingar eftersom det i de flesta fall inte går att avgöra om användaren kommer att fortsätta att visa mediet eller avgöra när det kommer att tas bort. Det är också en dålig upplevelse att fortsätta skicka ping i bakgrunden.

* _Vilket är det rätta sättet att hantera omstartsspårning efter att appen har funnits i bakgrunden länge?_

   Programmet ska anropa `trackSessionEnd` för att avsluta spårningssessionen. Från och med version 2.1 skickar SDK en&quot;end&quot;-pinga för att meddela back-end-servern att spårningssessionen är stängd.

* _Hur är det med att starta om samma session?_

   Detaljerade instruktioner om hur du startar om en spårningssession finns på den här sidan: [Återuppta en tidigare stängd session](/help/sdk-implement/cookbook/resuming-inactive.md) manuellt. SDK skickar ett återupptagningsförsök för att meddela backend-servern att användaren återtar sessionen manuellt.

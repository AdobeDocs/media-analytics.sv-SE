---
title: Hantera programavbrott under uppspelning
description: Lär dig hur du hanterar avbrott i spårning under uppspelning av media.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Hantera programavbrott under uppspelning{#handling-application-interrupts-during-playback}

Uppspelning i ett medieprogram kan avbrytas på flera olika sätt. En användare kan t.ex. uttryckligen trycka på paus eller placera programmet i bakgrunden. Oavsett vad som orsakar avbrott i medieuppspelningen är spårningsinstruktionerna desamma.

1. Anropa **`trackPause`** när programmet avbryts (går till bakgrunden, mediepaus osv.).
1. Anropa **`trackPlay`** när programmet återgår till förgrunden och/eller mediet återupptar uppspelningen.

>[!NOTE]
>
>Om `trackSessionStart` anropas när programmet returneras från bakgrunden kan uppspelningen fram till den punkten inte räknas med i den totala uppspelningstiden, samtidigt som tidigare förloppsmarkörer, segment osv. går förlorade. Ring i stället `trackPlay` när appen returnerar och/eller mediet fortsätter att spela upp.

## Vanliga frågor om hantering av programavbrott: {#faq-about-handling-application-interrupts}

* _Hur länge ska en app vara bakgrundsbelagd innan sessionen avslutas?_

  Om programmet tillåter uppspelning i bakgrunden kan det fortsätta spåra genom att anropa våra API:er, och vi skickar alla våra vanliga spårningsmeddelanden. Det är inte många videoprogram som tillåter bakgrundsuppspelning förutom YouTube Red, men det kan alla ljudappar göra. Om programmet inte tillåter uppspelning i bakgrunden bör du stanna i pausläget i en minut och sedan avsluta spårningssessionen. Programmet kan inte fortsätta skicka pausade pingar eftersom det i de flesta fall inte går att avgöra om användaren kommer att fortsätta att visa mediet eller avgöra när det kommer att tas bort. Det är också en dålig upplevelse att fortsätta skicka ping när det är i bakgrunden.

* _Vilket är det rätta sättet att hantera omstartsspårning efter att appen har funnits i bakgrunden under en lång tid?_

  Programmet ska anropa `trackSessionEnd` för att avsluta spårningssessionen. Från och med version 2.1 skickar SDK en&quot;end&quot;-pinga för att meddela back-end-servern att spårningssessionen är stängd.

* _Vad händer om du startar om samma session?_

  Information om hur du återupptar en spårningssession finns i [Återuppta inaktiva sessioner](resuming-inactive.md). SDK skickar ett återupptagningsförsök för att meddela backend-servern att användaren återtar sessionen manuellt.

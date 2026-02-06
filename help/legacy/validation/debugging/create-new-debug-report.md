---
title: Skapa en ny felsökningsrapport
description: Lär dig skapa en ny felsökningsrapport.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Skapa en ny felsökningsrapport{#create-a-new-debug-report}

Så här skapar du en ny felsökningsrapport:

1. I [!UICONTROL Create New Debug Report] väljer du följande:

   ![](assets/create-new-debug-report.png)

1. Fyll i fälten med följande information:

   * **Namnge rapporten** - Ange spelarens namn och datum så att du enkelt kan spåra spelaren under certifieringen och hålla varumärken och plattformar åtskilda.
   * **Adobe Analytics**

      * [!UICONTROL User Name] och [!UICONTROL Shared Secret] - Dessa fält är valfria, men du kan lägga till dina API-uppgifter för webbtjänster i Adobe Debug för att visa variabelnamnen och variabelinställningarna för rapportsviten.

        Du kommer åt på något av följande sätt:

         * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
         * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] Om du vill skapa en API-autentiseringsuppgift för webbtjänster för en ny användare lägger du till användaren i användargruppen [!UICONTROL User Management] i **Webbtjänståtkomst**.

      * [!UICONTROL Default Endpoint] - Data i det här fältet tillhandahålls av Adobe och kan inte ändras.
      * [!UICONTROL Extra Endpoint] - Lägg till `CNAMES`, om du använder dem, för spårningsserver som `metrics.companyname.com`

   * **Videoberättelser (Media Analytics)**

      * [!UICONTROL Default Endpoint] - Data i det här fältet tillhandahålls av Adobe och kan inte ändras.
      * [!UICONTROL Extra Endpoint] - Lägg till `CNAMES` om du använder dem för spårningsservern, t.ex. `metrics.companyname.com`.

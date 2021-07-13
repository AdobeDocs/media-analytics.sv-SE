---
title: Skapa en ny felsökningsrapport
description: Lär dig hur du skapar en ny felsökningsrapport.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Medieanalys
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 4%

---

# Skapa en ny felsökningsrapport{#create-a-new-debug-report}

Så här skapar du en ny felsökningsrapport:

1. Välj följande i [!UICONTROL Create New Debug Report]:

   ![](assets/create-new-debug-report.png)

1. Fyll i fälten med följande information:

   * **Namnge rapporten** - Ange spelarens namn och datum så att du enkelt kan spåra spelaren under certifieringen och hålla varumärken och plattformar åtskilda.
   * **Adobe Analytics**

      * [!UICONTROL User Name] och  [!UICONTROL Shared Secret] - Dessa fält är valfria, men du kan lägga till dina API-uppgifter för webbtjänster i Adobe Debug för att visa variabelnamnen och variabelinställningarna för rapportsviten.

         Du kommer åt på något av följande sätt:

         * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
         * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] Om du vill skapa en API-autentiseringsuppgift för webbtjänster för en ny användare lägger du till användaren i gruppen  [!UICONTROL User Management]Webbtjänståtkomst  **** för användare i .
      * [!UICONTROL Default Endpoint] - Data i det här fältet tillhandahålls av Adobe och kan inte ändras.
      * [!UICONTROL Extra Endpoint] - Lägg till  `CNAMES`om du använder dem för att spåra servrar som  `metrics.companyname.com`
   * **Hjärtslag för video (Media Analytics)**

      * [!UICONTROL Default Endpoint] - Data i det här fältet tillhandahålls av Adobe och kan inte ändras.
      * [!UICONTROL Extra Endpoint] - Lägg till  `CNAMES`, om du använder dem, för spårningsservern, t.ex.  `metrics.companyname.com`.

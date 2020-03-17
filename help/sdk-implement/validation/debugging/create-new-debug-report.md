---
title: Skapa en ny felsökningsrapport
description: I det här avsnittet beskrivs hur du skapar en ny felsökningsrapport.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Skapa en ny felsökningsrapport{#create-a-new-debug-report}

Så här skapar du en ny felsökningsrapport:

1. Välj [!UICONTROL Create New Debug Report] följande:

   ![](assets/create-new-debug-report.png)

1. Fyll i fälten med följande information:

   * **Namnge rapporten** - Ange spelarens namn och datum så att du enkelt kan spåra spelaren under certifieringen och hålla varumärken och plattformar åtskilda.
   * **Adobe Analytics**

      * [!UICONTROL User Name] och [!UICONTROL Shared Secret] - Dessa fält är valfria, men du kan lägga till dina API-uppgifter för webbtjänster i Adobe Debug för att visa variabelnamnen och variabelinställningarna för rapportsviten.

         Du kommer åt på något av följande sätt:

         * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
         * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] Om du vill skapa en API-autentiseringsuppgift för webbtjänster för en ny användare lägger du till användaren i användargruppen för [!UICONTROL User Management]webbtjänståtkomst **** i .
      * [!UICONTROL Default Endpoint] - Informationen i det här fältet tillhandahålls av Adobe och kan inte ändras.
      * [!UICONTROL Extra Endpoint] - Lägg till `CNAMES`om du använder dem för att spåra servrar som `metrics.companyname.com`
   * **Hjärtslag för video (Media Analytics)**

      * [!UICONTROL Default Endpoint] - Informationen i det här fältet tillhandahålls av Adobe och kan inte ändras.
      * [!UICONTROL Extra Endpoint] - Lägg till `CNAMES`, om du använder dem, för spårningsservern, t.ex. `metrics.companyname.com`.




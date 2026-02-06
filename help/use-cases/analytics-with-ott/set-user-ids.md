---
title: Ange användar-ID
description: API:er för att ange användar-ID:n, vilken server som en unik kundidentifierare.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# Ange användar-ID:n{#set-user-ids}

Användar-ID:t är en unik anpassad besökaridentifierare som definieras av programmet för en användare.

Ange och hämta det unika användar-ID:t på ADBMomobile SDK enligt följande:

* **Uppsättning:**

   * **Roku:**

     ```
     ADBMobile().setUserIdentifer("app-generated-unique-id")
     ```

   * **Chromecast:**

     ```
     ADBMobile().config.setUserIdentifer("app-generated-unique-id");
     ```

* **Hämta:**

   * **Roku:**

     ```
     vid = ADBMobile().userIdentifer()
     ```

   * **Chromecast:**

     ```
     vid = ADBMobile().config.getUserIdentifer();
     ```

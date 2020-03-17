---
title: Ange användar-ID
description: API:er för att ange användar-ID:n, vilken server som en unik kundidentifierare.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Ange användar-ID{#set-user-ids}

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

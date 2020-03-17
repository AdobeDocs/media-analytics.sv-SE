---
title: Spåra appåtgärder
description: Programåtgärder är de händelser som inträffar i appen som du vill mäta.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Spåra appåtgärder{#track-app-actions}

Åtgärder är de händelser som inträffar i programmet och som du vill mäta.

Varje åtgärd har en eller flera motsvarande mätvärden som ökas stegvis varje gång händelsen inträffar. Du kan t.ex. skicka ett `trackAction` samtal för varje ny prenumeration, varje gång innehållet betygsätts eller varje gång en nivå är slutförd.

Åtgärder spåras inte automatiskt, så anrop `trackAction` när en händelse som du vill spåra inträffar och mappa åtgärden till en anpassad händelse.

1. Ring när en händelse som du vill spåra inträffar `trackAction`.

   * **Roku:**

      ```js
      ADBMobile().trackAction("myapp.ActionName", {})
      ```

   * **Chromecast:**

      ```js
      ADBMobile.analytics.trackAction("myapp.ActionName", {});
      ```

1. Mappa åtgärden till en anpassad händelse.

   * **Roku:**

      ```js
      dictionary = {} 
      dictionary["myapp.social.SocialSource"] = "Twitter"  
      ADBMobile().trackAction("myapp.SocialShare", dictionary)
      ```

   * **Chromecast:**

      ```js
      var dictionary = {}; 
      dictionary["myapp.social.SocialSource"] = "Twitter"; 
      ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
      ```

Du kan också skicka ytterligare kontextdata för varje spårningsåtgärdsanrop.


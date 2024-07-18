---
title: Spåra programåtgärder
description: Programåtgärder är de händelser som inträffar i appen som du vill mäta.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Spåra appåtgärder{#track-app-actions}

Åtgärder är de händelser som inträffar i programmet och som du vill mäta.

Varje åtgärd har en eller flera motsvarande mätvärden som ökas stegvis varje gång händelsen inträffar. Du kan till exempel skicka ett `trackAction`-samtal för varje ny prenumeration, varje gång innehållet betygsätts eller varje gång en nivå har slutförts.

Åtgärder spåras inte automatiskt, så anropa `trackAction` när en händelse som du vill spåra inträffar och mappa åtgärden till en anpassad händelse.

1. Ring `trackAction` när en händelse som du vill spåra inträffar.

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

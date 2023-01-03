---
title: "Migrering från fristående Media SDK till Adobe Launch - iOS"
description: Lär dig hur du migrerar från Media SDK till Launch för iOS.
exl-id: f70b8e1b-cb9f-4230-86b2-171bdaed4615
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: fb09280ae6fb9f0ab7e67bd6ae134e6e26f88ec8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Migrering från fristående Media SDK till Adobe Launch - iOS

>[!NOTE]
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) för en konsoliderad hänvisning till terminologiska förändringar.

## Konfiguration

### Fristående media SDK

I det fristående Media SDK konfigurerar du spårningskonfigurationen i appen och skickar den till SDK när du skapar spåraren.

```objective-c
ADBMediaHeartbeatConfig *config =
  [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"v2.0.0";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### Starta tillägg

1. I Experience Platform Launch klickar du på [!UICONTROL Extensions] fliken för din mobila egenskap
1. På [!UICONTROL Catalog] går du till Adobe Media Analytics för ljud- och videotillägg och klickar på [!UICONTROL Install].
1. Konfigurera spårningsparametrarna på sidan för tilläggsinställningar.
Media-tillägget använder de konfigurerade parametrarna för spårning.

   ![](assets/launch_config_mobile.png)

[Konfigurera Media Analytics-tillägget](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

## Skapa spårare

### Fristående media SDK

I den fristående Media SDK skapar du manuellt `ADBMediaHeartbeatConfig` och konfigurera spårningsparametrarna. Implementera delegatgränssnittet som visar
`getQoSObject()` och `getCurrentPlaybackTime()functions.`

Skapa en MediaHeartbeat-instans för spårning:

```objective-c
@interface PlayerDelegate : NSObject<ADBMediaHeartbeatDelegate>
@end

@implementation PlayerDelegate {
}

- (NSTimeInterval) getCurrentPlaybackTime {
    // When called should return the current player time in seconds.
    return playhead_;
}

- (nonnull ADBMediaObject*) getQoSObject {
    // When called should return the latest qos values.
    return qosObject_;
}
@end

ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"app-version";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;
ADBMediaHeartbeatDelegate* delegate = [[PlayerDelegate alloc] init];

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:delegate config:config];
```

### Starta tillägg

[Media API-referens - Skapa mediespårare](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createtracker)

Innan du skapar spåraren ska du registrera medietillägget och de beroende tilläggen med mobilkärnan.

```objective-c
// Register the extension once during app launch
#import <ACPCore.h>
#import <ACPAnalytics.h>
#import <ACPMedia.h>
#import <ACPIdentity.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"your-launch-app-id"];
    [ACPMedia registerExtension];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPCore start:nil];
    return YES;
}
```

När medietillägget har registrerats kan spåraren skapas med följande API.
Spåraren väljer automatiskt konfigurationen från den konfigurerade startegenskapen.

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

## Uppdaterar värden för spelhuvud och upplevelsekvalitet.

### Fristående media SDK

I det fristående Media SDK är ett delegatobjekt som implementerar
`ADBMediaHeartbeartDelegate` protokollet skickas när spåraren skapas.
Implementeringen bör returnera det senaste QoE-numret och spelhuvudet när spåraren anropar `getQoSObject()` och `getCurrentPlaybackTime()` gränssnittsmetoder.

### Starta tillägg

Implementeringen ska uppdatera spelarens spelhuvud genom att anropa
`updateCurrentPlayhead` metod som exponeras av spåraren. För korrekt spårning bör du anropa den här metoden minst en gång per sekund.

[Media API-referens - Uppdatera aktuellt spelhuvud](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#updatecurrentplayhead)

Implementeringen bör uppdatera QoE-informationen genom att anropa
`updateQoEObject` metod som exponeras av spåraren. Du bör anropa den här metoden när det finns en ändring i kvalitetsmåtten.

[Media API-referens - Uppdatera QoE-objekt](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createqoeobject)

## Skicka standardmedier/annonsmetadata

### Fristående media SDK

* Standardmetadata för media:

   ```objective-c
   ADBMediaObject *mediaObject =
     [ADBMediaHeartbeat createMediaObjectWithName:@"media-name"
                        mediaId:@"media-id"
                        length:60
                        streamType:ADBMediaHeartbeatStreamTypeVod
                        mediaType:ADBMediaTypeVideo];
   
   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata = [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample show" forKey:ADBVideoMetadataKeySHOW];
   [standardMetadata setObject:@"Sample season" forKey:ADBVideoMetadataKeySEASON];
   [mediaObject setValue:standardMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
   
   //Attaching custom metadata
   NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   
   [tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* Standardmetadata för annonsering:

   ```objective-c
   ADBMediaObject* adObject =
     [ADBMediaHeartbeat createAdObjectWithName:[adData objectForKey:@"name"]
                        adId:[adData objectForKey:@"id"]
                        position:[[adData objectForKey:@"position"] doubleValue]
                        length:[[adData objectForKey:@"length"] doubleValue]];
   
   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata =
     [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample Advertiser"
                     forKey:ADBAdMetadataKeyADVERTISER];
   [standardMetadata setObject:@"Sample Campaign"
                     forKey:ADBAdMetadataKeyCAMPAIGN_ID];
   [adObject setValue:standardMetadata
                     forKey:ADBMediaObjectKeyStandardAdMetadata];
   
   //Attaching custom metadata
   NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
   [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
   
   [tracker trackEvent:ADBMediaHeartbeatEventAdStart
            mediaObject:adObject
            data:adDictionary];
   ```

### Starta tillägg

* Standardmetadata för media:

   ```objective-c
   NSDictionary *mediaObject =
     [ACPMedia createMediaObjectWithName:@"media-name"
               mediaId:@"media-id"
               length:60
               streamType:ACPMediaStreamTypeVod
               mediaType:ACPMediaTypeVideo];
   
   NSMutableDictionary *mediaMetadata =
     [[NSMutableDictionary alloc] init];
   
   // Standard metadata keys provided by adobe.
   [mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
   [mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];
   
   // Custom metadata keys
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   [_tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* Standardmetadata för annonsering:

   ```objective-c
   NSDictionary* adObject =
     [ACPMedia createAdObjectWithName:@"ad-name"
               adId:@"ad-id"
               position:1
               length:15];
   
   NSMutableDictionary* adMetadata =
     [[NSMutableDictionary alloc] init];
   
   // Standard metadata keys provided by adobe.
   [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
   [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];
   
   // Custom metadata keys
   [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];
   
   [tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];
   ```

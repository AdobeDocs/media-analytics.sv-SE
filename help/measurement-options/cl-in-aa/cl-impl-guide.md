---
title: Implementeringshandbok för anpassade länkar
description: null
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Implementeringshandbok för anpassad länk{#custom-link-implementation-guide}

Anpassad videospårning använder [manuell länkspårning med anpassad länkkod](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) i Analytics `appMeasurement`.
Oftast används videouppföljning för anpassade videolänkar på plattformar och enheter där minimal videomätning krävs.

* I JavaScript: funktionen `s.tl()`
* I mobilappar: [trackAction() Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html), [trackAction() iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html), [trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
* I API:t för datainmatning: [linktype-tagg](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## Krav

* Åtkomst till API-händelser och data för videospelare
* Möjlighet att lägga till skript om Analytics SDK används
* Möjlighet att lägga till spårningsfyrar (egna skript eller hårdkod) om API för datainmatning används

## Metadata

* Metadata kan läggas till i alla spårningsanrop som en del av länkdata
* Kom ihåg att uppdatera `linkTrackVars` och `linkTrackEvents`

```javascript
/* Call on video complete */ 
 
if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15'; 
    s.linkTrackEvents = 'event3'; 
    s.prop10 = mediaName; 
    s.eVar10 = mediaName; 
    s.eVar12 = "video"; 
    s.eVar13 = document.title; 
    s.eVar15 = mediaPlayerName; 
    s.events = 'event3'; 
    s.tl(this,'o','Video Complete'); 
};
```

## Varför använda anpassad länk

* Minimala krav krävs
* Fungerar på alla plattformar, inklusive ej skript
* Alla beräkningar, t.ex. hur lång tid som tillbringats eller kvartilerna, måste beräknas i ett anpassat skript
* Mycket enkelt utan dolda bibliotek eller skript
* Total kontroll över alla delar av videodata

## Exempel på JavaScript för HTML5 Player

```javascript
<script type="text/javascript"> 
  myvideo = document.getElementById('movie'); 
  myvideo.addEventListener('play',myHandler,false); 
  myvideo.addEventListener('seeked',myHandler,false); 
  myvideo.addEventListener('seeking',myHandler,false); 
  myvideo.addEventListener('pause',myHandler,false); 
  myvideo.addEventListener('ended',myHandler,false); 
   
  function myHandler(e) { 
      var video = document.getElementsByTagName('video')[0]; 
      var mediaName="13502979:Sailing"; 
      var mediaLength = video.duration; 
      var mediaPlayerName = "HTML5 Player"; 
      /*Define video offset*/ 
      if (video.currentTime > 0) { 
          mediaOffset = Math.floor(video.currentTime); 
      } else { 
          mediaOffset = 0; 
      }; 
      /*Call on video start*/ 
      if (e.type == "play") { 
          if (mediaOffset == 0) { 
              console.log(mediaPlayerName + 
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime)); 
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15'; 
              s.linkTrackEvents='event2'; 
              s.prop10=mediaName; 
              s.eVar10=mediaName; 
              s.eVar12="video"; 
              s.eVar13=document.title; 
              s.eVar15=mediaPlayerName; 
              s.events='event2'; 
              s.tl(this,'o','Video Start'); 
          } 
      }; 
   
      /*Call on video pause*/ 
      if (e.type == "pause") { 
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime)); 
          if (video.currentTime != video.duration) { 
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15'; 
              s.linkTrackEvents='event7'; 
              s.prop10=mediaName; 
              s.eVar10=mediaName; 
              s.eVar12="video"; 
              s.eVar13=document.title; 
              s.eVar15=mediaPlayerName; 
              s.events='event7'; 
              s.tl(this,'o','Video Pause'); 
          } 
      }; 
   
      /*Call on video complete*/ 
      if (e.type == "ended") { 
          console.log(mediaPlayerName + 
            ' -> ended -> playhead: ' + 
            Math.floor(video.currentTime)); 
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15'; 
          s.linkTrackEvents = 'event3'; 
          s.prop10= m ediaName; 
          s.eVar10=mediaName; 
          s.eVar12="video"; 
          s.eVar13=document.title; 
          s.eVar15=mediaPlayerName; 
          s.events='event3'; 
          s.tl(this,'o','Video Complete'); 
      }; 
  }; 
</script>
```

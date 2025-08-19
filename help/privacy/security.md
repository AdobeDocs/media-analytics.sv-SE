---
title: Säkerhet
description: Läs mer om säkerhet i relation till direktuppspelande medietjänster
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: a301612f-5019-40c3-af40-d608cd320e16
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 49%

---

# Säkerhet {#security}

På Adobe tar vi säkerhet och integritet på allvar. Från ett rigoröst säkerhetstänk i våra interna processer och verktyg för programutveckling till våra funktionsövergripande incidentresponsteam så strävar vi efter att alltid ligga steget före och vara flexibla. Dessutom hjälper vårt samarbete med partners, forskare och andra branschorganisationer oss att förstå de senaste hoten och bästa säkerhetspraxis. Med vårt förebyggande arbetssätt kan vi kontinuerligt bygga in säkerhet i de produkter och tjänster vi erbjuder.


## Säkerhet för transportlager {#transport-layer-security}

**Säkerhetsmeddelande för transportlager -** Adobe har säkerhetsstandarder som kräver att äldre säkerhetsprotokoll upphör att gälla. För att fortsätta uppfylla de föränderliga säkerhetsprotokollstandarderna går Adobe mot att använda TLS 1.2 (Transport Layer Security) för att få den senaste och säkraste versionen. Från och med 20 februari 2019 har Adobe endast stöd för TLS 1.1 och senare. I och med den här ändringen kommer Adobe inte längre att samla in data från slutanvändare med äldre enheter eller webbläsare som använder TLS 1.0. Att migrera till TLS 1.2 ger högre säkerhet. Det är viktigt att du går igenom detaljerna och planerar ändringarna för en smidig övergång.

>[!NOTE]
>
>TLS är för närvarande det vanligaste säkerhetsprotokollet i webbläsare och andra program när data måste utväxlas säkert över nätverk.

---
title: Klachten
description: 'Meer informatie over klachten die zijn geregistreerd wanneer een gebruiker aangeeft dat een e-mail ongewenst of onverwacht is. '
feature: Metrics
topics: Deliverability
kt: 7048
thumbnail: kt7048.jpg
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: d42a8c3b06308fca0cf3e9db8d634a767fc0cdc6
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%

---


# Klachten

Klachten worden geregistreerd wanneer een gebruiker aangeeft dat een e-mailbericht ongewenst of onverwacht is. Deze abonneeactie wordt typisch het programma geopend door of de e-mailcliënt van de abonnee wanneer zij de spamknoop of via een derdespam rapporterend systeem raken.

## ISP-klacht

De meeste Rij 1 en sommige Rij 2 ISPs verstrekken een spam meldend methode aan hun gebruikers aangezien opt-out en unsubscribe processen in het verleden maliciously zijn gebruikt om een e-mailadres te bevestigen. Adobe Campaign ontvangt deze klachten via ISP FBL&#39;s. Dit wordt gevestigd tijdens het opstellingsproces voor om het even welke ISPs die FBLs verstrekken en staat Adobe Campaign toe om e-mailadressen automatisch toe te voegen die aan de quarantainetabel voor onderdrukking klaagden. De pieken in ISP klachten kunnen een indicator van slechte lijstkwaliteit, minder-dan-optimale methodes van de lijstinzameling, of zwak betrokkenheidsbeleid zijn. Ze worden ook vaak vermeld wanneer de inhoud niet relevant is.

## Klachten van derden

Er zijn verscheidene anti-spamgroepen die voor spamrapportering op een breder niveau toestaan. De gegevens van de klacht die door deze derden worden gebruikt worden gebruikt om e-mailinhoud te etiketteren om spame-mail te identificeren. Dit proces wordt ook wel vingerafdrukken genoemd. Gebruikers van deze methoden voor klachten van derden zijn over het algemeen zuiniger over e-mail, zodat zij een grotere impact kunnen hebben dan andere klachten kunnen hebben als zij niet worden beantwoord.

>[!NOTE]
>
>ISPs verzamelt klachten en gebruikt hen om de algemene reputatie van een afzender te bepalen. Alle klachten moeten worden onderdrukt en niet langer zo snel mogelijk worden benaderd, overeenkomstig de plaatselijke wetten en voorschriften.

## Productspecifieke bronnen

**Adobe Campaign Standard**

* [Klachten](https://experienceleague.adobe.com/docs/campaign-standard/using/reporting/list-of-reports/complaints.html#reporting)
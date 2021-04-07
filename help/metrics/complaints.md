---
title: Klachten
description: 'Lees meer over klachten die worden geregistreerd wanneer een gebruiker aangeeft dat een e-mail ongewenst of onverwacht is. '
feature: Metrics
topics: Deliverability
kt: 7048
thumbnail: kt7048.jpg
doc-type: article
activity: understand
team: ACS
translation-type: ht
source-git-commit: 550821608eb7049f739a156536dd31b6b2faa2fa
workflow-type: ht
source-wordcount: '291'
ht-degree: 100%

---


# Klachten

Klachten worden geregistreerd wanneer een gebruiker aangeeft dat een e-mailbericht ongewenst of onverwacht is. Deze actie wordt meestal geregistreerd via de e-mailclient van de abonnee wanneer deze de spamknop selecteert, of via een systeem van derden voor spammeldingen.

## ISP-klacht

De meeste Tier 1- en sommige Tier 2-ISP’s bieden hun gebruikers een methode aan voor het melden van spam, omdat procedures voor opt-out en uitschrijven in het verleden misbruikt zijn voor het valideren van e-mailadressen. Adobe Campaign ontvangt deze klachten via feedbackloops (FBL’s) van de ISP. Een FBL wordt ingeschakeld tijdens het configuratieproces voor ISP’s die FBL’s aanbieden. Via een FBL kan Adobe Campaign automatisch e-mailadressen waarover klachten zijn gekomen, toevoegen aan de quarantainetabel om deze adressen te onderdrukken. Pieken in klachten bij een ISP kunnen duiden op een slechte kwaliteit van de mailinglijst, inadequate methoden voor verzameling van e-mailadressen of een zwak beleid op het gebied van engagement. Dergelijke pieken worden ook vaak gezien wanneer de content niet relevant is.

## Spamklachten van derden

Er zijn verscheidene antispamgroepen die het melden van spam op bredere schaal toestaan. Deze derde partijen gebruiken de metrics voor spamklachten om e-mailcontent te taggen voor het identificeren van spammail. Dit proces wordt ook wel &#39;fingerprinting&#39; genoemd. Gebruikers van deze methoden voor spamklachten van derden hebben over het algemeen meer kennis over e-mail. Als er niets met hun klachten wordt gedaan, kunnen deze een grotere impact hebben dan andere spamklachten.

>[!NOTE]
>
>ISP’s verzamelen klachten en gebruiken deze om de algemene reputatie van een verzender te bepalen. Alle klachten moeten zo snel mogelijk worden onderdrukt en er moeten geen berichten meer naar het desbetreffende e-mailadres worden gestuurd, overeenkomstig de plaatselijke wetten en voorschriften.

## Productspecifieke bronnen

**Adobe Campaign Classic**

* [Trackingsindicatoren](https://experienceleague.adobe.com/docs/campaign-classic/using/reporting/reports-on-deliveries/delivery-reports.html?lang=nl#tracking-indicators)

**Adobe Campaign Standard**

* [Klachtenrapport](https://experienceleague.adobe.com/docs/campaign-standard/using/reporting/list-of-reports/complaints.html?lang=nl#reporting)
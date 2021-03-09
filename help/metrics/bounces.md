---
title: Bounces
description: Meer informatie over de verschillende typen grenzen
feature: Metrics
topics: Deliverability
kt: 7047
thumbnail: kt7047.jpg
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: d42a8c3b06308fca0cf3e9db8d634a767fc0cdc6
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---


# Bounces

De grenzen zijn het resultaat van een leveringspoging en mislukking waar ISP achtermislukkingsberichten verstrekt. De verwerking van de stuitbehandeling is een kritiek deel van lijsthygiëne. Nadat een bepaalde e-mail meerdere keren achter elkaar is teruggestuurd, wordt deze tijdens dit proces gemarkeerd voor onderdrukking. Het aantal en het type van grenzen die worden vereist om onderdrukking teweeg te brengen variëren van systeem tot systeem. Hierdoor wordt voorkomen dat systemen ongeldige e-mailadressen blijven verzenden. De grenzen zijn één van de belangrijkste stukken van gegevens die ISPs gebruikt om IP reputatie te bepalen. Het is heel belangrijk om deze maatstaf in de gaten te houden. &quot;Geleverd&quot; versus &quot;teruggestort&quot; is waarschijnlijk de meest gebruikelijke manier om de levering van marketingberichten te meten: hoe hoger het geleverde percentage is , hoe beter .

We graven in twee verschillende soorten stommingen.

## Harde vlekken

De harde stegels zijn permanente mislukkingen die worden geproduceerd nadat ISP een postingspoging aan een abonneeadres als niet te leveren niet bepaalt. In Adobe Campaign worden harde golven die als niet-leverbaar zijn gecategoriseerd, aan de quarantaine toegevoegd, wat betekent dat ze niet opnieuw zouden worden geplaatst. In sommige gevallen wordt een harde stuit genegeerd als de oorzaak van de fout onbekend is.
Hier volgen enkele voorbeelden van harde grenzen:

* Adres bestaat niet
* Account uitgeschakeld
* Ongeldige syntaxis
* Ongeldig domein

## Zachte golven

De zachte grenzen zijn tijdelijke mislukkingen die ISPs produceert wanneer zij moeilijkheden hebben leverend post. Zachte mislukkingen zullen veelvoudige tijden (met variantie afhankelijk van gebruik van douane of uit-van-doos leveringsmontages) opnieuw proberen om een succesvolle levering te proberen. Adressen dat voortdurend zachte stuit niet aan quarantaine zal worden toegevoegd tot het maximumaantal herpogingen is geprobeerd (die opnieuw afhankelijk van montages) variëren. Tot de meest voorkomende oorzaken van zachte grenzen behoren:

* Postbus vol
* E-mailserver ontvangen
* Problemen met reputatie van afzender

![stuitertypen](../assets/bounce-types.png)

>[!NOTE]
>
>De stuiteringen zijn een zeer belangrijke indicator van een reputatie kwestie omdat zij een slechte gegevensbron (harde stuit) of een reputatie kwestie met ISP (zachte stuit) kunnen benadrukken.
>
>Zachte grenzen treden vaak op als onderdeel van het verzenden van e-mail en moeten tijdens de hertestverwerking kunnen worden opgelost voordat ze worden gekarakteriseerd als een probleem dat werkelijk te leveren is. Als uw soft bounce tarief voor één enkele ISP groter is dan 30 percenten en niet binnen 24 uren oplost, is het een goed idee om een zorg met uw adviseur van de Leesbaarheid van Adobe Campaign te verhogen.

## Productspecifieke bronnen

**Adobe Campaign Standard**

* [Lijst met rapporten - Bounce-overzicht (productdocumentatie)](https://experienceleague.adobe.com/docs/campaign-standard/using/reporting/list-of-reports/bounce-summary.html?lang=en#reporting)
* [Werken met leveringsfouten (productdocumentatie)](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-delivery-failures.html?lang=en#about-delivery-failures)

**Adobe Campaign Classic**

* [Werken met leveringsfouten (productdocumentatie)](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html?lang=en#sending-messages)
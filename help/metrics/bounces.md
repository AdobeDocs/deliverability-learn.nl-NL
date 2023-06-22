---
title: Bounces
description: Meer informatie over de verschillende typen bounces.
topics: Deliverability
jira: KT-7047
thumbnail: kt7047.jpg
doc-type: article
activity: understand
team: ACS
exl-id: 6338eb67-3efd-476e-8b26-97bbb6a1d35f
source-git-commit: 9444f8601f2f349398ee5deb9d5f4d4f7abb44f5
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# Bounces

Bounces zijn het resultaat van een mislukte leveringspoging waarbij de ISP een melding van de mislukte poging stuurt. Een goede afhandeling van de bounces is cruciaal voor een schone mailinglijst. Nadat een bepaalde e-mail meerdere keren achter elkaar is afgewezen, zorgt het afhandelingsproces ervoor dat dit e-mailadres wordt gemarkeerd om te worden onderdrukt. Het aantal en het type bounces die erin resulteren dat het e-mailadres wordt onderdrukt, variëren per systeem. Dit proces voorkomt dat systemen doorgaan met het verzenden van e-mails naar ongeldige adressen. Bounces zijn één van de belangrijkste gegevenselementen die ISP’s gebruiken voor het bepalen van de IP-reputatie. Het is erg belangrijk om deze metric in de gaten te houden. ‘Afgeleverd’ versus ‘niet bezorgd’ is waarschijnlijk de meest gebruikelijke manier om de aflevering van marketingberichten te meten: hoe hoger het afleverpercentage, hoe beter.

We gaan wat dieper in op twee soorten bounces.

## Hard bounces

Een hard bounce is een permanent mislukte leveringspoging die wordt gemeld nadat de ISP heeft vastgesteld dat een e-mail niet kan worden afgeleverd op het e-mailadres van de abonnee. Bij Adobe Campaign worden hard bounces die als niet-leverbaar zijn gecategoriseerd, in quarantaine geplaatst. Dat houdt in dat er geen nieuwe verzendpoging volgt. In sommige gevallen wordt een hard bounce genegeerd als de oorzaak van de fout onbekend is.
Hier volgen enkele voorbeelden van hard bounces:

* Adres bestaat niet
* Account is uitgeschakeld
* Onjuiste syntaxis
* Ongeldig domein

## Soft bounces

Een soft bounce is een tijdelijk mislukte leveringspoging die wordt gemeld wanneer de ISP problemen heeft met het afleveren van de e-mail. Er volgen meerdere verzendpogingen (met variantie, afhankelijk van het gebruik van aangepaste of standaardinstellingen voor e-maillevering) om de e-mail succesvol af te leveren. Adressen waarbij telkens opnieuw een soft bounce optreedt, worden niet in quarantaine geplaatst totdat het maximumaantal hernieuwde pogingen is bereikt (ook dat varieert op basis van de instellingen). Tot de meest voorkomende oorzaken van soft bounces behoren:

* Mailbox is vol
* De ontvangende e-mailserver is down
* Problemen met de reputatie van de verzender

![soorten bounces](../assets/bounce-types.png)

>[!NOTE]
>
>Bounces zijn een belangrijke indicator van een reputatieprobleem omdat ze een slechte databron (hard bounce) of een reputatieprobleem met een ISP (soft bounce) aan het licht kunnen brengen.
>
>Soft bounces treden vaak op bij het verzenden van e-mail en moeten de kans krijgen om te worden opgelost bij hernieuwde verzendpogingen voordat ze worden gecategoriseerd als een echt leveringsprobleem. Als uw percentage van soft bounces bij één ISP hoger is dan 30% en de soft bounces niet binnen 24 uur zijn opgelost, is het raadzaam om deze kwestie aan te kaarten bij uw Adobe Campaign-consultant voor leverbaarheid.

## Productspecifieke bronnen

**Adobe Campaign Classic**

* [Typen verzendingsfouten en redenen](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html?lang=nl#delivery-failure-types-and-reasons)
* [Niet-bezorgbare e-mail beheren](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html?lang=nl#bounce-mail-management)
* [Rapport met niet-verzendbare en niet-bezorgbare e-mail](https://experienceleague.adobe.com/docs/campaign-classic/using/reporting/reports-on-deliveries/global-reports.html?lang=nl#non-deliverables-and-bounces)

**Adobe Campaign Standard**

* [Typen verzendingsfouten en redenen](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-delivery-failures.html?lang=nl#delivery-failure-types-and-reasons)
* [Kwalificatie van niet-bezorgde e-mails](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-delivery-failures.html?lang=nl#bounce-mail-qualification)
* [Samenvattingsrapport van niet-bezorgde e-mails](https://experienceleague.adobe.com/docs/campaign-standard/using/reporting/list-of-reports/bounce-summary.html?lang=nl#reporting)

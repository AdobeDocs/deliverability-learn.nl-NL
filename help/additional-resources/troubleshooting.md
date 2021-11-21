---
title: Probleemoplossing voor levering
description: Leer hoe u leveringsproblemen kunt identificeren en oplossen.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 4cc85124-e7e4-4cd5-99a9-23d2d8cf08fe
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Probleemoplossing voor levering {#troubleshooting}

Hieronder vindt u een aantal tips en trucs die u kunnen helpen om problemen met betrekking tot de prestaties op te sporen en aan te pakken.

## Identificeer een leveringsprobleem {#identify-deliverability-issue}

Om een mogelijke kwestie te identificeren, de elementen die op worden vermeld [die pagina](/help/ongoing-monitoring.md) kan uw aandacht vestigen.

<!--
Mailing or campaign metrics: unsubscribe, abuse complaint and/or bounce rates are higher than usual.
Subscriber activity: opens, clicks and/or transactions are lower than usual.
Seed accounts show filtered or non-delivered mailings.
-->

## Mogelijke hypothetische oorzaken {#potential-causes}

Stel uzelf de volgende vragen om de mogelijke oorzaken van het probleem van de leverbaarheid te achterhalen:

* Was er een recente wijziging in de segmentatie van lijsten?
* Heb ik nieuwe gegevensbronnen verkregen?
* Heb ik per ongeluk een quarantainebestand gepost?
* Kan het probleem worden veroorzaakt door mijn berichtinhoud?
* Verzend ik vaak genoeg om warme IPs te handhaven?
* segmenteer ik mijn berichten op activiteit/betrokkenheid, of verzend volledig-dossiers?
* Wat is het &#39;veilige&#39; segment in mijn bestand wat betreft recentie?
* Beschikt ik over strategieën voor reactivering en herbevestiging voor segmenten die niet als veilig worden gedefinieerd?

## Het probleem verhelpen {#address-issue}

### Klachten

[Klachten](/help/metrics/complaints.md) worden bepaald door abonnees die e-mail als spam door de overeenkomstige knoop van hun inbox te raken melden.

Als uw bezorgingsprobleem is veroorzaakt door klachten:
* U moet proberen te bepalen waarom de ontvangers klagen.
* Je kunt ook overwegen om je afmeldingskoppeling naar de bovenkant van je e-mail te verplaatsen. Dit zal abonnees aanmoedigen om zich af te melden in plaats van met de spamknoop te klagen.

Afzenders kunnen een schat aan informatie uit hun [feedbacklus](/help/transition-process/infrastructure.md#feedback-loops) klachten:
* Het is belangrijk om de gegevens op te nemen en te zoeken naar patronen in zaken als opt-in-bron, hoe lang het adres is ingetekend, of zelfs bepaalde gedrags-demografie.
* Klachten kunnen vaak een riskante gegevensbron of segment in het bestand identificeren. Risky wordt gedefinieerd als het meest waarschijnlijk om te klagen, wat reputatie, en beurtelings, inbox tarieven kan beschadigen.

De klachten zijn ook afkomstig van abonnees die gewoon geen e-mail meer willen ontvangen:
* Dit kan vaak toe te schrijven zijn aan overseinen, de perceptie van uw abonnees van het bericht, dat zij niet het bericht verwachtten, of zich niet het kiezen binnen herinneren.
* Het is ook belangrijk om een controle in werking te stellen om ervoor te zorgen dat alle punten van inzameling duidelijk zijn, en dat er geen vooraf gecontroleerde dozen in uw punten van verwerving zijn.
* U moet ook een welkomstbericht sturen wanneer abonnees zich aanmelden om de toon te bepalen en uit te leggen hoe vaak ze e-mails van u kunnen ontvangen.

### Geldigheid van gegevens

**Harde vlekken** komt voor wanneer u naar een **niet-leverbaar adres** bij een ISP. Een adres kan om vele redenen zoals:
* Onjuist gespeld adres. Dit kan worden opgelost met een realtime service voor gegevensvalidatie, of door een bevestigde aanmeldingsprocedure te vereisen voordat marketinge-mails naar dat adres worden verzonden.
* Onjuiste lijst of gegevensbron. Als het uit een nieuwe bron komt, herzie hoe de adressen werden verzameld en zorg ervoor dat er toestemming was.
* Verzenden naar een adres dat op een bepaald moment actief was, maar na een periode van inactiviteit is gesloten of beëindigd.

### Betrokkenheid

Naast klachten en gegevensgeldigheid, concentreren ISPs zich meer dan ooit op **positieve betrokkenheid** besluiten over de uitvoering te nemen. Ze kijken of je abonnees je e-mails openen of ze verwijderen zonder ze te lezen. Omdat deze gegevens niet worden gedeeld met afzenders, moeten we de beschikbare informatie gebruiken en de taken voor het openen, klikken en uitvoeren als betrokkenheid vertalen.

In het kader van het voortdurende reputatie-onderhoud is het belangrijk te begrijpen hoe betrokken abonnees op uw lijst staan en een **hiërarchie van het recuperatierisico** voor de abonnees op elk dossier. Recentie wordt gedefinieerd als laatste open-/klikdatum, -datum of -datum. Dit tijdkader kan verticaal verschillen. Dit doet u als volgt:

1. Bepaal actieve (&quot;veilige&quot;) segmenten voor elke verticaal. Dit zijn typisch abonnees die binnen de laatste 3-6 maanden actief zijn geweest.
1. Verminder de frequentie tot inactieven.
1. Een [hernieuwde betrokkenheid](/help/additional-resources/re-engagement.md) reeks voor matige risico-inactieven. Dit is doorgaans 6 tot 9 maanden zonder betrokkenheid.
1. Ontwikkelen van een herbevestigingscampagne voor inactieven met een hoger risico. Dit zijn doorgaans abonnees die in 9 tot 12 maanden geen e-mailberichten hebben ontvangen.
1. Stel ten slotte een keuzeregel in en verwijder abonnees die uw e-mails niet hebben geopend in &#39;x&#39; maanden. We raden doorgaans 12+ maanden aan, maar dit kan verschillen afhankelijk van de verkoop- en aankoopcyclus.

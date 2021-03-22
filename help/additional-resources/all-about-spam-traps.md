---
title: Alles over spamovervullingen
description: Leer hoe u spamvallen begrijpt, identificeert en voorkomt bij het beheren van de leverbaarbaarheid.
feature: Aanvullende bronnen
topics: Deliverability
kt: null
thumbnail: null
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: 3696ec013014ea41c634ac4829ec40977d224ff1
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Alles over spamovervullingen

Een [spamval](/help/metrics/spam-traps.md) is een geldig adres, zonder foutbericht wanneer e-mails worden verzonden naar. Een spamtrap heeft een hoofdmissie: spammers of afzenders te identificeren zonder gegevenshygiënisch proces.

## Wie beheert deze spamovervaladressen?

Het eerste type van spamvaladressen is het IP en bedrijf van de lijst van gewezen personen van het Domein zoals SpamHaus, Sorbs, SpamCop. Deze bedrijven hebben een enorm netwerk van adressen die op diverse Internet-pagina&#39;s als website, blog, forums worden verzonden zodat hun adressen door spammers worden verzameld.

Het tweede type van spamval is gebaseerd oude actieve ISP adressen. Deze ISPs heeft hun eigen netwerk van de spamval dat op inactieve adressen wordt gebouwd in val wordt herconverteerd en elke klap die de afzender IP en domeinreputatie beïnvloedt.

## Hoe werkt het?

**Een e-mailadres zonder eindgebruiker**: Deze adressen hebben en zullen nooit een eindgebruiker hebben die aan nieuwsbrieven of een ander type van mededelingen kon registreren.

**Een e-mailadres dat door een gebruiker** wordt verlaten: Na een periode van inactiviteit, worden de adressen gedeactiveerd door ISPs. Bounces-berichten worden naar afzenders verzonden om hen over deze nieuwe status te informeren. De afzenders moeten in quarantaine deze adressen duwen of hen uit toekomstige mededelingen verwijderen. ISPs gebruikt deze adressen die in &quot;spamval&quot;worden getransformeerd om afzenders met slechte praktijken te controleren.

## Hoe te om een spamval te erkennen of te identificeren?

Het is een moeilijke baan om spamvallen te identificeren, moeten deze adressen anoniem blijven aangezien zij worden gebruikt om slechte afzenders te identificeren. Het grootste deel van ISPs heeft open en klikt systeem niet om slechte afzenders te controleren treffers. Volgens eerdere definities is het mogelijk om een pod met verdachte adressen te bepalen en de efficiëntie van de podselectie te testen.

## Waarom uw gegevensbestand door spamvallen wordt besmet?

Uw e-mailadresgegevensbestand bevat spamval, hoe kon het mogelijk zijn? De twee belangrijkste redenen zijn het gebrek aan hygiëne in de gegevensbank of het verzamelen van disfuncties.

Deze paar punten helpen u om uw processen te controleren:

* Verzamel disfunctie:
   * Waar komen uw e-mailadressen vandaan? Hoeveel bronnen worden gebruikt om deze adressen te verzamelen? Kunt u ze identificeren? Interne/coregistratie?
   * Werkt uw opt-in-systeem goed?
   * Hebt u domeinen en alias van uw adressen gecontroleerd? Doe het met de onderstaande tabel!
* Databasehygiëneproces:
   * Wat is uw proces betreffende inactief adres op de laatste 12 maanden?
   * Verwerkt u een quarantaine op zachte grenzen als &quot;inactieve gebruiker&quot;?
   * Wanneer is de laatste keer dat u uw database hebt verzorgd en u hebt geprobeerd deze op te schonen? Doe het regelmatig.

## Aliassen en domeinen die moeten worden vermeden

**Aliassen**

![](../../help/assets/aliases.png)

**Domeinen**

![](../../help/assets/domains.png)
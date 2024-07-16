---
title: Alles over spamvallen
description: Leer hoe u spamvallen begrijpt, identificeert en voorkomt bij het beheren van de leverbaarbaarheid.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 45cdcda0-70e4-47f4-8713-a834500e7881
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 1%

---

# Alles over spamvallen

A [ spamval ](/help/metrics/spam-traps.md) is een geldig adres, zonder foutenmelding wanneer de e-mails worden verzonden naar. Een spamvanger heeft een hoofdtaak: spammers of afzenders identificeren zonder proces voor gegevenshygiëne.

## Wie beheert deze spamovervaladressen?

Het eerste type van spamvaladressen is het IP en bedrijf van de lijst van gewezen personen van het Domein zoals SpamHaus, Sorbs, SpamCop. Deze bedrijven hebben een enorm netwerk van adressen die op diverse Internet-pagina&#39;s als website, blog, forums worden verzonden zodat hun adressen door spammers worden verzameld.

Het tweede type van spamval is gebaseerd oude actieve ISP adressen. Deze ISPs heeft hun eigen netwerk van de spamval dat op inactieve adressen wordt gebouwd in val wordt herconverteerd en elke klap die de afzender IP en domeinreputatie beïnvloedt.

## Hoe werkt het?

**een e-mailadres zonder eind - gebruiker**: Deze adressen hebben en zullen nooit een eindgebruiker hebben die aan nieuwsbrieven of een ander type van mededelingen kon registreren.

**een e-mailadres dat door een gebruiker** wordt verlaten: Na een periode van inactiviteit, worden de adressen gedeactiveerd door ISPs. Bounces-berichten worden naar afzenders verzonden om hen over deze nieuwe status te informeren. De afzenders moeten in quarantaine deze adressen duwen of hen uit toekomstige mededelingen verwijderen. ISPs gebruikt deze adressen die in &quot;spamval&quot;worden getransformeerd om afzenders met slechte praktijken te controleren.

## Hoe te om een spamval te erkennen of te identificeren?

Het is een moeilijke baan om spamvallen te identificeren, moeten deze adressen anoniem blijven aangezien zij worden gebruikt om slechte afzenders te identificeren. Het grootste deel van ISPs heeft open en klikt systeem niet om slechte afzenders te controleren treffers. Volgens eerdere definities is het mogelijk om een pod met verdachte adressen te bepalen en de efficiëntie van de podselectie te testen.

## Waarom uw gegevensbestand door spamvallen wordt besmet?

Uw e-mailadresgegevensbestand bevat spamval, hoe kon het mogelijk zijn? De twee belangrijkste redenen zijn het gebrek aan hygiëne in de gegevensbank of het verzamelen van disfuncties.

Deze paar punten helpen u om uw processen te controleren:

* Verzamel disfunctie:
   * Waar komen uw e-mailadressen vandaan? Hoeveel bronnen worden gebruikt om deze adressen te verzamelen? Kunt u ze identificeren? Interne/coregistratie?
   * Werkt uw opt-in-systeem goed?
   * Hebt u domeinen en alias van uw adressen gecontroleerd? Doe het met de onderstaande tabel!
* Databasehygiëne:
   * Wat is uw proces betreffende inactief adres op de laatste 12 maanden?
   * Verwerkt u een quarantaine op zachte grenzen als &quot;inactieve gebruiker&quot;?
   * Wanneer is de laatste keer dat u uw database hebt verzorgd en u hebt geprobeerd deze op te schonen? Doe het regelmatig.

## Aliassen en domeinen om te vermijden

**Aliassen**

![](../../help/assets/aliases.png)

**Domeinen**

![](../../help/assets/domains.png)

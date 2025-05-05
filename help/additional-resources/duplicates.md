---
title: Duplicaten
description: Leer hoe u duplicaten kunt identificeren en beperken om de leesbaarheid te verbeteren.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: f89dbb38-a8d4-4294-b017-6fed72591593
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 4%

---

# Duplicaten {#duplicates}

Het hebben van dubbele e-mailadressen kan veelvoudige gevolgen hebben:

* Hetzelfde bericht wordt meerdere keren verzonden. Zelfs als de Adobe standaard een deduplicatieprocedure uitvoert voordat ze wordt verzonden, is er niets om te voorkomen dat hetzelfde bericht wordt verzonden door verschillende handelingen met dezelfde inhoud wanneer een doel wordt gesplitst.
* Abonnementsverzoeken worden niet geaccepteerd. Als een ontvanger zich afmeldt na het ontvangen van een bericht, is zijn dubbele profiel nog steeds geschikt voor toekomstige berichten.

Naast deze zijstap van opt-in procedures, zal deze situatie gebruikers waarschijnlijk leiden om de berichten als spam te beschouwen en een procedure van de lijst van gewezen personen bij ISP teweeg te brengen.

U moet bijzonder voorzichtig zijn wanneer het uitvoeren van verrichtingen op het gegevensbestand:

* De invoer moet zorgvuldig worden geconfigureerd, met name wanneer de verzoeningssleutel wordt gekozen.
* Gewijzigde e-mailadressen kunnen ook een bron van duplicaten zijn. Met name, kunnen twee adressen met verschillende domeinen aan de zelfde brievenbus worden verpletterd, bijvoorbeeld als een bedrijf naam heeft veranderd en het vroegere domein voor een bepaalde tijd heeft gehandhaafd: joe.doe@amce-co.com en joe.doe@acme-rebranded.com.
* Automatische invoer, hetzij van lijsten of van andere databases, is een element dat in aanmerking moet worden genomen bij het beheer van profielen. Wat gebeurt er als u een profiel verwijdert of verplaatst in een andere partitie? Het kan in de aanvankelijke verdeling door automatisch het invoeren worden ontspannen, bijvoorbeeld, wanneer een kooporder wordt geplaatst.
* Het opslaan van profielen in verschillende mappen kan worden geïmplementeerd met behulp van weergaven in plaats van partities. Op deze manier, bent u zeker dat de profielen in de zelfde fysieke verdeling terwijl nog het toelaten van de adequate rechten worden getoond en worden geleid.

Er zijn echter gevallen waarin duplicaten tussen de verschillende partities normaal zijn. Bij het verzenden van documenten voor derden of voor verschillende bedrijfsentiteiten is het bijvoorbeeld logisch dat dezelfde persoon om verschillende redenen een ontvanger is. Het is echter zelden normaal om duplicaten binnen dezelfde partitie te zoeken.

## Productspecifieke bronnen

Deduplicating adressen beschermt uw verzendende reputatie en verzekert goed quarantainebeheer. Meer informatie vindt u in de volgende secties over productdocumentatie:

**Adobe Campaign Classic**

* [ activiteit van de Deduplicatie ](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/targeting-activities/deduplication.html?lang=nl-NL)
* [ Gebruikend de functionaliteit van de Fusie van de Deduplicatie activiteit ](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/deduplication-merge.html?lang=nl-NL)

**Adobe Campaign Standard**

* [De data uit een geïmporteerd bestand dedupliceren](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/workflow-use-case/data-management/deduplicating-data-imported-file.html?lang=nl-NL)

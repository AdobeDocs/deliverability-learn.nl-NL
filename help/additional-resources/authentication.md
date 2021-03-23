---
title: Verificatie
description: Leer meer op SPF, DKIM, en de authentificatiemethodes DMARC.
feature: Aanvullende bronnen
topics: Deliverability
kt: null
thumbnail: null
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: 1e539b5df54250a5927701009e7a9c84e5d73fae
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# Verificatie

## SPF {#spf}

SPF (het Kader van het Beleid van de Afzender) is een norm van de e-mailauthentificatie die de eigenaar van een domein toestaat om te specificeren welke e-mailservers e-mail namens dat domein mogen verzenden. Deze standaard gebruikt het domein in de &quot;terugkeer-Weg&quot;kopbal van e-mail (die ook als &quot;Omhulsel van&quot;adres wordt bedoeld).

>[!NOTE]
>
>U kunt [dit externe hulpmiddel ](https://www.kitterman.com/spf/validate.html) gebruiken om een SPF verslag te verifiëren.

SPF is een techniek die, tot op zekere hoogte, u toelaat om ervoor te zorgen dat de domeinnaam die in een e-mail wordt gebruikt niet wordt vervalst. Wanneer een bericht van een domein wordt ontvangen, wordt de DNS server van het domein gevraagd. De reactie is een kort verslag (het SPF verslag) dat details welke servers worden gemachtigd om e-mail van dit domein te verzenden. Als wij veronderstellen dat slechts de eigenaar van het domein de middelen heeft om dit verslag te veranderen, kunnen wij in overweging nemen dat deze techniek niet het afzenderadres om toelaat te vervalsen, minstens niet het deel van het recht van &quot;@&quot;.

In het definitieve [RFC 4408 specificatie](https://www.rfc-editor.org/info/rfc4408), worden twee elementen van het bericht gebruikt om het domein te bepalen dat als afzender wordt beschouwd: het domein dat door het &quot;HELO&quot;bevel SMTP (of &quot;EHLO&quot;) wordt gespecificeerd en het domein dat door het adres van de &quot;terugkeer-Weg&quot;(of &quot;MAIL VAN&quot;) kopbal wordt gespecificeerd, die ook het stuiteradres is. Op grond van verschillende overwegingen kan slechts met een van deze waarden rekening worden gehouden; wij adviseren ervoor te zorgen dat beide bronnen het zelfde domein specificeren.

Het controleren van SPF verstrekt een evaluatie van de geldigheid van het domein van de afzender:

* **Geen**: Er kan geen evaluatie worden uitgevoerd.
* **Neutraal**: Het gevraagde domein laat geen evaluatie toe.
* **Doorgeven**: Het domein wordt als authentiek beschouwd.
* **Mislukt**: Het domein wordt vervalst en het bericht zou moeten worden verworpen.
* **SoftFail**: Het domein is waarschijnlijk gesmeed, maar het bericht mag niet alleen op basis van dit resultaat worden afgewezen.
* **TempError**: Een tijdelijke fout heeft de evaluatie gestopt. Het bericht kan worden verworpen.
* **PermError**: De SPF-records van het domein zijn ongeldig.

Opgemerkt zij dat de verslagen die op het niveau van de DNS servers worden gemaakt tot 48 uren kunnen vergen om in aanmerking worden genomen. Deze vertraging hangt af van hoe vaak de DNS geheime voorgeheugens van de ontvangende servers worden verfrist.

## DKIM {#dkim}

DKIM (DomainKeys Identified Mail)-verificatie is een opvolger van SPF. Het gebruikt openbare - zeer belangrijke cryptografie die de ontvangende e-mailserver toestaat om te verifiëren dat een bericht in feite werd verzonden door de persoon of de entiteit het beweert werd verzonden door, en of de berichtinhoud binnen tussen de tijd werd veranderd het oorspronkelijk werd verzonden (en DKIM &quot;ondertekend&quot;) en de tijd het werd ontvangen. Deze standaard gebruikt doorgaans het domein in de kop &quot;Van&quot; of &quot;Afzender&quot;.

DKIM komt uit een combinatie DomainKeys, Yahoo! en Cisco identificeerde de authentificatieprincipes van de Post van Internet en wordt gebruikt om de authenticiteit van het afzenderdomein te controleren en de integriteit van het bericht te waarborgen.

DKIM heeft **DomainKeys**-verificatie vervangen.

Voor het gebruik van DKIM zijn enkele voorwaarden vereist:

* **Beveiliging**: Versleuteling is een belangrijk element van de DKIM. Om het veiligheidsniveau van DKIM te verzekeren, is 1024b de beste praktijken geadviseerde encryptiegrootte. De lagere sleutels DKIM worden niet beschouwd als geldig door de meerderheid van toegangsleveranciers.
* **Reputatie**: Reputatie is gebaseerd op IP en/of het domein, maar de minder transparante DKIM selecteur is ook een zeer belangrijk element dat in overweging moet worden genomen. Het is belangrijk dat u de kiezer kiest: vermijden dat de &quot; wanbetaling &quot; , die door iedereen kan worden gebruikt en dus een zwakke reputatie heeft , behouden blijft . U moet een verschillende selecteur voor **behoud versus verwervingsmededelingen** en voor authentificatie uitvoeren.

Meer informatie over de DKIM-voorwaarde bij het gebruik van Campaign Classic in [deze sectie](/help/additional-resources/acc-technical-recommendations.md#dkim-acc).

## DMARC {#dmarc}

DMARC (Domain-based Message Authentication, Reporting and Conformance) is de meest recente vorm van e-mailverificatie en is afhankelijk van zowel SPF- als DKIM-verificatie om te bepalen of een e-mail wel of niet wordt verzonden. DMARC is uniek en krachtig op twee belangrijke manieren:

* Conformiteit - het staat de afzender toe om ISPs op te dragen wat met om het even welk bericht te doen dat er niet in slaagt voor authentiek te verklaren (bijvoorbeeld: niet aanvaarden).
* Het melden - het verstrekt de afzender van een gedetailleerd rapport dat alle berichten toont die authentificatie DMARC, samen met het &quot;Van&quot;domein en IP adres ontbrak dat voor elk wordt gebruikt. Dit staat een bedrijf toe om wettige e-mail te identificeren die authentificatie ontbreekt en één of ander type van &quot;moeilijke situatie&quot;(bijvoorbeeld, toevoegend IP adressen aan hun SPF verslag), evenals de bronnen en de prevalentie van phishingpogingen op hun e-maildomeinen vereist.

>[!NOTE]
>
>DMARC kan hefboomwerking de rapporten die door [250ok](https://250ok.com/) worden geproduceerd.

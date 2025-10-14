---
title: Verificatie
description: Leer meer op SPF, DKIM, en de authentificatiemethodes DMARC.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 03609139-b39b-4051-bcde-9ac7c5358b87
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# Verificatie

## SPF {#spf}

SPF (het Kader van het Beleid van de Afzender) is een norm van de e-mailauthentificatie die de eigenaar van een domein toestaat om te specificeren welke e-mailservers e-mail namens dat domein mogen verzenden. Deze standaard gebruikt het domein in de &quot;terugkeer-Weg&quot;kopbal van e-mail (die ook als &quot;Omhulsel van&quot;adres wordt bedoeld).

>[!NOTE]
>
>U kunt [&#x200B; dit externe hulpmiddel &#x200B;](https://www.kitterman.com/spf/validate.html) gebruiken om een SPF verslag te verifiëren.

SPF is een techniek die, tot op zekere hoogte, u toelaat om ervoor te zorgen dat de domeinnaam die in een e-mail wordt gebruikt niet wordt vervalst. Wanneer een bericht van een domein wordt ontvangen, wordt de DNS server van het domein gevraagd. De reactie is een kort verslag (het SPF verslag) dat details welke servers worden gemachtigd om e-mail van dit domein te verzenden. Als wij veronderstellen dat slechts de eigenaar van het domein de middelen heeft om dit verslag te veranderen, kunnen wij in overweging nemen dat deze techniek niet het afzenderadres om toelaat te vervalsen, minstens niet het deel van het recht van &quot;@&quot;.

In definitieve [&#x200B; RFC 4408 specificatie &#x200B;](https://www.rfc-editor.org/info/rfc4408), worden twee elementen van het bericht gebruikt om het domein te bepalen dat als afzender wordt beschouwd: het domein dat door het bevel van SMTP &quot;HELO&quot;(of &quot;EHLO&quot;wordt gespecificeerd) en het domein dat door het adres van de &quot;terugkeer-Weg&quot;(of &quot;MAIL VAN&quot;) kopbal wordt gespecificeerd, die ook het stuitadres is. Met verschillende overwegingen kunt u alleen rekening houden met een van deze waarden. We raden u aan ervoor te zorgen dat beide bronnen hetzelfde domein opgeven.

Het controleren van SPF verstrekt een evaluatie van de geldigheid van het domein van de afzender:

* **niets**: Geen evaluatie kon worden uitgevoerd.
* **Neutral**: Het domein waarop wordt gevraagd laat evaluatie niet toe.
* **pas** over: Het domein wordt beschouwd als authentiek.
* **Fail**: Het domein wordt gesmeed en het bericht zou moeten worden verworpen.
* **SoftFail**: Het domein wordt waarschijnlijk gesmeed maar het bericht zou niet moeten worden verworpen uitsluitend gebaseerd op dit resultaat.
* **TempError**: Een tijdelijke fout hield de evaluatie tegen. Het bericht kan worden verworpen.
* **PermError**: De verslagen SPF van het domein zijn ongeldig.

Opgemerkt zij dat de verslagen die op het niveau van de DNS servers worden gemaakt tot 48 uren kunnen vergen om in aanmerking worden genomen. Deze vertraging hangt af van hoe vaak de DNS geheime voorgeheugens van de ontvangende servers worden verfrist.

## DKIM {#dkim}

DKIM (DomainKeys Identified Mail)-verificatie is een opvolger van SPF. Het gebruikt openbare - zeer belangrijke cryptografie die de ontvangende e-mailserver toestaat om te verifiëren dat een bericht in feite werd verzonden door de persoon of de entiteit het beweert werd verzonden door, en of de berichtinhoud binnen tussen de tijd werd veranderd het oorspronkelijk werd verzonden (en DKIM &quot;ondertekend&quot;) en de tijd het werd ontvangen. Deze standaard gebruikt doorgaans het domein in de kop &quot;Van&quot; of &quot;Afzender&quot;.

DKIM komt uit een combinatie DomainKeys, Yahoo! en Cisco identificeerde de authentificatieprincipes van de Post van Internet en wordt gebruikt om de authenticiteit van het afzenderdomein te controleren en de integriteit van het bericht te waarborgen.

DKIM verving **authentificatie 0&rbrace; DomainKeys.**

Voor het gebruik van DKIM zijn enkele voorwaarden vereist:

* **Veiligheid**: De encryptie is een zeer belangrijk element van DKIM. Om het veiligheidsniveau van DKIM te verzekeren, is 1024b de beste praktijken geadviseerde encryptie grootte. De lagere sleutels DKIM worden niet beschouwd als geldig door de meerderheid van toegangsleveranciers.
* **Reputatie**: De Reputatie is gebaseerd op IP en/of het domein, maar de minder transparante selecteur DKIM is ook een zeer belangrijk element dat in aanmerking moet worden genomen. Het is belangrijk de kiezer te kiezen: zorg dat u de standaardkiezer, die door iedereen kan worden gebruikt, niet behoudt en dus een zwakke reputatie heeft. U moet een verschillende selecteur voor **behoud vs. verwervingsmededelingen** en voor authentificatie uitvoeren.

Leer meer op voorwaarde DKIM wanneer het gebruiken van Campaign Classic in [&#x200B; deze sectie &#x200B;](/help/additional-resources/acc-technical-recommendations.md#dkim-acc).

## DMARC {#dmarc}

DMARC (Domain-based Message Authentication, Reporting and Conformance) is de meest recente vorm van e-mailverificatie en is afhankelijk van zowel SPF- als DKIM-verificatie om te bepalen of een e-mail wel of niet wordt verzonden. DMARC is uniek en krachtig op twee belangrijke manieren:

* Conformiteit - het staat de afzender toe om ISPs op te dragen wat met om het even welk bericht te doen dat er niet in slaagt voor authentiek te verklaren (bijvoorbeeld: keur het niet goed).
* Het melden - het verstrekt de afzender van een gedetailleerd rapport dat alle berichten toont die authentificatie DMARC, samen met het &quot;Van&quot;domein en IP adres ontbrak dat voor elk wordt gebruikt. Dit staat een bedrijf toe om wettige e-mail te identificeren die authentificatie ontbreekt en één of ander type van &quot;moeilijke situatie&quot;(bijvoorbeeld, toevoegend IP adressen aan hun SPF verslag), evenals de bronnen en de prevalentie van phishingpogingen op hun e-maildomeinen vereist.

>[!NOTE]
>
>DMARC kan hefboomwerking de rapporten die door [&#x200B; worden geproduceerd 250ok &#x200B;](https://250ok.com/).

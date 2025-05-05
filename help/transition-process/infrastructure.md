---
title: Infrastructuur
description: Leer wat nodig is om een e-mailinfrastructuur correct te bouwen.
topics: Deliverability
jira: KT-7052
thumbnail: kt7052.jpg
doc-type: article
activity: understand
role: Admin, Leader
level: Beginner
team: ACS
exl-id: 4025d95c-cc77-4e0c-9904-aaf60019b18c
source-git-commit: 6b312cdbba496818337c97ec4f42962aea757901
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 1%

---

# Infrastructuur

Succesvolle prestaties zijn afhankelijk van een sterke basis. E-mailinfrastructuur is een kernelement. Een goed geconstrueerde e-mailinfrastructuur omvat meerdere componenten, namelijk domein(en) en IP-adres(sen). Deze onderdelen zijn als de machine achter de e-mails die je verzendt en zijn vaak het anker van het versturen van reputatie. Leveringsconsultants zorgen ervoor dat deze elementen tijdens de implementatie op de juiste wijze worden ingesteld, maar vanwege het faam-element is het belangrijk dat u over deze basiskennis beschikt.

## Instellen en strategie van domeinen {#domain-setup-and-strategy}

De tijden zijn veranderd, en sommige ISPs (zoals Gmail en Yahoo) neemt nu domeinreputatie als extra punt op wanneer het komt om e-mailreputatie aan een afzender vast te maken. Uw domeinreputatie is gebaseerd op uw verzendend domein in plaats van uw IP adres. Dit betekent dat uw merk belangrijkheid neemt wanneer het over ISP het filtreren besluiten komt.

Een deel van het onboarding proces voor nieuwe afzenders op de platforms van de Adobe omvat vestiging uw verzendende domeinen en het verzekeren dat uw infrastructuur behoorlijk wordt gevestigd. U zou met een deskundige moeten werken op welke domeinen u op lange termijn van plan bent te gebruiken. Hier volgen enkele tips die een goede domeinstrategie vormen:

* Wees zo duidelijk en weerspiegelend mogelijk van het merk met het domein u kiest zodat de gebruikers niet verkeerd de post als spam identificeren. Sommige voorbeelden zijn newsletter.foo.com, receipts.foo.com enzovoort.
* U zou uw ouder of collectief domein niet moeten gebruiken aangezien het de levering van post van uw organisatie aan ISPs kon beïnvloeden.
* U kunt overwegen een subdomein van het bovenliggende domein te gebruiken om het verzendende domein te legitimeren.
* Scheid uw subdomeinen voor Transactionele en het berichtcategorieën van de Marketing. Dit zal uw e-mailverkeer op een betrouwbaardere basis helpen stromen aangezien ISPs deze verzendende methode zoekt, die een bekende e-mailbeste praktijk is en hoogst geadviseerd.

## IP-strategie {#ip-strategy}

Het is belangrijk om een goed gestructureerde IP strategie te vormen helpen een positieve reputatie vestigen. Het aantal IPs en de opstelling varieert afhankelijk van uw bedrijfsmodel en marketing doelstellingen. Werk samen met een deskundige om een duidelijke strategie te ontwikkelen om van rechts te beginnen. Houd rekening met het volgende:

* **teveel IPs** kan reputatie kwesties teweegbrengen aangezien het een gemeenschappelijke tactiek van spammers aan **sneeuwschoen** is, die een tactiek is door spammers wordt gebruikt waar het verkeer over vele IPs wordt verspreid om de levering van spampost te maximaliseren. Alhoewel u geen spammer bent, zou u als één kunnen kijken als u teveel IPs gebruikt, vooral als die IPs geen vroeger verkeer heeft gehad.
* **Te weinig IPs** kan productiekwesties veroorzaken en potentieel reputatiekwesties teweegbrengen. De productie varieert door ISP. Hoeveel en hoe snel ISP bereid is om te aanvaarden is typisch gebaseerd op hun infrastructuur en het verzenden van reputatiedrempels.
* Het scheiden van verkeer voor overseinentypen is zeer belangrijk. Het is belangrijk om, op een absoluut minimum, afzonderlijke marketing en transactionele post op afzonderlijke IP pools te behandelen.
* Afhankelijk van uw poststrategie, kan het ook raadzaam zijn om verschillende producten of marketing stromen op verschillende IP pools te scheiden als uw reputatie drastisch verschillend is. Sommige markten segmenteren ook per regio. Het scheiden van IP voor verkeer met een lagere reputatie zal niet de reputatie kwestie oplossen, maar het zal kwesties met uw &quot;goede&quot;reputatie e-mailleveringen verhinderen. Want je wilt je goede publiek niet opofferen voor een riskantere.

## Feedbackloops {#feedback-loops}

Achter de schermen verwerken Adobe platforms gegevens over stormen, klachten, afmelden en nog veel meer. De opstelling van deze terugkoppelt lijnen is een belangrijk aspect aan leverbaarheid. Klachten kunnen een reputatie beschadigen, dus u moet e-mailadressen versturen die uw klachten van het doelpubliek registreren. Het is belangrijk om op te merken dat Gmail deze gegevens niet terugverstrekt. De lijst unsubscribe kopballen en overeenkomst het filtreren zijn vooral belangrijk voor abonnees Gmail, die nu de meerderheid van abonneegegevensbestanden bestaan.

## Verificatie {#authentication}

De authentificatie is het proces dat ISPs gebruikt om de identiteit van een afzender te bevestigen. De twee meest gebruikte verificatieprotocollen zijn [!DNL Sender Policy Framework] (SPF) en [!DNL DomainKeys Identified Mail] (DKIM). Deze zijn niet zichtbaar aan het eind - gebruiker maar helpen ISPs filtere-mail van geverifieerde afzenders. [!DNL Domain-based Message Authentication Reporting and Conformance] (DMARC) wint populariteit, hoewel zijn beleid nog niet door alle ISPs in hun reputatie wordt opgenomen.

### SPF

[!DNL Sender Policy Framework] (SPF) is een authentificatiemethode die de eigenaar van een domein toestaat om te specificeren welke postservers zij gebruiken om post van dat domein te verzenden.

### DKIM

[!DNL Domain Keys Identified Mail] (DKIM) is een authentificatiemethode die wordt gebruikt om vervalste afzenderadressen (algemeen genoemd spoofing) te ontdekken. Als DKIM wordt toegelaten, staat het de ontvanger toe om te bevestigen of de afzender gemachtigd is om post van dat domein te verzenden.

### DMARC

[!DNL Domain-based Message Authentication, Reporting and Conformance] (DMARC) is een verificatiemethode waarmee domeineigenaars hun domein kunnen beschermen tegen ongeoorloofd gebruik. DMARC gebruikt SPF of DKIM of allebei om een domeineigenaar toe te staan om te controleren wat met post gebeurt die authentificatie ontbreekt: geleverd, quarantined, of verworpen.

## Productspecifieke bronnen

**Campaign**

* Leer hoe te om een subdomain volledig aan Adobe Campaign Classic of Norm in [ te delegeren deze sectie ](/help/additional-resources/ac-domain-name-setup.md).
* [ Controlebord: Volledige subdomain delegatie (leerprogramma) ](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html?lang=nl-NL) - *Leer hoe te om een subdomain aan Adobe Campaign Classic volledig te delegeren.*
* [ Controlebord: Volledige subdomain delegatie (leerprogramma) ](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html?lang=nl-NL) - *Leer hoe te om een subdomain aan Adobe Campaign Standard volledig te delegeren.*
* Leer meer bij het uitvoeren van een terugkoppel lijn voor een instantie van het Campaign Classic in [ deze sectie ](/help/additional-resources/acc-technical-recommendations.md#feedback-loop-acc).

## Aanvullende bronnen

* Leer meer op SPF, DKIM, en DMARC authentificatiemethodes in [ deze sectie ](/help/additional-resources/authentication.md).
* Leer meer bij het verhogen van uw e-mailreputatie met IP opwarmen in [ deze sectie ](/help/additional-resources/increase-reputation-with-ip-warming.md).

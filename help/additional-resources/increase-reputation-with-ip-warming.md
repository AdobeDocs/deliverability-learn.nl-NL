---
title: Uw e-mailreputatie verbeteren met opwarming van IP-adressen
description: Leer waarom het belangrijk is om uw e-mailreputatie met IP te verbeteren opwarmen, en hoe te te te werk te gaan voor optimale leverbaarheid.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: b553a13e-2055-4abc-b784-fd52792380d0
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 2%

---

# Uw e-mailreputatie verbeteren met opwarming van IP-adressen

<!--Increase your email reputation with IP warming

## IP Warming overview

In the Adobe Deliverability Consulting and Deliverability Operations teams, we have a vested interest in helping new Campaign customers be as successful as possible as they embark on the route of an IP warming process. If you’ve never been a part of such a project, you may have a lot of questions about it. Let’s get down to the details!-->

## Aan de slag

Adobe vereist klanten om hun configuratie te delen om het team van de Leverbaarheid van de Adobe te helpen uw uniek programma begrijpen. De vragen die we stellen, zijn ontworpen om het Adobe-leverbaarheidsteam een idee te geven van uw reputatie en e-mailvolume. Zonder een concreet inzicht in uw bedrijfsmodel, e-mailmarketing doelstellingen en reputatie metriek, zullen wij geen strategie kunnen aanpassen en er is risico op leveringsproblemen.

Aan het begin zult u uw eigen toegewijde IP-adressen (Internet Protocol) krijgen. In de context van het verzenden van e-mail, is een IP adres de route die wordt gebruikt om uw e-mailberichten aan uw klanten te leveren. IP de adressen en de domeinen worden gebruikt om afzenders op een netwerk aan ontvangende ISPs te identificeren. Adobe wijst het juiste aantal speciale IP-adressen toe voor het verzenden van e-mails op basis van uw verzendvolume, e-mailprogramma&#39;s, praktijken voor gegevenssegmentatie en uw contract.

**Verwante onderwerpen:**
* [Zorgen voor een soepele overgang bij de overstap naar een ander e-mailplatform](../../help/transition-process/switching-email-platforms.md)
* [IP-strategie](../../help/transition-process/infrastructure.md#ip-strategy)
* [ISP-specifieke overwegingen tijdens &#39;IP warming&#39;](../../help/transition-process/isp-specific-considerations-during-ip-warming.md)

## IP Warm: Waarom is het gedaan? {#why-ip-warming}

De Dienstverleners van Internet (ISPs) of de Leveranciers van de Brievenbus (MBPs) nemen voorzorgsmaatregelen wanneer zij onbekende IP ontdekken en domein verzenden. Dit is standaardprocedure verbonden aan om het even welke nieuwe verzendende IPs, ongeacht afzendertype. ISPs/MBPs zet IP en verzendend domein onder hoog toezicht om te bepalen als de e-mails die van dit IP en domein worden verzonden spam of niet zijn.  Dit is standaardprocedure verbonden aan om het even welke nieuwe verzendende IPs, ongeacht afzendertype.

ISPs onderzoekt zorgvuldig het verzendende volume, verzendt frequentie, klachten, en stuitert tarieven die uit deze berichten worden geproduceerd. Deze worden allemaal nauwkeurig gecontroleerd, omdat het indicatoren zijn van de reputatie van de verzender - of het nu goed of slecht is.

Het onderzoek van deze gegevenspunten vergt natuurlijk tijd en kan niet over een paar dagen worden afgerond. Reputatie wordt in de loop der tijd opgebouwd. Dit proces is alsof je een vreemdeling thuis laat. Zou u bedenkingen hebben bij het binnenkomen van iemand die u nog nooit hebt ontmoet?

Het antwoord is zeer waarschijnlijk ja. Je zou deze persoon en hun motieven willen analyseren. Betekenen ze schade? Zijn ze een bedreiging? ISPs doet het zelfde om hun netwerk tegen kwaadwillig of ongewenst verkeer te beschermen. De positieve reputatie metriek helpt u een lange weg in een succesvol IP opwarend proces gaan. Daarom benadrukken wij het belang van het eerst verzenden van kleine e-mailvolumes en het eerst verzenden naar uw zeer betrokken klanten. Voor meer op dit, zie [Doelcriteria wanneer het verzenden van nieuw verkeer](/help/transition-process/targeting-criteria.md).

Het verzenden van grote hoeveelheden e-mail van een gloednieuwe IP of IPs direct uit de poort is een slechte praktijk en zal u waarschijnlijk sommige leveringsproblemen veroorzaken. Het is belangrijk om op te merken dat zelfs als u kleine volumes gaat verzenden en deze geleidelijk wilt verhogen zoals aanbevolen, u de best practices voor e-mail nog steeds moet volgen.

![](../../help/assets/ip-warming-volume-trend.png)

## Machtiging tot e-mail (expliciete opt-in)

Dit is het belangrijkste onderdeel van het beheren en vergroten van een e-maillijst voor abonnees. Naarmate anti-spamwetten internationaal groeien en alomvattend worden, moet het primair de aandacht van een markteur zijn om ervoor te zorgen dat zij expliciete (of uitdrukkelijke) toestemming van elke abonnee op hun lijst hebben gekregen. Elke abonnee heeft er actief mee ingestemd e-mails van je merk te ontvangen. Dit verschilt van impliciete toestemming wanneer een persoon aan een e-maillijst wordt toegevoegd na het nemen van een actie die zich niet expliciet voor een e-mailprogramma had aangemeld.

Meer informatie over het beleid [Acceptable Use Policy](https://www.adobe.com/legal/terms/aup.html) van Adobe.

## Reputatiemetriek: Wat zoekt ISPs?

ISPs gebruikt verfijnde technologie om opgeleide besluiten over al dan niet te nemen om e-mail te leveren zij van externe netwerken ontvangen. Soms hebben ze ingewikkelde en merkgebonden algoritmen in hun gereedschapset om hen in dit proces te helpen.

Enkele onderzochte gegevenspunten zijn:

* Spam-overvullingen
* treffers voor Lijst van gewezen personen
* E-mailgrenzen
* Abonnementsbetrokkenheid

ISPs vereist specifieke technische configuraties die zich op hun beleid en beste praktijken richten. Adobe configureert uw IPs en gedelegeerde subdomeinen om u als verantwoordelijke en vertrouwde op afzender te identificeren. Dit wordt [e-mailverificatie](/help/transition-process/infrastructure.md#authentication) genoemd. De hulp van de authentificatie ontvangers bevestigen of een afzender de rechten heeft om van dat IP of domein te verzenden.

De authentificatie staat ISPs toe om te bevestigen dat het bedrijf dat van een domein of IP verzendt het recht heeft om dit te doen. Het is in feite gedaan om uw identiteit te bewijzen en ervoor te zorgen dat u zich niet als iemand anders voordoet en dat iemand anders u niet pretendeert te zijn.

Bij Adobe, zullen wij SPF en DKIM door gebrek vormen en wij zullen DMARC door verzoek vormen. ISPs verwijzing SPF en DKIM als primaire vormen van authentificatie. Vele ISPs neemt ook DMARC (op domein-gebaseerde Authentificatie van het Bericht, Rapportering &amp; Conformiteit) in hun het filtreren besluiten op. Niet-geverifieerde e-mailberichten worden niet noodzakelijkerwijs geblokkeerd, maar er worden wel extra filters op toegepast.

## IP Warm: Wat te verwachten

### Gedraaide of geblokkeerde post

Spammers verzenden voortdurend van nieuwe IPs - zij zullen door een pool van IPs branden tot zij worden gesloten en het proces op een andere pool van IPs herhalen. Dientengevolge, behandelt ISPs verkeer dat van nieuwe IPs zorgvuldig wordt verzonden. Zij blokkeren IPs van het verzenden van grote hoeveelheid e-mail omdat zij vermoeden dat dit kwaadwillige activiteit die door spammers wordt uitgevoerd is.

Daarom is het niet ongebruikelijk om uitgestelde of vertraagde berichten te ontvangen wanneer u begint van uw nieuwe IPs te posten. Na een paar pogingen, wordt het bericht gewoonlijk goedgekeurd en geleverd.

Het bereiken van een normale stroom van verkeer door aan ISPs die nieuwe afzenders uitstelt kan een paar dagen vergen. Maar toch, stop niet het verzenden van post - blijf zich op slechts het verzenden naar uw hoogst betrokken e-mailabonnees concentreren.

In zeldzame gevallen, blokkeert ISP de nieuwe afzender. Adobe volgt uw account en als een dergelijk blok wordt vermoed, richt hij zich tot de ISP om te proberen de situatie op de best mogelijke manier te verhelpen.

Houd er rekening mee dat consistentie hier van essentieel belang is. Onregelmatige verzendende volumepatronen en onregelmatige mailingpatronen veroorzaken onderweg enkele uitdagingen op het gebied van de leverbaarheid.

### Klachten

[](/help/metrics/complaints.md) Klacht wanneer een abonnee een e-mail als spam door zijn e-mailprogramma etiketteert. Dit verzendt een bericht naar ISP over de klachtenactiviteit. Als er genoeg van deze klachten zijn die in ISP komen, dat ISP zal handelen om zijn klanten te beschermen - misschien blokkeert vele e-mails van het krijgen aan de abonnees of een deel van e-mails aan de bulkomslag in tegenstelling tot abonnees&#39; inboxes. Als uw bezorgingsprobleem wordt veroorzaakt door klachten, is het belangrijk om te bepalen waarom ontvangers een klacht indienen.

Abonnees klagen om verschillende redenen. Soms wil een abonnee geen e-mail meer van u ontvangen, bijvoorbeeld omdat hij of zij het gevoel heeft dat hij of zij teveel berichten over hetzelfde onderwerp ontvangt, het bericht niet verwacht of zich niet meer aanmeldt voor het ontvangen van uw e-mails.

### Geldigheid van gegevens

De harde stuitingen komen voor wanneer u naar een niet te leveren adres bij ISP verzendt. Een adres kan om vele redenen, zoals een fout in het typen van het adres of het post aan een adres zijn dat eerder actief was maar na een periode van inactiviteit gesloten of geëindigd is.

Als u een aanzienlijk aantal harde grenzen tegenkomt, is het belangrijk om te begrijpen waarom. Controleer hoe de adressen zijn verzameld en bevestig dat u hiervoor toestemming hebt gegeven. Soms sluiten mensen hun e-mailaccount en geven ze geen melding aan diegenen die dat adres op hun marketinglijst hebben.

### Engagement

ISPs zoekt verenigbaar volume en goede gegevenskwaliteit. U zult langzaam en gestaag het verkeer in de komende vier tot acht weken verhogen. Soms is er meer of minder tijd nodig op basis van uw volume en doelen, maar meestal is het minstens 8 weken bezig.

Het e-mailverkeer moet langzaam en gestaag worden geïmplementeerd, elke week groter tot de volledige lijst is verzonden. Bovendien zal elk segment het programma tot voltooiing volgen. Begin met de meest recente abonnees eerst, en eindig met de minst betrokken abonnees het laatst. Gelieve te merken ook op dat bepaalde ISPs een meer aangepaste benadering wegens kan vereisen hoe zij nieuw verkeer behandelen.

Meer informatie over [betrokkenheid](/help/engagement.md).

## De cursus blijven

U kunt worden verleidt om het proces van IP opwarmen te versnellen door meer volume te verzenden dan wordt geadviseerd, verwaarloosend om tijd door te brengen identificerend uw meest betrokken abonnees en nalaten deze abonnees eerst in een inspanning te posten om een positieve reputatie op te bouwen. Ik verzoek u dit verzoek te weerstaan. Het zal u op de lange termijn niet helpen.

Het is heel belangrijk om uw hoogst betrokken (met e-mail te beginnen!) abonnees slechts voor de beginstadia van IP opwarming. Deze klanten zijn uw waardevolste klanten en hun neiging om uw e-mails te openen zal helpen beginnen ISPs te tonen dat u een teller bent die post verzendt die interessant en gezocht is. Het toont ook ISPs dat u door de regels en volgende beste praktijken speelt.

## Conclusie

Onthoud: IP Warm is een marathon - geen sprint!  Hoewel het proces omslachtig en tijdrovend kan lijken, zou het meer werk zijn om te proberen een reputatie te herstellen die wordt beschadigd door het niet volgen van beproefde en echte e-mailbeste praktijken.

Hoe beter uw verzendpraktijken zijn en hoe hoger uw reputatie bij ISP&#39;s is, des te groter de kans dat uw e-mails worden bezorgd. De opwarming van IP en het op gang brengen, samen met het volgen van de beste praktijken voor het ontwerp van uw post, zullen helpen uw inbox levering optimaliseren.

Ons wereldwijde leverbaarheidsteam is uw partner in dit proces en zal u tijdens deze opwarmingsfase van het IP helpen om u voor succes te positioneren.

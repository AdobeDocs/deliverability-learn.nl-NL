---
title: Domeinnaam instellen
description: Leer hoe u een subdomein kunt delegeren naar Adobe Campaign.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 4d52d197-d20e-450c-bfcf-e4541c474be4
source-git-commit: 82f7254a9027f79d2af59aece81f032105c192d5
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 2%

---

# Domeinnaam instellen

In dit document worden de zakelijke en technische vereisten beschreven voor het instellen en delegeren van domeinnamen. U moet een subdomein selecteren voor het verzenden van e-mail en eventueel een extern onderliggend subdomein voor het hosten van webcomponenten (bestemmingspagina&#39;s, opt-out-pagina) voor het Adobe-platform dat u gebruikt.

>[!NOTE]
>
>U kunt ook nieuwe subdomeinen instellen met het Configuratiescherm (beschikbaar als bèta). Lees meer in [deze sectie](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/setting-up-new-subdomain.html?lang=nl-NL#must-read).

## Subdomeinen

Met Adobe, kan de digitale marketing echt de contextafhankelijke motor worden die het de marketingprogramma van de klantenovereenkomst van uw merk drijft.  E-mail blijft de basis van digitale marketingprogramma&#39;s. Het is echter moeilijker geworden om de inbox te bereiken dan ooit.

Creërend subdomain voor e-mailcampagnes staat brands toe om verschillende types van verkeer (marketing versus collectief bijvoorbeeld) in specifieke IP pools en met specifieke domeinen te isoleren, die het [ IP opwarmingsproces ](../../help/additional-resources/increase-reputation-with-ip-warming.md) zullen versnellen en over het algemeen leverbaarheid zullen verbeteren. Als u een domein deelt en het wordt geblokkeerd of aan de lijst van gewezen personen toegevoegd, zou het uw collectieve postlevering kunnen beïnvloeden. Nochtans, zullen de kwesties van de reputatie of de blokken op een domein specifiek voor uw e-mailmarketing mededelingen enkel die stroom van e-mail beïnvloeden.  Als u uw hoofddomein als afzender of het adres &#39;Van&#39; voor meerdere e-mailstreams gebruikt, kan de e-mailverificatie ook worden verbroken, waardoor uw berichten worden geblokkeerd of in de spammap worden geplaatst.

### Delegatie

De domeinnaamdelegatie is een methode die de eigenaar van een domeinnaam (technisch: een DNS-zone) toestaat om een onderverdeling van de domeinnaam (technisch: een DNS-zone eronder, die een subzone kan worden genoemd) aan een andere entiteit te delegeren. In feite geldt dat als een klant de zone &#39;example.com&#39; afhandelt, hij de subzone &#39;marketing.example.com&#39; kan delegeren aan Adobe Campaign.

Dit betekent dat de DNS van Adobe Campaign servers volledige bevoegdheid op slechts die streek en niet het top-level domein zullen hebben. DNS-servers van Adobe Campaign bieden gezaghebbende antwoorden op vragen over domeinnamen in die zone, zoals &quot;t.marketing.example.com&quot; zelf, maar niet &quot;www.example.com&quot;.

Door een subdomein voor gebruik met Adobe Campaign te delegeren, kunnen de cliënten op Adobe vertrouwen om de DNS infrastructuur te handhaven die wordt vereist om aan industrie-standaardleveringsvereisten voor hun e-mailmarketing verzendende domeinen te voldoen, terwijl het blijven DNS voor hun interne e-maildomeinen handhaven en controleren.  Bij subdomeindelegatie is het mogelijk:

Clients kunnen hun merkafbeelding behouden door een DNS-alias met domeinnamen te gebruiken
Adobe om autonoom alle technische beste praktijken uit te voeren om de leverbaarheid tijdens het e-mailen volledig te optimaliseren

## DNS-instellingsopties

Om een op wolken-gebaseerde beheerde dienst te verlenen, moedigt de Adobe cliënten sterk aan om subdomain delegatie te gebruiken wanneer het opstellen van Adobe Campaign.  Nochtans, biedt de Adobe cliënten een alternatieve optie - de opstelling van CNAME - voor het vormen DNS aan.

| Optie | Beschrijving | Verantwoordelijkheden Adobe | Verantwoordelijkheden van klanten |
|--- |------- |--- |--- |
| Subdomeindelegatie naar Adobe Campaign | De cliënt delegeert subdomain (email.example.com) aan Adobe. In dit scenario, kan de Adobe de Campagne als beheerde dienst leveren door alle aspecten van DNS te controleren en te handhaven die voor het leveren, het teruggeven, en het volgen van e-mailcampagnes worden vereist. | Volledig beheer van het subdomein en alle DNS-records die voor Adobe Campaign zijn vereist. | Correcte delegatie van het subdomein aan Adobe |
| Gebruik van CNAME&#39;s | De cliënt leidt tot subdomain en gebruikt CNAMEs om aan Adobe-specifieke verslagen te richten.  Met deze configuratie delen Adobe en de klant de verantwoordelijkheid voor het onderhoud van DNS. | Beheer van DNS-records vereist voor Adobe Campaign. | Creatie en controle van subdomain en creatie/beheer van de CNAME verslagen die voor Adobe Campaign worden vereist. |

## Vereiste DNS-records

| Recordtype | Doel | Voorbeelden van record/inhoud |
|--- |--- |--- |
| MX | E-mailservers opgeven voor binnenkomende berichten | <i> email.example.com </i></br><i> 10 binnenkomend.email.example.com </i> |
| SPF (TXT) | Beleidskader voor afzender | <i> email.example.com </i></br> &quot;v=spf1 redirect=__spf.campagne.adobe.com&quot; |
| DKIM (TXT) | DomainKeys Identified Mail | <i> cliënt._domainkey.email.example.com </i></br> &quot;v=DKIM1; k=rsa;&quot; &quot;DKIMPUBLICKEY HERE&quot; |
| Gegevens van hosts (A) | Pagina&#39;s spiegelen, afbeeldingen hosten en koppelingen bijhouden, alle verzendende domeinen | m.email.example.com IN A 123.111.100.99 </br> t.email.example.com IN A 123.111.100.98 </br> email.example.com IN A 123.11.100.97 |
| DNS omkeren (PTR) | Wijst de cliëntIP adressen aan een cliënt brandde hostname toe | 18.101.100.192.in-addr.arpa domeinnaamaanwijzer r18.email.example.com |
| CNAME | Biedt een alias voor een andere domeinnaam | t1.email.example.com is een alias voor t1.email.example.campaign.adobe.com |


De op domein-gebaseerde Authentificatie van het Bericht, het Melden, en de Conformiteit (DMARC) wordt geadviseerd om e-mailafzenders voor authentiek te verklaren en ervoor te zorgen dat de bestemmings-e-mailsystemen berichten vertrouwen die van uw domein worden verzonden.

Voorbeeld van DMARC TXT-record:

```
_dmarc.email.example.com

“v=DMARC1; p=none; rua=mailto:mailauth-reports@myemail.com” 
```

U kunt DMARC handmatig implementeren of contact opnemen met de Adobe om u te helpen bij het instellen van DMARC voor uw merk.

## Installatievereisten

### Subdomeindelegatie

Dit vereist de cliënt om subdomain in hun DNS servers tot stand te brengen en de naamservers voor dit subdomain te bepalen die die door Adobe worden gehandhaafd.  Bijvoorbeeld, zal een cliënt de waarvan belangrijkste domeinnaam &quot;example.com&quot;is en die het beheer van &quot;marketing.example.com&quot;aan Adobe voor zijn e-mailleveringen wil delegeren deze delegatie moeten materialiseren om de volgende typeverslagen aan zijn DNS toe te voegen:

```
marketing.example.com. NS a.ns.campaign.adobe.com.
marketing.example.com. NS b.ns.campaign.adobe.com.
marketing.example.com. NS c.ns.campaign.adobe.com.
marketing.example.com. NS d.ns.campaign.adobe.com.
```

Het delegeren van een domeinnaam impliceert dat dit domein zal worden gewijd aan het leveren van e-mail via het Adobe Campaign platform, en daarom niet voor andere middelen kan worden gebruikt (bijvoorbeeld het verzenden van e-mail van een andere e-mailinfrastructuur).

Tijdens het opstellingsproces, zal de Adobe ervoor zorgen het domein aan de Adobe inkomende e-mailinfrastructuur in bijlage is om de terugkomende e-mails te beheren en te verwerken die terug naar deze domeinen (MX type DNS verslagconfiguratie) komen.

### Gebruik van CNAME&#39;s

Als de cliënt verkiest om CNAMEs eerder dan afgevaardigde te gebruiken subdomain aan Adobe, tijdens de opstellingsfase, zal de Adobe de verslagen verstrekken die in de cliëntDNS servers moeten worden geplaatst en zal de overeenkomstige waarden in Adobe Campaign DNS servers vormen.

## Algemene vereisten voor implementatie

Wanneer het uitvoeren van een nieuwe onderneming marketing oplossing, zijn er vereisten voor extern gerichte componenten.  Dit zijn onder andere het hosten van bestemmingspagina&#39;s en webformulieren, het instellen van koppelingen en webpagina&#39;s die moeten worden bijgehouden, het weergeven van spiegelpagina&#39;s en het configureren van een uitschakelpagina.

Hoewel deze vereisten worden beheerd via componenten die door zowel de Adobe als de klant worden gehost, bevatten ze URL&#39;s die door de ontvangers van de e-mails kunnen worden gezien.  Om te voorkomen dat URL&#39;s de onderliggende technische oplossing of hostingprovider aangeven, kunnen subdomeinen worden ingesteld om dit transparant te maken voor de ontvangers van de e-mails.  Als u bijvoorbeeld naar een URL kijkt, bijvoorbeeld http://www.customer.com/, is het domein &quot;www.customer.com&quot;.  Het subdomein van dit zou &quot;www&quot;zijn.

### Subdomeinvereisten

Bepaal de subdomein(s) die moeten worden gebruikt voor URL&#39;s met branding (spiegelpagina&#39;s en URL&#39;s bijhouden) in de Adobe Campaign-toepassing.  Bepaal ook wat &quot;van Adres&quot;, &quot;van Naam&quot;en &quot;antwoord-aan Adres&quot;voor elk subdomein op e-mailleveringen zal zijn.

Vul de onderstaande tabel in. De eerste regel is slechts een voorbeeld.

| Subdomein | Van adres | Van naam | Reageren op adres |
|--- |--- |--- |--- |
| emails.customer.com | news@emails.customer.com | Klant | customercare@customer.com |
| </br> | </br> | </br> | </br> |

>[!NOTE]
>
>* Het doel van het gebied &quot;Antwoord-aan Adres&quot;is wanneer u de ontvanger op een verschillend adres wilt antwoorden dan &quot;van Adres&quot;.  Terwijl niet een vereist gebied, adviseert de Adobe sterk dat &quot;antwoord-aan Adres&quot;geldig en met een gecontroleerd brievenbus verbonden zijn.  Deze brievenbus moet door de klant worden ontvangen.  Dit kan bijvoorbeeld een ondersteuningsmailbox zijn, customercare@customer.com, waar e-mails worden gelezen en waarop wordt gereageerd.
>* Als de klant geen &quot;Antwoord-aan Adres&quot;kiest, dan is het standaardadres altijd `<tenant>-<type>-<env>@<subdomain>`.
>* Wanneer &quot;antwoord-aan Adres&quot;opstelling deze manier is, zullen de antwoorden naar een ongecontroleerde brievenbus worden verzonden.
>* Wanneer het verzenden van e-mails van Adobe Campaign, wordt de brievenbus &quot;van Adres&quot;niet gecontroleerd en de marketing gebruikers kunnen tot deze brievenbus toegang hebben. Adobe Campaign biedt ook niet de mogelijkheid om e-mails die in dit postvak zijn ontvangen automatisch te beantwoorden of door te sturen.
>* Het adres van de Campagne van/van de Afzender en het adres van de Fout kunnen niet &quot;misbruik&quot;of &quot;postmaster&quot;zijn.

## Subdomeinen delegeren

De subdomein(s) die zijn gekozen voor gebruik voor het Adobe Campaign-platform, moeten worden gedelegeerd door het maken van NS-records (four Name Server).  Hierdoor kan het subdomein correct worden gedelegeerd aan de Adobe.  Hieronder ziet u een voorbeeld van een subdomeindelegatie en de respectievelijke DNS-instructies.  Vervang &quot;emails.customer.com&quot; door het subdomein dat u wilt delegeren.  Houd er rekening mee dat het subdomein uniek moet zijn en niet al door een andere partij kan worden gebruikt (bijvoorbeeld een bestaande ESP of MSP).

| Gedelegeerde subdomein | DNS-instructies |
|--- |--- |
| `<subdomain>` | `<subdomain>` a.ns.campaign.adobe.com. </br> `<subdomain>` b.ns.campaign.adobe.com. </br> `<subdomain>` c.ns.campaign.adobe.com. </br> `<subdomain>` d.ns.campaign.adobe.com. |

## Bijhouden, pagina&#39;s spiegelen, bronnen

Zodra de e-mail die subdomain(s) verzendt behoorlijk aan Adobe Campaign wordt/worden gedelegeerd, zal het team van TechOps van de Adobe twee of meer laag-vlakke domeinen tot stand brengen om het volgen en spiegel van pagina&#39;s onafhankelijk te beheren.

| Type | Domein |
|--- |--- |
| Pagina&#39;s spiegelen | m.`<subdomain>` |
| Tracking | t.`<subdomain>` |
| Bronnen | res.`<subdomain>` |

## Implementatie in de cloud (optioneel)

Dit geldt alleen als de Adobe Campaign Classic volledig via Adobe in de cloud wordt gehost.  Dit is een optionele configuratie.

Alle enquêtes, webformulieren en bestemmingspagina&#39;s die moeten worden ontwikkeld, worden volledig door Adobe Campaign gehost in de cloud.  Indien nodig, kan een extra subdomein aan Adobe (bijvoorbeeld, web.customer.com) worden gedelegeerd om voor om het even welke Webcomponenten binnen het hulpmiddel te gebruiken.  Het subdomein moet uniek zijn en kan niet door een andere partij worden gebruikt (bijvoorbeeld een bestaande ESP of MSP).

| Gedelegeerde subdomein | DNS-instructies |
|--- |--- |
| `<subdomain>` | `<subdomain>` a.ns.campaign.adobe.com.</br>`<subdomain>` b.ns.campaign.adobe.com.</br>`<subdomain>` c.ns.campaign.adobe.com.</br>`<subdomain>` d.ns.campaign.adobe.com. |

>[!NOTE]
>
>Standaard wordt voor alle webcomponenten in het hulpprogramma het eerste subdomein gebruikt dat is gedelegeerd om te worden gebruikt voor e-mail.

## Implementatie van cloudberichten (optioneel)

Als de Adobe Campaign Classic marketing instantie op gebouw bij de klant wordt ontvangen, zal de klant extra technische configuraties moeten maken.

Alle enquêtes, webformulieren en bestemmingspagina&#39;s die moeten worden ontwikkeld, worden beheerd via het marketingexemplaar van Adobe Campaign, waar de verslagen van de ontvangers aanwezig zijn.

De extra DNS configuratie van CNAME wordt vereist om extern gerichte Webcomponenten op te stellen die door de marketing instantie van Adobe Campaign worden ontvangen.  Hierdoor kunnen webcomponenten (bijvoorbeeld web.customer.com) voor iedereen toegankelijk zijn voor internet en worden gemarkeerd met het domein van de klant.

Firewall(s) moeten ook worden geconfigureerd om toegang te verlenen tot de marketinginstantie van Adobe Campaign die deze webcomponenten host (op poort 80 of 443).

**Beste praktijken Recommendations:**

Het subdomein voor de host van webcomponenten is zichtbaar voor klanten. Zorg er dus voor dat het op de juiste wijze van branding is voorzien en eenvoudig te onthouden is, aangezien het mogelijk handmatig moet worden ingevoerd, bijvoorbeeld: https://web.customer.com.
Als formulieren moeten worden gehost op beveiligde pagina&#39;s (HTTPS), is aanvullende technische configuratie vereist, zoals hieronder beschreven.

| Gedelegeerde subdomein | DNS-instructies |
|--- |--- |
| `<subdomain>` | `<subdomain>` CNAME `<internal customer server>` |

## Gerenderde services

Na deze delegaties zorgt de Adobe ervoor dat de volgende diensten worden uitgevoerd voor elk gedelegeerd of CNAME-aliased verzendend domein:

* Maken van postmaster@ en misbruik@-postvakken
* Opstelling van terugkoppellijnen voor het gedelegeerde domein
* Op verzoek, zal de Adobe ook een verslag DMARC zoals gespecificeerd vormen. Uw Deliverability Consultant kan u helpen bij het ontwerpen van een langetermijnbeleid en -plan voor DMARC voor uw verzendende domeinen.
De parameters die door Adobe worden vastgesteld zijn slechts geldig vanaf het tijdstip dat de delegatie werd voltooid en vervolgens door Adobe werd geverifieerd, en blijven functioneel.  In alle Adobe Campaign Cloud-aanbiedingen wordt domeinnaamdelegatie standaard opgenomen.

## Facturerings- en uitvoeringsvoorwaarden

* Afhankelijk van het oorspronkelijke contract en het gekozen type pakket kunnen andere delegaties worden opgenomen, naast de delegaties die als standaard naast deze oorspronkelijke delegatie zijn opgenomen,
* Buiten deze delegaties worden extra delegaties gefactureerd,
* De factureringsmethode voor deze extra delegaties brengt extra maandelijkse kosten met zich mee, zoals bepaald in het oorspronkelijke contract.

Deze delegaties worden aanvaard mits de CLIENT de bijbehorende domeinnamen kiest die via het Adobe Campaign-instrument aan leveringen worden toegewezen, en de delegatievoorwaarden die in het desbetreffende document worden beschreven, correct worden toegepast.

## Stopzetting van diensten

De CLIENT zal op elk moment schriftelijk kunnen eisen dat hij niet langer van de delegatiediensten profiteert en de nodige DNS-configuraties zelf kan overnemen.

Als dit zou moeten gebeuren, zal de Adobe de CLIENT van een raming voorzien die het aantal de dienstdagen detailleert noodzakelijk om op niet domein-delegatie wijze terug te keren.

Adobe wordt vrijgesteld van aansprakelijkheid voor de betrokkenheid van het bovengenoemde leveringspercentage als de klant de hierboven vermelde toezeggingen niet nakomt.

De beëindiging van de Dienst van de Marketing Cloud zal automatisch tot het eind van domeindelegaties, en DNS onderhoud voor die domeinen door Adobe leiden.

## Subdomeinen controleren met het Configuratiescherm

Zodra subdomeinen voor uw instantie worden gevormd, kunt u hen controleren gebruikend het Controlebord.

Op deze manier kunt u alle subdomeinen weergeven die u aan Adobe Campaign hebt gedelegeerd en kunt u de vernieuwing van hun SSL-certificaten aanvragen.

Raadpleeg de [desbetreffende documentatie](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/monitoring-subdomains.html?lang=nl-NL#subdomains-and-certificates) voor meer informatie.

>[!NOTE]
>
>[ Controlebord ](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=nl) is beschikbaar aan klanten die Adobe Managed Services slechts gebruiken.

---
title: SSL-certificaataanvraagproces
description: Leer hoe u SSL-certificaten installeert op de subdomeinen die u aan Adobe hebt gedelegeerd.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 8a78abd3-afba-49a7-a2ae-8b2c75326749
source-git-commit: 0be68f5674904aa105985a6e5fc4771c41f7fe48
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 1%

---

# Proces voor het aanvragen van een SSL-certificaat

Zodra u een domein aan Adobe voor het verzenden van e-mail (zie [ de naamopstelling van het Domein ](/help/additional-resources/ac-domain-name-setup.md)) hebt gedelegeerd, zal Adobe bepaalde subdomeinen voor specifieke functies creëren en gebruiken.

Bijvoorbeeld, als u *email.example.com* aan Adobe voor het verzenden van e-mails hebt gedelegeerd, zal Adobe subdomeinen zoals het volgende tot stand brengen:
* *t.email.example.com* - voor het volgen verbindingen
* *m.email.example.com* - voor spiegelpagina&#39;s
* *res.email.example.com* - voor ontvangen middelen (zoals beelden)

Het wordt geadviseerd om **deze domeinen via SSL (HTTPS) te beveiligen**. Onbeveiligde koppelingen (HTTP) zijn immers kwetsbaar voor interceptie en zullen waarschuwingen afgeven aan moderne browsers.

Als u SSL-certificaten op deze subdomeinen wilt installeren, dient u een CSR-bestand aan te vragen en vervolgens SSL-certificaten aan te schaffen die Adobe kan installeren of vernieuwen.

>[!CAUTION]
>
>Alvorens een SSL certificaat te installeren, zorg ervoor u zich van de eerste vereisten bewust bent die op [ worden vermeld deze pagina ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html?lang=nl#installing-ssl-certificate).
>
>Adobe biedt alleen ondersteuning voor maximaal 2048-bits certificaten. 4096-bits certificaten worden nog niet ondersteund.

## Woordenlijst

| Term | Beschrijving |
|--- |--- |
| CA (Certificate Authority) | Een SSL-certificaatprovider die digitale certificaten uitgeeft aan organisaties of personen nadat hun identiteit is geverifieerd, zoals DigiCert, Symantec, enz.<ul><li>Een vertrouwde CA wordt meestal beschouwd als een derde CA die een basiscertificaat uitgeeft.</li><li>Als het certificaat is ondertekend door dezelfde organisatie/onderneming die het certificaat gebruikt, wordt het geclassificeerd als niet-vertrouwde CA, zelfs als het SSL-certificaten zijn, zoals zelfondertekende certificaten.</li></ul> |
| Kettingcertificaat | Een certificaat dat een basiscertificaat en een of meer tussenliggende certificaten bevat, wordt een certificaatketen (of gekoppeld) genoemd. |
| CSR (certificaataanvraag) | Een blok gecodeerde tekst dat aan een Instantie van het Certificaat wordt gegeven wanneer het vragen van een SSL certificaat. Deze wordt meestal gegenereerd op de server waarop het certificaat is geïnstalleerd. |
| DER (Distinguished Encoding Rules) | Een extensietype voor certificaten. De extensie .der wordt gebruikt voor binaire DER-gecodeerde certificaten. Deze bestanden kunnen ook de extensie .cer of .crt ondersteunen. |
| EV-certificaat (Extended Validation) | Een certificaat EV is een nieuw type van certificaat dat wordt ontworpen om phishingaanvallen te verhinderen. Hiervoor is uitgebreide validatie van uw bedrijf en van de persoon die het certificaat bestelt vereist. |
| Certificaat voor hoge zekerheid | De CA geeft hoge-betrouwbaarheidscertificaten uit nadat de eigendom van de domeinnaam en de geldige bedrijfsregistratie zijn geverifieerd. |
| Intermediaire CA | Een certificeringsinstantie van tussentijdse certificaten die in een kettingcertificaat zijn opgenomen. |
| Intermediair certificaat | Een certificeringsinstantie geeft certificaten uit in de vorm van een boomstructuur. Het basiscertificaat is het bovenste certificaat van de boomstructuur. Elk certificaat tussen uw certificaat en het basiscertificaat wordt een keten- of tussenliggend certificaat genoemd. |
| Lage-betrouwbaarheidsverklaring | Een certificaat met lage betrouwbaarheid, ook wel domeingevalideerd certificaat genoemd, bevat alleen de domeinnaam in het certificaat (en niet de naam van het bedrijf of de organisatie). |
| PEM (Privacy Enhanced Mail) | Een certificaat met de extensie .pem dat ASCII-gegevens (Base64) bevat. Dergelijke certificaten beginnen met een regel &quot; - - - - - - BEGIN CERTIFICAAT - - - - -&quot;. |
| Basiscertificaat | Een certificeringsinstantie geeft certificaten uit in de vorm van een boomstructuur. Het basiscertificaat is het bovenste certificaat van de boomstructuur. |
| SAN (Alternatieve naam onderwerp) | Alternatieve onderwerpnamen zijn aanvullende hostnamen (sites, IP-adressen, algemene namen, enz.) die moeten worden ondertekend als onderdeel van één SSL-certificaat. |
| Zelfondertekend certificaat | Een certificaat dat is ondertekend door de persoon die het heeft gemaakt in plaats van een vertrouwde certificeringsinstantie. Zelfondertekende certificaten kunnen hetzelfde coderingsniveau inschakelen als een certificaat dat is ondertekend door een CA, maar er zijn twee grote nadelen:<ul><li>De verbinding van een bezoeker kan worden gekaapt, zodat een aanvaller alle verzonden gegevens kan bekijken (waardoor het doel van het coderen van de verbinding wordt omzeild)</li><li> Het certificaat kan niet worden ingetrokken, zoals een vertrouwd certificaat kan.</li></ul> |
| SSL (Secure Sockets Layer) | De standaardbeveiligingstechnologie voor het tot stand brengen van een gecodeerde koppeling tussen een webserver en een browser. |
| Certificaat met jokertekens | Een vervangingscertificaat kan een onbeperkt aantal eerste-niveausubdomeinen op één enkele domeinnaam, zoals *.adobe.com beveiligen. |

## Belangrijkste stappen

1. Vraag om een CSR-bestand (Certificate Signing Request) en geef Adobe de vereiste informatie (land, staat, plaats, naam van de organisatie, naam van de organisatie enz.).
1. Valideer het CSR-bestand dat door Adobe is gegenereerd en controleer of alle gegevens die u hebt opgegeven correct zijn.
1. Gebruik de details CSR om een certificaat te produceren dat door een vertrouwde op CertificatieInstantie <!--taking care of asking for using the subjectAltName SSL extension (SAN) if it is for several domain names, and get/purchase the resulting certificate (ideally) in PEM format for Apache server--> wordt ondertekend.
1. Valideer het SSL-certificaat en controleer of dit overeenkomt met de CSR.
1. Geef het SSL-certificaat door aan Adobe, die het zal installeren.
1. Test of het SSL-certificaat is geïnstalleerd voor elk beveiligd subdomein.
1. Controleer de geldigheidsperiode van het SSL-certificaat.
1. Werk een specifieke configuratie in Adobe Campaign bij.

## Gedetailleerd proces

### Vereisten

U moet de domeinnamen en de functies (bijhouden, pagina&#39;s spiegelen, webapps enz.) identificeren om te beveiligen.
>[!NOTE]
>
>Adobe kan u helpen bij het definiëren van de domeinnamen en -functies die moeten worden gebruikt. Neem voor meer informatie contact op met uw Adobe-accountteam.

### Stap 1 - krijg een CSR- dossier

Voer de onderstaande stappen uit om een CSR-bestand (Certificate Signing Request) te verkrijgen.

* Als u toegang tot het [ Controlebord ](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=nl) hebt, volg de instructies op [ deze pagina ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html?lang=nl#subdomains-and-certificates) om een Csr- dossier van het Controlebord te produceren en te downloaden.

* Als dat niet het geval is, maakt u een ondersteuningsticket via https://adminconsole.adobe.com/ om een CSR-bestand op te halen van de Adobe Customer Care voor de vereiste subdomein(s).

Hier volgen enkele aanbevolen procedures:

* Eén aanvraag per gedelegeerd subdomein opheffen.
* Het is mogelijk om veelvoudige subdomeinen in één enkel CSR- verzoek te combineren, maar slechts binnen het zelfde milieu. Bijvoorbeeld, in Campaign Classic, zijn de marketing server, [ midsourcing server ](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/install-campaign-on-prem/mid-sourcing-server.html), en de [ uitvoeringsinstantie ](https://experienceleague.adobe.com/docs/campaign-classic/using/transactional-messaging/configure-transactional-messaging/configuring-instances.html#execution-instance) drie afzonderlijke milieu&#39;s.
* U moet een nieuwe CSR krijgen alvorens om het even welke SSL certificaatvernieuwing. Gebruik geen oud CSR-bestand van een jaar geleden of meer.

U moet de volgende informatie opgeven.

>[!CAUTION]
>
>Alle velden die in de onderstaande tabellen worden vermeld, moeten worden ingevuld. Anders, kan het CSR- verzoek niet worden verwerkt.

**Informatie om van de hulp van het team van Adobe te voorzien:**

| Te verstrekken informatie | Voorbeeldwaarde | Opmerking |
|--- |--- |--- |
| Clientnaam | My Company Inc. | Naam van uw organisatie. Dit veld wordt door Adobe gebruikt voor het bijhouden van uw aanvraag (het maakt geen deel uit van het CSR/SSL-certificaat). |
| URL Adobe Campaign-omgeving | https://client-mid-prod1.campaign.adobe.com | Adobe Campaign instance URL. |
| Gemeenschappelijke Naam [ CN ] | t.subdomain.customer.com | Dit kan om het even welke relevante domeinen zijn, maar gewoonlijk het volgende domein. |
| De Alternatieve Naam van het onderwerp [ San ] | t.subdomain.customer.com | Zorg ervoor dat u het volgende subdomein opneemt als een SAN. |
| De Alternatieve Naam van het onderwerp [ San ] | m.subdomain.customer.com | |
| De Alternatieve Naam van het onderwerp [ San ] | res.subdomain.customer.com | |

**Informatie door uw intern team van IT/SSL te verstrekken:**

| Te verstrekken informatie | Voorbeeldwaarde | Opmerking |
|--- |--- |--- |
| Land [ C ] | VS | Dit moet een code van twee letters zijn. Heb toegang tot de volledige landlijst [ hier ](https://www.ssl.com/csrs/country_codes/).</br>*Nota: Voor Verenigd Koninkrijk, gebruik GB (niet VK).* |
| Staat (of de Naam van de Provincie) [ ST ] | Illinois | Indien van toepassing. De waarde moet een volledige naam zijn en mag niet worden afgekort. |
| Plaats/Localiteitsnaam [ L ] | Chicago | |
| De Naam van de organisatie [ O ] | ACME | |
| De Naam van de eenheid van de organisatie [ OU ] | IT | |

>[!NOTE]
>
>Vervang &quot;subdomain.customer.com&quot;met uw gedelegeerde subdomain, en de andere voorbeeldwaarden met de aangewezen waarden.

### Stap 2 - Valideer het CSR-bestand

Nadat u uw verzoek met de relevante informatie hebt verzonden, genereert Adobe een CSR-bestand (Certificate Signing Request).

De tekst in het resulterende Csr- dossier moet met **beginnen&quot;—BEGIN CERTIFICAATVERZOEK—&quot;**.

Voer de volgende stappen uit nadat u het CSR-bestand van Adobe hebt ontvangen:

1. Kopieer en plak de tekst van het CSR-bestand in een onlindecoder, zoals https://www.sslshopper.com/csr-decoder.html, <!--https://www.certlogik.com/decoder/,--> of https://www.entrust.net/ssl-technical/csr-viewer.cfm.
Alternatief, kunt u het ** bevel gebruiken OpenSSL plaatselijk op een machine van Linux.
1. Controleer of alle controles zijn gelukt.
1. Controleer of de juiste parameters en domeinnamen zijn opgenomen.
1. Controleer of alle andere gegevens overeenkomen met de gegevens die u hebt opgegeven bij het verzenden van uw verzoek.

### Stap 3 - Het SSL-certificaat genereren

Wanneer het CSR-bestand is opgegeven, moet u een SSL-certificaat voor de juiste domeinen aanschaffen en genereren met behulp van het CSR-bestand.

* Het SSL-certificaat:
   * moet in Apache PEM-formaat zijn;
   * mag niet langer zijn dan 2048 bits;
   * moet worden ondertekend door een geldige certificeringsinstantie (certificeringsinstantie);
   * moeten alle SAN&#39;s (Alternatieve namen van onderwerp) bevatten, zoals vermeld in het CSR-bestand.
* Als er een of meer tussenliggende certificaten zijn, moet u het basiscertificaat en alle tussenliggende certificaten aan Adobe verstrekken.
* U kunt elke geldigheidsperiode van een certificaat instellen, maar Adobe raadt u aan deze lang genoeg te kiezen (bijvoorbeeld twee jaar).

>[!NOTE]
>
>Als u uw eigen interne hulpmiddelen of een portaal gebruikt die door CA wordt verstrekt om het certificaat te verzoeken, zorg ervoor om de zelfde details te gebruiken zoals die in het Csr- verzoek worden verstrekt om om het even welke vertragingen of discrepanties in het proces van de certificaatgeneratie te vermijden.

### Stap 4 - Valideer het SSL-certificaat

Nadat het SSL-certificaat is gegenereerd, moet u het valideren voordat u het naar Adobe verzendt. Hiervoor voert u de volgende stappen uit:

1. Controleer of het certificaat de extensie .pem heeft. Als dit niet het geval is, zet het in formaat PEM om. U kunt de omzetting maken gebruikend *OpenSSL*.
1. Bevestig dat het certificaat met **&quot;&quot;—BEGIN CERTIFICAAT—&quot;** begint.
1. Kopieer de certificaattekst naar een online decoder, zoals https://www.sslshopper.com/certificate-decoder.html of https://www.entrust.net/ssl-technical/csr-viewer.cfm.
Alternatief, kunt u het ** bevel gebruiken OpenSSL plaatselijk op een machine van Linux. Voor meer op dit, verwijs naar [ deze externe pagina ](https://www.shellhacks.com/decode-ssl-certificate/).
1. Zorg ervoor dat het certificaat correct is omgezet, inclusief de Common Name, SAN, Issuer and Validity Period.
1. Als de SSL certificaatcontrole succesvol is, controleer dat het certificaat CSR gebruikend [ deze website ](https://www.sslshopper.com/certificate-key-matcher.html) aanpast: selecteer **Controle als CSR en een certificaat** aanpassen, en uw certificaat en uw CSR op de overeenkomstige gebieden ingaan. Ze moeten overeenkomen.

### Stap 5 - Vraag de SSL certificaatinstallatie aan

* Als u toegang tot het [ Controlebord ](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=nl) hebt, volg de instructies op [ deze pagina ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html?lang=nl#installing-ssl-certificate) om het certificaat aan Controlebord te uploaden.

* Anders maakt u een ander ondersteuningsticket via https://adminconsole.adobe.com/ om Adobe te verzoeken het certificaat op de Adobe-server(s) te installeren.

U moet het volgende opgeven:

* Het certificaatbestand, het basiscertificaat en eventuele tussentijdse certificaten (die aan het ticket zijn gehecht), bij voorkeur in Apache PEM-indeling.
* Het aantal van het vorige kaartje van de Steun dat voor CSR wordt opgeheven.
* Dezelfde gegevens die zijn verstrekt voor het CSR-ticket (inclusief algemene naam, instantie-URL, staat, plaats/locatie, naam van organisatie, naam van organisatie-eenheid, enz.).

### Stap 6 - Test de SSL certificaatinstallatie

Nadat het SSL-certificaat is geïnstalleerd en bevestigd door Adobe Customer Care, moet u controleren of het voor alle URL&#39;s is geïnstalleerd.

Voer de tests hieronder uit alvorens het SSL installatiekaartje te sluiten. Zorg ook ervoor u om het even welke specifieke configuratie zoals die in [ wordt opgedragen deze sectie ](#update-configuration) bijwerkt.

Navigeer naar de volgende URL&#39;s in uw browser (vervang &quot;subdomain.customer.com&quot; door uw subdomein):

* https://subdomain.customer.com/r/test (voor [ Webtoepassingen ](https://experienceleague.adobe.com/docs/campaign-classic/using/designing-content/web-applications/about-web-applications.html) slechts subdomeinen - is niet op e-mailsubdomeinen van toepassing)
* https://t.subdomain.customer.com/r/test
* https://m.subdomain.customer.com/r/test
* https://res.subdomain.customer.com/r/test

Een succesvol resultaat geeft omgevingsinformatie en de adresbalk in de URL geeft aan dat de verbinding veilig is. Het volgende bericht wordt bijvoorbeeld weergegeven in Google Chrome:

![](../../help/assets/ssl-google-successful-result.png)

Als het SSL-certificaat niet correct is geïnstalleerd, wordt de volgende waarschuwing weergegeven:

![](../../help/assets/ssl-google-unsuccessful-result.png)

### Stap 7 - controleer de geldigheid van het certificaat

U kunt de geldigheidsperiode van het certificaat in uw browser controleren. Bijvoorbeeld, in Google Chrome, klik **Veilig** > **Certificaat**.

Het is uw verantwoordelijkheid om de geldigheidsperiode te controleren. Adobe raadt u aan een proces te implementeren om de vervaldatum van certificaten te controleren. Leer meer op wat gebeurt wanneer uw SSL certificaat in [ dit artikel ](https://www.thesslstore.com/blog/what-happens-when-your-ssl-certificate-expires/) verloopt.

* Maak een ondersteuningsticket om een bijgewerkt certificaat aan te vragen ten minste twee weken voor de vervaldatum van het certificaat. U te hoeven om geen extra CSR aan te vragen, tenzij de details CSR zijn veranderd.

* Als u toegang tot het [ Controlebord ](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=nl) hebt, en als uw milieu door Adobe in een milieu van AWS wordt ontvangen, kunt u het Controlebord gebruiken om het certificaat te vernieuwen alvorens het verloopt. Lees meer in [deze sectie](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/monitoring-ssl-certificates.html#monitoring-certificates).

### Stap 8 - werk om het even welke specifieke configuratie bij {#update-configuration}

Als u zeker weet dat de aangevraagde SSL-certificaten correct zijn geïnstalleerd, kunt u alle referenties in Adobe Campaign bijwerken van HTTP naar HTTPS.

>[!NOTE]
>
>Voor Campaign Classic, wordt URLs om bij te werken hoofdzakelijk gevestigd in de [ tovenaar van de Plaatsing ](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/initial-configuration/deploying-an-instance.html#deployment-wizard) en in de [ Externe rekeningen ](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/accessing-external-database/external-accounts.html) (het volgen, spiegelpagina, en openbare middeldomeinen). Voor Campaign Standard, verwijs naar [ Brandende configuratie ](https://experienceleague.adobe.com/docs/campaign-standard/using/administrating/application-settings/branding.html#about-brand-identity).

Zodra configuraties zijn bijgewerkt, worden nieuwe e-mailberichten verzonden met HTTPS-URL&#39;s in plaats van met HTTP. Als u wilt controleren of de URL&#39;s nu veilig zijn, kunt u snel de volgende tests uitvoeren:

* Upload een afbeelding vanuit Adobe Campaign. Nadat de afbeelding is geüpload, moet de geretourneerde URL HTTPS zijn.
* Maak een test-e-maillevering, inclusief een koppeling naar een spiegel, sommige afbeeldingen, tekst en een koppeling voor niet-abonnementen. Verzend de e-mail naar een externe e-mailid (zoals uw Gmail-adres). Na ontvangst opent u de e-mail en zorgt u ervoor dat alle koppelingen in de e-mail correct worden geopend in het HTTPS-formulier (niet HTTP), zonder dat er een SSL-certificaatwaarschuwing of -fout optreedt.

## Productspecifieke bronnen

**Campaign Classic**

* [ Controlebord: Het toevoegen van SSL certificaten (leerprogramma) ](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html) - leer hoe te om SSL certificaten toe te voegen om uw subdomeinen te beveiligen.

**Campaign Standard**

* [ Controlebord: Het toevoegen van SSL certificaten (leerprogramma) ](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html) - leer hoe te om SSL certificaten toe te voegen om uw subdomeinen te beveiligen.

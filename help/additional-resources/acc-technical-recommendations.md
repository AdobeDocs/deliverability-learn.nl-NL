---
title: Campaign Classic - Technische aanbevelingen
description: Ontdek de technieken, configuraties en gereedschappen die u kunt gebruiken om de prestaties met Adobe Campaign Classic te verbeteren.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 39ed3773-18bf-4653-93b6-ffc64546406b
source-git-commit: 097f41c29e189c2a8abf79e65ec322d39a2213db
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 1%

---

# Campaign Classic - Technische aanbevelingen {#technical-recommendations}

Hieronder vindt u een aantal technieken, configuraties en gereedschappen die u kunt gebruiken om de snelheid van uw producten te verbeteren wanneer u Adobe Campaign Classic gebruikt.

## Configuratie {#configuration}

### DNS omkeren {#reverse-dns}

Adobe Campaign controleert of omgekeerde DNS voor een IP adres wordt gegeven en dat dit correct naar IP wijst.

Een belangrijk punt in de netwerkconfiguratie zorgt ervoor dat correcte omgekeerde DNS voor elk van de IP adressen voor uitgaande berichten wordt bepaald. Dit betekent dat voor een bepaald IP adres, er een omgekeerd DNS verslag (PTR verslag) met een passende DNS (een verslag van A) die terug naar het aanvankelijke IP adres van een lus voorzien is.

De domeinkeus voor omgekeerde DNS heeft een effect wanneer het behandelen van bepaalde ISPs. AOL accepteert, met name, alleen feedbackloops met een adres in hetzelfde domein als de omgekeerde DNS (zie [Feedbacklus](#feedback-loop)).

>[!NOTE]
>
>U kunt [dit externe gereedschap](https://mxtoolbox.com/SuperTool.aspx) om de configuratie van een domein te verifiëren.

### MX-regels {#mx-rules}

MX-regels (Mail eXchanger) zijn de regels die de communicatie tussen een verzendende server en een ontvangende server beheren.

Meer bepaald, worden zij gebruikt om de snelheid te controleren waarbij Adobe Campaign MTA (de Agent van de Overdracht van het Bericht) e-mails naar elk individueel e-maildomein of ISP (bijvoorbeeld, hotmail.com, comcast.net) verzendt. Deze regels zijn typisch gebaseerd op grenzen die door ISPs worden gepubliceerd (bijvoorbeeld, omvatten niet meer dan 20 berichten per elke verbinding SMTP).

>[!NOTE]
>
>Voor meer informatie over MX-beheer in Adobe Campaign Classic raadpleegt u [deze sectie](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/email-deliverability.html#mx-configuration).

### TLS {#tls}

TLS (Transport Layer Security) is een versleutelingsprotocol dat kan worden gebruikt om de verbinding tussen twee e-mailservers te beveiligen en de inhoud van een e-mailbericht te beschermen tegen lezen door andere personen dan de beoogde ontvangers.

### Domein van afzender {#sender-domain}

Als u het domein wilt definiëren dat wordt gebruikt voor de opdracht HELO, bewerkt u het configuratiebestand van de instantie (conf/config-instance.xml) en definieert u als volgt een kenmerk &quot;localDomain&quot;:

```
<serverConf>
  <shared>
    <dnsConfig localDomain="mydomain.net"/>
  </shared>
</serverConf>
```

MAIL VAN domein is het domein dat in technische stuitberichten wordt gebruikt. Dit adres wordt gedefinieerd in de implementatietovenaar of via de optie NmsEmail_DefaultErrorAddr.

### SPF-record {#dns-configuration}

Een SPF-record kan momenteel op een DNS-server worden gedefinieerd als een TXT-typerecord (code 16) of een SPF-typerecord (code 99). Een SPF-record heeft de vorm van een tekenreeks. Bijvoorbeeld:

```
v=spf1 ip4:12.34.56.78/32 ip4:12.34.56.79/32 ~all
```

bepaalt de twee IP adressen, 12.34.56.78 en 12.34.56.79, zoals gemachtigd om e-mails voor het domein te verzenden. **~all** betekent dat elk ander adres moet worden geïnterpreteerd als een SoftFail.

Recommendations voor het definiëren van een SPF-record:

* Toevoegen **~all** (SoftFail) of **-all** (Mislukt) aan het einde om alle andere servers dan de gedefinieerde te weigeren. Zonder dit, zullen de servers dit domein (met een Neutrale evaluatie) kunnen vervalsen.
* Niet toevoegen **ptr** (openspf.org beveelt aan dit als kostbaar en onbetrouwbaar te verhelpen).

>[!NOTE]
>
>Meer informatie over SPF in [deze sectie](/help/additional-resources/authentication.md#spf).

## Verificatie

>[!NOTE]
>
>Meer informatie over de verschillende vormen van e-mailverificatie vindt u in [deze sectie](/help/additional-resources/authentication.md).

### DKIM {#dkim-acc}

>[!NOTE]
>
>Voor gehoste of hybride installaties, als u een upgrade hebt uitgevoerd naar de [Enhanced MTA](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-emails/sending-an-email/sending-with-enhanced-mta.html#sending-messages), DKIM ondertekenen van e-mailverificatie wordt uitgevoerd door de Enhanced MTA voor alle berichten met alle domeinen.

Gebruiken [DKIM](/help/additional-resources/authentication.md#dkim) met Adobe Campaign Classic is de volgende voorwaarde vereist:

**Adobe Campaign-optiedeclaratie**: in Adobe Campaign is de persoonlijke sleutel DKIM gebaseerd op een DKIM-kiezer en een domein. Het is momenteel niet mogelijk om meerdere persoonlijke sleutels voor hetzelfde domein of subdomein te maken met verschillende kiezers. Het is niet mogelijk om te bepalen welk selecteerdomein/subdomein voor de authentificatie in noch het platform noch e-mail moet worden gebruikt. Het platform zal alternatief één van de privé sleutels selecteren, wat betekent de authentificatie een hoge kans heeft om te ontbreken.

* Als u DomainKeys voor uw instantie van Adobe Campaign hebt gevormd, moet u enkel selecteren **dkim** in de [Regels voor domeinbeheer](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html#email-management-rules). Indien niet, volg de zelfde configuratiestappen (privé/openbare sleutel) zoals voor DomainKeys (die DKIM verving).
* Het is niet noodzakelijk om zowel DomainKeys als DKIM voor het zelfde domein toe te laten aangezien DKIM een betere versie van DomainKeys is.
* De volgende domeinen valideren momenteel DKIM: AOL, Gmail.

## Feedbacklus {#feedback-loop-acc}

Een feedbacklijn werkt door op het ISP niveau een bepaald e-mailadres voor een waaier van IP adressen te verklaren die voor het verzenden van berichten worden gebruikt. ISP zal naar deze brievenbus, op een gelijkaardige manier verzenden zoals wat voor stuitberichten wordt gedaan, die berichten die door ontvangers als spam worden gemeld. Het platform moet zo worden geconfigureerd dat toekomstige leveringen aan gebruikers die een klacht hebben ingediend, worden geblokkeerd. Het is belangrijk dat zij niet langer contact met hen opnemen, ook al hebben zij niet de juiste opt-out-link gebruikt. Het is gebaseerd op deze klachten dat ISP een IP adres aan zijn lijst van gewezen personen zal toevoegen. Afhankelijk van ISP, zal een klachtentarief van rond 1% in het blokkeren van een IP adres resulteren.

Er wordt momenteel een standaard ontwikkeld voor het definiëren van de indeling van feedbacklusberichten: de [Misbruikrapportage-indeling (ARF)](https://tools.ietf.org/html/rfc6650).

Het implementeren van een feedbacklus voor een instantie vereist:

* Een brievenbus specifiek aan de instantie, die de stuiterende brievenbus kan zijn
* IP die adressen verzendt specifiek aan de instantie

Bij het implementeren van een eenvoudige feedbacklus in Adobe Campaign wordt de functionaliteit voor het stuiterende bericht gebruikt. De terugkoppelt lijnbrievenbus wordt gebruikt als stuiterende brievenbus en een regel wordt bepaald om deze berichten te ontdekken. De e-mailadressen van de ontvangers die het bericht als spam hebben gemeld, worden toegevoegd aan de quarantainelijst.

* Een stuiterende mailregel maken of wijzigen **Feedback_loop**, in **[!UICONTROL Administration > Campaign Management > Non deliverables Management > Mail rule sets]** om welke reden **Geweigerd** en het type **Hard**.
* Als een brievenbus speciaal voor de terugkoppel lijn is bepaald, bepaal de parameters om tot het toegang te hebben door een nieuwe externe rekening van de Steekproef te creëren Mails in **[!UICONTROL Administration > Platform > External accounts]**.

Het mechanisme is onmiddellijk operationeel voor het verwerken van kennisgevingen van klachten. Om ervoor te zorgen deze regel correct werkt, kunt u de rekeningen tijdelijk deactiveren zodat zij deze berichten niet verzamelen, dan controleren de inhoud van terugkoppelt lijnbrievenbus manueel. Voer op de server de volgende opdrachten uit:

```
nlserver stop inMail@instance,
nlserver inMail -instance:instance -verbose.
```

Als u gedwongen bent om één enkel te gebruiken terugkoppelt lijnadres voor veelvoudige instanties, moet u:

* Herhaal de ontvangen berichten op zo veel brievenbussen aangezien er instanties zijn,
* Heb elke brievenbus die door één enkele instantie wordt opgepakt,
* Vorm de instanties zodat zij slechts de berichten verwerken die hen aangaan: de instantieinformatie is inbegrepen in de bericht-identiteitskaart- kopbal van berichten die door Adobe Campaign worden verzonden en daarom ook in de terugkoppel lusberichten wordt gevestigd. Geef de opdracht **checkInstanceName** parameter in het dossier van de instantieconfiguratie (door gebrek, wordt de instantie niet geverifieerd en dit kan bepaald adres ertoe leiden om verkeerd in quarantined te zijn):

  ```
  <serverConf>
    <inMail checkInstanceName="true"/>
  </serverConf>
  ```

Met de Adobe Campaign-service voor leveringszekerheid wordt uw abonnement op feedbacklusservices beheerd voor de volgende ISP&#39;s: AOL, BlueTime, Comcast, Cox, EarthLink, FastMail, Gmail, Hotmail, HostedEmail, Libero, Mail.ru, MailTrust, OpenSRS, QQ, RoadRunner, Synacor, Telenor, Terra, UnitedOnline, USA, XS4ALL Yahoo, Yandex, Zoho.

## List-Unsubscribe {#list-unsubscribe}

### Info over List-Unsubscribe {#about-list-unsubscribe}

Een SMTP-header toevoegen met de naam **List-Unsubscribe** is verplicht voor een optimaal beheer van de leverbaarheid. Vanaf 1 juni 2024 moeten Yahoo en Gmail afzenders voldoen aan de Single-Click List-Unsubscribe. Om te begrijpen hoe te om lijst-Unsubscribe te vormen één-Klik gelieve te zien hieronder.


Deze kopbal kan als alternatief aan het &quot;Rapport als SPAM&quot;pictogram worden gebruikt. De koppeling wordt weergegeven als een niet-geabonneerde koppeling in de e-mailinterface.

Als u deze functie gebruikt, wordt uw reputatie beschermd en wordt feedback uitgevoerd als een abonnement opzeggen.

Als u List-Unsubscribe wilt gebruiken, moet u een bevellijn gelijkend op als volgt ingaan:

```
List-Unsubscribe: <mailto: client@newsletter.example.com?subject=unsubscribe?body=unsubscribe>
```

>[!CAUTION]
>
>Het bovenstaande voorbeeld is gebaseerd op de tabel met ontvangers. Als de gegevensbestandimplementatie van een andere lijst wordt gedaan, zorg ervoor om de bevellijn met de correcte informatie te herformuleren.

De volgende opdrachtregel kan worden gebruikt om een dynamisch object te maken **List-Unsubscribe**:

```
List-Unsubscribe: <mailto: %=errorAddress%?subject=unsubscribe%=message.mimeMessageId%>
```

Gmail, Outlook.com, en Microsoft Outlook steunen deze methode en een unsubscribe knoop is beschikbaar direct in hun interface. Deze techniek verlaagt de klachtenpercentages.

U kunt de **List-Unsubscribe** door:

* Direct [toevoegen van de bevellijn in het leveringsmalplaatje](#adding-a-command-line-in-a-delivery-template)
* [Een typologieregel maken](#creating-a-typology-rule)

### Een opdrachtregel toevoegen in een leveringssjabloon {#adding-a-command-line-in-a-delivery-template}

De bevellijn moet in de extra sectie van de kopbal van SMTP van e-mail worden toegevoegd.

Deze toevoeging kan in elke e-mail, of in bestaande leveringsmalplaatjes worden gedaan. U kunt ook een nieuwe leveringssjabloon maken die deze functionaliteit bevat.

* List-Unsubscribe: <mailto:unsubscribe@domain.com>
Als u op de koppeling Abonnement opzeggen klikt, wordt de standaard e-mailclient van de gebruiker geopend. Deze typologieregel moet worden toegevoegd aan een typologie die wordt gebruikt voor het maken van e-mail.

* List-Unsubscribe: <https://domain.com/unsubscribe.jsp>
Als u op de koppeling voor afmelden klikt, wordt de gebruiker omgeleid naar het afmeldingsformulier.
  ![afbeelding](/help/assets/ListUnsubscribe1.png)


### Een typologieregel maken {#creating-a-typology-rule}

De regel moet het manuscript bevatten dat de bevellijn produceert en het moet in de e-mailkopbal worden omvat.

>[!NOTE]
>
>We raden u aan een typologieregel te maken: de functionaliteit List-Unsubscribe wordt automatisch toegevoegd aan elke e-mail.

>[!NOTE]
>
>Leer hoe u in Adobe Campaign Classic typologische regels maakt [deze sectie](https://experienceleague.adobe.com/docs/campaign-classic/using/orchestrating-campaigns/campaign-optimization/about-campaign-typologies.html#typology-rules).

### Een-klik lijst opzeggen

Vanaf 1 juni 2024 moeten Yahoo en Gmail afzenders voldoen aan List-Unsubscribe (Engelstalig) met één klik. Om aan het één-Klik lijst-ophef vereiste te voldoen moeten de afzenders:

* Toevoegen in een &quot;List-Unsubscribe-Post: List-Unsubscribe=One-Click&quot;
* Een URI opnemen voor afmelden van koppeling
* De ontvangst van de reactie van de POST van HTTP van de ontvanger steunen, die Adobe Campaign steunt.

Om één-Klik lijst-Unsubscribe direct te vormen:

* Voeg toe in de volgende webtoepassing &quot;Niet-klikgerichte ontvangers afmelden&quot; 
* Ga naar Bronnen -> Online -> Webtoepassingen
* Upload &quot;Ontvangers zonder klik afmelden&quot; [XML](/help/assets/WebAppUnsubNoClick.xml.zip)

* Configureer List-Unsubscribe en List-Unsubscribe-Post
* Ga naar de sectie SMTP van de Eigenschappen van de Levering.
* Onder Extra Kopballen SMTP, ga in de bevellijnen (Elke kopbal zou op een afzonderlijke lijn moeten zijn) in:

```
List-Unsubscribe-Post: List-Unsubscribe=One-Click
List-Unsubscribe: <https//domain.com/webApp/unsubNoClick?id=<%= recipient.cryptidcamp %>>, <mailto: %=errorAddress%?
subject=unsubscribe%=message.mimeMessageId%>
```

In het bovenstaande voorbeeld wordt een List-Unsubscribe (Engelstalig) met één klik ingeschakeld voor ISP&#39;s die One-Click ondersteunen, terwijl ontvangers die geen ondersteuning bieden voor URL list-unsubscribe (URL-lijst afmelden) toch een aanvraag kunnen indienen om hun abonnement op te zeggen via e-mail.


### Creërend Typologieregel om lijst-Unsubscribe met één klik te steunen:

Maak de nieuwe typologieregel:

* Klik in de navigatiestructuur op &quot;nieuw&quot; om een nieuwe typologie te maken

![afbeelding](/help/assets/CreatingTypologyRules1.png){width="50%"}{hight="50%"}

Ga om de typologieregel te vormen te werk:

* Type regel: besturingselement
* Kanaal: e-mail
* Fase: Aan het begin van personalisatie
* Niveau: uw keuze
* Actief

![afbeelding](/help/assets/CreatingTypologyRules2.png)

Code javascript of the Typology rule:

>[!NOTE]
>
>De hieronder beschreven code moet alleen als voorbeeld worden gebruikt.
>In dit voorbeeld wordt beschreven hoe u:
>* Configureer een URL List-Unsubscribe en voeg de kopteksten toe of voeg de bestaande mailto toe: parameters en vervang deze door: &lt;mailto..>, <http://…>
>* Toevoegen in de header List-Unsubscribe-Post
>In het voorbeeld met de post-URL wordt var headerUnsubUrl = &quot;http://campmomentumv7-mkt-prod3.campaign.adobe.com/webApp/unsubNoClick?id=&lt;%= receiving.cryptedId %>&quot; gebruikt:
>* U kunt andere parameters toevoegen (zoals &amp;service = ...)
>


```
// Function to add or replace a header in the provided headers 
function addHeader(headers, header, value)  { 
    
  // Create the new header line 
  var headerLine = header + ": " + value; 
    
  // Create a regular expression to find the specified header 
  var regExp = new RegExp(header + ":(.*)$", "i") 
    
  // Split the headers into individual lines 
  var headerLines = headers.split("\n"); 
    
  // Loop through each line 
  for (var i=0; i < headerLines.length; i++) { 
      
    // Check if the specified header exists 
    var match = headerLines[i].match(regExp) 
      
    // If it exists 
    if ( match != null ) { 
        
      // Replace the existing header line 
      headerLines[i] = headerLine; 
        
      // Return the modified headers 
      return headerLines.join("\n"); 
    } 
  } 
    
  // If the header does not exist, add the new header line 
  headerLines.push(headerLine); 
    
  // Return the modified headers 
  return headerLines.join("\n"); 
} 
  
// Function to get the value of a specified header from the provided headers 
function getHeader(headers, header) { 
    
  // Create a regular expression to find the specified header 
  var regExp = new RegExp(header + ":(.*)$", "i") 
    
  // Split the headers into individual lines 
  var headerLines = headers.split("\n"); 
    
  // Loop each line 
  for each (line in headerLines) { 
      
    // Check if the specified header exists 
    var match = line.match(regExp); 
      
    // If it exists 
    if ( match != null ) { 
        
      // Return the header value, removing leading whitespace 
      return match[1].replace(/^\s*/, ""); 
    } 
  } 
    
  // If the header does not exist, return an empty string 
  return ""; 
} 
  
  
// Define the unsubscribe URL 
var headerUnsubUrl = "http://campmomentumv7-mkt-prod3.campaign.adobe.com/webApp/unsubNoClick?id=<%= recipient.cryptedId %>"; 
  
// Get the value of the List-Unsubscribe header 
var headerUnsub = getHeader(delivery.mailParameters.headers, "List-Unsubscribe"); 
  
// If the List-Unsubscribe header does not exist 
if ( headerUnsub === "" ) { 
  // Add the List-Unsubscribe header 
  delivery.mailParameters.headers = addHeader(delivery.mailParameters.headers, "List-Unsubscribe", "<"+headerUnsubUrl+">"); 
} 
// If the List-Unsubscribe header exists and contains 'mailto' 
else if(headerUnsub.search('mailto')){ 
  // Replace the existing List-Unsubscribe header 
  delivery.mailParameters.headers = addHeader(delivery.mailParameters.headers, "List-Unsubscribe", "<"+headerUnsubUrl+">"); 
} 
  
// Get the value of the List-Unsubscribe-Post header 
var headerUnsubPost = getHeader(delivery.mailParameters.headers, "List-Unsubscribe-Post"); 
  
// If the List-Unsubscribe-Post header does not exist 
if ( headerUnsubPost === "" ) { 
  // Add the List-Unsubscribe-Post header 
  delivery.mailParameters.headers = addHeader(delivery.mailParameters.headers, "List-Unsubscribe-Post", "List-Unsubscribe=One-Click"); 
} 
  
// Return true to indicate success 
return true; 
```

![afbeelding](/help/assets/CreatingTypologyRules3.png)

Voeg uw nieuwe regel aan een Typologie aan een e-mail (Standaard typologie is ok) toe.

![afbeelding](/help/assets/CreatingTypologyRules4.png)

Bereid een nieuwe levering voor (verifieer dat de Extra kopballen SMTP in leveringsbezit leeg is)

![afbeelding](/help/assets/CreatingTypologyRules5.png)

Controleer tijdens de voorbereiding van de levering of de nieuwe typologieregel is toegepast.

![afbeelding](/help/assets/CreatingTypologyRules6.png)

Bevestig dat lijst-unsubscribe aanwezig is.

![afbeelding](/help/assets/CreatingTypologyRules7.png)

## E-mailoptimalisatie {#email-optimization}

### SMTP {#smtp}

SMTP (Simple Mail Transfer Protocol) is een internetstandaard voor e-mailverzending.

De fouten SMTP die niet door een regel worden gecontroleerd zijn vermeld in **[!UICONTROL Administration]** > **[!UICONTROL Campaign Management]** > **[!UICONTROL Non deliverables Management]** > **[!UICONTROL Delivery log qualification]** map. Deze foutberichten worden standaard geïnterpreteerd als onbereikbare schermfouten.

De meest voorkomende fouten moeten worden geïdentificeerd en er moet een corresponderende regel aan worden toegevoegd **[!UICONTROL Administration]** > **[!UICONTROL Campaign Management]** > **[!UICONTROL Non deliverables Management]** > **[!UICONTROL Mail rule sets]** als u wenst om correct te kwalificeren terugkoppelt van de servers SMTP. Zonder deze methode zal het platform onnodige herhalingen (bij onbekende gebruikers) uitvoeren of ten onrechte bepaalde ontvangers in quarantaine plaatsen na een bepaald aantal tests.

### Specifieke IPs {#dedicated-ips}

De Adobe verstrekt een specifieke IP strategie voor elke klant van een oprijplaat-omhoog IP om een reputatie te bouwen en leveringsprestaties te optimaliseren.

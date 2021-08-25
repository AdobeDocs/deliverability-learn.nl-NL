---
title: Campaign Classic - Technische aanbevelingen
description: Ontdek de technieken, configuraties en gereedschappen die u kunt gebruiken om de prestaties met Adobe Campaign Classic te verbeteren.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 39ed3773-18bf-4653-93b6-ffc64546406b
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '1575'
ht-degree: 1%

---

# Campaign Classic - Technische aanbevelingen {#technical-recommendations}

Hieronder vindt u een aantal technieken, configuraties en gereedschappen die u kunt gebruiken om de snelheid van uw producten te verbeteren wanneer u Adobe Campaign Classic gebruikt.

## Configuratie {#configuration}

### DNS omkeren {#reverse-dns}

Adobe Campaign controleert of omgekeerde DNS voor een IP adres wordt gegeven en dat dit correct naar IP wijst.

Een belangrijk punt in de netwerkconfiguratie zorgt ervoor dat correcte omgekeerde DNS voor elk van de IP adressen voor uitgaande berichten wordt bepaald. Dit betekent dat voor een bepaald IP adres, er een omgekeerd DNS verslag (PTR verslag) met een passende DNS (een verslag van A) die terug naar het aanvankelijke IP adres van een lus voorzien is.

De domeinkeus voor omgekeerde DNS heeft een effect wanneer het behandelen van bepaalde ISPs. AOL, in het bijzonder, keurt slechts terugkoppelt lijnen met een adres in het zelfde domein als omgekeerde DNS (zie [Terugkoppelen lijn](#feedback-loop)) goed.

>[!NOTE]
>
>U kunt [dit externe hulpmiddel](https://mxtoolbox.com/SuperTool.aspx) gebruiken om de configuratie van een domein te verifiëren.

### MX-regels {#mx-rules}

MX-regels (Mail eXchanger) zijn de regels die de communicatie tussen een verzendende server en een ontvangende server beheren.

Meer bepaald, worden zij gebruikt om de snelheid te controleren waarbij Adobe Campaign MTA (de Agent van de Overdracht van het Bericht) e-mails naar elk individueel e-maildomein of ISP (bijvoorbeeld, hotmail.com, comcast.net) verzendt. Deze regels zijn typisch gebaseerd op grenzen die door ISPs worden gepubliceerd (bijvoorbeeld, omvatten niet meer dan 20 berichten per elke verbinding SMTP).

>[!NOTE]
>
>Raadpleeg [deze sectie](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/email-deliverability.html#mx-configuration) voor meer informatie over MX-beheer in Adobe Campaign Classic.

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

bepaalt de twee IP adressen, 12.34.56.78 en 12.34.56.79, zoals gemachtigd om e-mails voor het domein te verzenden. **~** betekent altijd dat elk ander adres moet worden geïnterpreteerd als een SoftFail.

Recommendations voor het definiëren van een SPF-record:

* Voeg **~all** (SoftFail) of **-all** (Fail) aan het einde toe om alle andere servers dan de gedefinieerde te weigeren. Zonder dit, zullen de servers dit domein (met een Neutrale evaluatie) kunnen vervalsen.
* Voeg **ptr** niet toe (open spf.org beveelt hiertegen aan als duur en onbetrouwbaar).

>[!NOTE]
>
>Meer informatie over SPF vindt u in [deze sectie](/help/additional-resources/authentication.md#spf).

## Verificatie

>[!NOTE]
>
>Meer informatie over de verschillende vormen van e-mailverificatie vindt u in [deze sectie](/help/additional-resources/authentication.md).

### DKIM {#dkim-acc}

>[!NOTE]
>
>Voor gehoste of hybride installaties, als u aan [Verbeterde MTA](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-emails/sending-an-email/sending-with-enhanced-mta.html#sending-messages) hebt bevorderd, wordt het e-mailauthentificeren DKIM gedaan door Verbeterde MTA voor alle berichten met alle domeinen.

Voor het gebruik van [DKIM](/help/additional-resources/authentication.md#dkim) met Adobe Campaign Classic is de volgende voorwaarde vereist:

**Optiedeclaratie** Adobe Campaign: in Adobe Campaign is de persoonlijke sleutel DKIM gebaseerd op een DKIM-kiezer en een domein. Het is momenteel niet mogelijk om meerdere persoonlijke sleutels voor hetzelfde domein of subdomein te maken met verschillende kiezers. Het is niet mogelijk om te bepalen welk selecteerdomein/subdomein voor de authentificatie in noch het platform noch e-mail moet worden gebruikt. Het platform zal alternatief één van de privé sleutels selecteren, wat betekent de authentificatie een hoge kans heeft om te ontbreken.

* Als u DomainKeys voor uw instantie van Adobe Campaign hebt gevormd, moet u enkel **dkim** in [Regels van het Domeinbeheer ](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html#email-management-rules) selecteren. Indien niet, volg de zelfde configuratiestappen (privé/openbare sleutel) zoals voor DomainKeys (die DKIM verving).
* Het is niet noodzakelijk om zowel DomainKeys als DKIM voor het zelfde domein toe te laten aangezien DKIM een betere versie van DomainKeys is.
* De volgende domeinen valideren momenteel DKIM: AOL, Gmail.

## Feedbacklus {#feedback-loop-acc}

Een feedbacklijn werkt door op het ISP niveau een bepaald e-mailadres voor een waaier van IP adressen te verklaren die voor het verzenden van berichten worden gebruikt. ISP zal naar deze brievenbus, op een gelijkaardige manier verzenden zoals wat voor stuitberichten wordt gedaan, die berichten die door ontvangers als spam worden gemeld. Het platform moet zo worden geconfigureerd dat toekomstige leveringen aan gebruikers die een klacht hebben ingediend, worden geblokkeerd. Het is belangrijk dat zij niet langer contact met hen opnemen, ook al hebben zij niet de juiste opt-out-link gebruikt. Het is gebaseerd op deze klachten dat ISP een IP adres aan zijn lijst van gewezen personen zal toevoegen. Afhankelijk van ISP, zal een klachtentarief van rond 1% in het blokkeren van een IP adres resulteren.

Er wordt momenteel een standaard ontwikkeld voor het definiëren van de indeling van feedbacklusberichten: de [Misbruikrapportage-indeling (ARF)](https://tools.ietf.org/html/rfc6650).

Het implementeren van een feedbacklus voor een instantie vereist:

* Een brievenbus specifiek aan de instantie, die de stuiterende brievenbus kan zijn
* IP die adressen verzendt specifiek aan de instantie

Bij het implementeren van een eenvoudige feedbacklus in Adobe Campaign wordt de functionaliteit voor het stuiterende bericht gebruikt. De terugkoppelt lijnbrievenbus wordt gebruikt als stuiterende brievenbus en een regel wordt bepaald om deze berichten te ontdekken. De e-mailadressen van de ontvangers die het bericht als spam hebben gemeld, worden toegevoegd aan de quarantainelijst.

* Creeer of wijzig een stuiterende postregel, **Feedback_loop**, in **[!UICONTROL Administration > Campaign Management > Non deliverables Management > Mail rule sets]** met de reden **Afgewezen** en het type **Hard**.
* Als een brievenbus speciaal voor de terugkoppel lijn is bepaald, bepaal de parameters om tot het toegang te hebben door een nieuwe externe rekening van de Steekproef te creëren Mails in **[!UICONTROL Administration > Platform > External accounts]**.

Het mechanisme is onmiddellijk operationeel voor het verwerken van kennisgevingen van klachten. Om ervoor te zorgen deze regel correct werkt, kunt u de rekeningen tijdelijk deactiveren zodat zij deze berichten niet verzamelen, dan controleren de inhoud van terugkoppelt lijnbrievenbus manueel. Voer op de server de volgende opdrachten uit:

```
nlserver stop inMail@instance,
nlserver inMail -instance:instance -verbose.
```

Als u gedwongen bent om één enkel te gebruiken terugkoppelt lijnadres voor veelvoudige instanties, moet u:

* Herhaal de ontvangen berichten op zo veel brievenbussen aangezien er instanties zijn,
* Heb elke brievenbus die door één enkele instantie wordt opgepakt,
* Vorm de instanties zodat zij slechts de berichten verwerken die hen aangaan: De instance-informatie is opgenomen in de Message-ID-header van berichten die door Adobe Campaign worden verzonden en bevindt zich daarom ook in de feedbacklusberichten. U geeft gewoon de parameter **checkInstanceName** op in het configuratiebestand van de instantie (de instantie wordt standaard niet geverifieerd en dit kan ertoe leiden dat bepaalde adressen onjuist in quarantined worden geplaatst):

   ```
   <serverConf>
     <inMail checkInstanceName="true"/>
   </serverConf>
   ```

Met de Adobe Campaign Deliverability-service wordt uw abonnement op feedbacklusservices voor de volgende ISP&#39;s beheerd: AOL, BlueTime, Comcast, Cox, EarthLink, FastMail, Gmail, Hotmail, HostedEmail, Libero, Mail.ru, MailTrust, OpenSRS, QQ, RoadRunner, Synacor, Telenor, Terra, UnitedOnline, USA, XS4ALL, Yahoo, Yandex, Zoho.

## List-Unsubscribe {#list-unsubscribe}

### Info over List-Unsubscribe {#about-list-unsubscribe}

Het toevoegen van een kopbal SMTP genoemd **List-Unsubscribe** is verplicht om optimaal leveringsbeheer te verzekeren.

Deze kopbal kan als alternatief aan het &quot;Rapport als SPAM&quot;pictogram worden gebruikt. De koppeling wordt als een koppeling zonder abonnement weergegeven in de e-mailinterface.

Als u deze functie gebruikt, wordt uw reputatie beschermd en wordt feedback uitgevoerd als een abonnement.

Als u List-Unsubscribe wilt gebruiken, moet u een bevellijn gelijkend op als volgt ingaan:

```
List-Unsubscribe: mailto: client@newsletter.example.com?subject=unsubscribe?body=unsubscribe
```

>[!CAUTION]
>
>Het bovenstaande voorbeeld is gebaseerd op de tabel met ontvangers. Als de gegevensbestandimplementatie van een andere lijst wordt gedaan, zorg ervoor om de bevellijn met de correcte informatie te herformuleren.

De volgende bevellijn kan worden gebruikt om tot een dynamisch **List-Unsubscribe** te leiden:

```
List-Unsubscribe: mailto: %=errorAddress%?subject=unsubscribe%=message.mimeMessageId%
```

Gmail, Outlook.com, en Microsoft Outlook steunen deze methode en een unsubscribe knoop is beschikbaar direct in hun interface. Deze techniek verlaagt de klachtenpercentages.

U kunt **List-Unsubscribe** uitvoeren door of:

* Direct [toevoegen van de bevellijn in het leveringsmalplaatje](#adding-a-command-line-in-a-delivery-template)
* [Een typologieregel maken](#creating-a-typology-rule)

### Een opdrachtregel toevoegen in een leveringssjabloon {#adding-a-command-line-in-a-delivery-template}

De bevellijn moet in de extra sectie van de kopbal van SMTP van e-mail worden toegevoegd.

Deze toevoeging kan in elke e-mail, of in bestaande leveringsmalplaatjes worden gedaan. U kunt ook een nieuwe leveringssjabloon maken die deze functionaliteit bevat.

### Een typologieregel maken {#creating-a-typology-rule}

De regel moet het manuscript bevatten dat de bevellijn produceert en het moet in de e-mailkopbal worden omvat.

>[!NOTE]
>
>We raden u aan een typologieregel te maken: De List-Unsubscribe-functionaliteit wordt automatisch toegevoegd aan elke e-mail.

1. List-Unsubscribe: &lt;mailto:unsubscribe@domain.com>

   Als u op de koppeling **unsubscribe** klikt, wordt de standaard e-mailclient van de gebruiker geopend. Deze typologieregel moet worden toegevoegd aan een typologie die wordt gebruikt voor het maken van e-mail.

1. List-Unsubscribe: `<https://domain.com/unsubscribe.jsp>`

   Als u op de koppeling **unsubscribe** klikt, wordt de gebruiker omgeleid naar het formulier voor het niet-abonneren.

   Voorbeeld:

   ![](../assets/s_tn_del_unsubscribe_param.png)

>[!NOTE]
>
>Leer hoe u typologische regels maakt in Adobe Campaign Classic in [deze sectie](https://experienceleague.adobe.com/docs/campaign-classic/using/orchestrating-campaigns/campaign-optimization/about-campaign-typologies.html#typology-rules).

## E-mailoptimalisatie {#email-optimization}

### SMTP {#smtp}

SMTP (Simple Mail Transfer Protocol) is een internetstandaard voor e-mailverzending.

De SMTP fouten die niet door een regel worden gecontroleerd zijn vermeld in **[!UICONTROL Administration]** > **[!UICONTROL Campaign Management]** > **[!UICONTROL Non deliverables Management]** > **[!UICONTROL Delivery log qualification]** omslag. Deze foutberichten worden standaard geïnterpreteerd als onbereikbare schermfouten.

De meest voorkomende fouten moeten worden geïdentificeerd en er moet een corresponderende regel worden toegevoegd in **[!UICONTROL Administration]** > **[!UICONTROL Non deliverables Management]** > **[!UICONTROL Mail rule sets]** als u de feedback van de SMTP-servers correct wilt kwalificeren. **[!UICONTROL Campaign Management]** Zonder deze methode zal het platform onnodige herhalingen (bij onbekende gebruikers) uitvoeren of ten onrechte bepaalde ontvangers in quarantaine plaatsen na een bepaald aantal tests.

### Specifieke IPs {#dedicated-ips}

Adobe verstrekt een specifieke IP strategie voor elke klant van een oprijplaat-omhoog IP om een reputatie te bouwen en leveringsprestaties te optimaliseren.

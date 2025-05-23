---
title: Gmail-merkindicatoren voor berichtidentificatie (BIMI) implementeren
description: Leer hoe u BIMI kunt implementeren
topics: Deliverability
role: Admin
level: Beginner
jira: KT-14079
exl-id: 6b911bcc-a531-466a-8bd3-7fa469b96cc7
source-git-commit: b96539608acd51ce76ef5bdaf5afd07b5a4208b7
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# Implementeren [!DNL Brand Indicators for Message Identification] (BIMI)

[!DNL Brand Indicators for Message Identification] (BIMI) is een industriestandaard waarmee een goedgekeurd logo naast de e-mail van een afzender op deelnemende platforms kan worden weergegeven.

Met deze norm, kan een merk een embleem bepalen dat in postvakjes van brievenbusleveranciers zou moeten worden getoond. Zodra gepubliceerd in een zogenaamd BIMI DNS (het Systeem van de Naam van het Domein) verslag, zou een brievenbusleverancier dit embleem omhoog kunnen halen en het tonen in inbox als bepaalde criteria worden vervuld.

Verschillende aanbieders voeren verschillende implementaties uit, maar de voordelen zijn duidelijk: in de inbox staan, vertrouwen opbouwen en controle hebben over wat wordt getoond.

BIMI verbetert niet rechtstreeks de leverbaarheid of uw reputatie. Het kan helpen meer vertrouwen met uw ontvangers op te bouwen en daardoor ook meer betrokkenheid drijven.

## Hoe ziet het eruit?

U kunt sommige voorbeelden van implementaties van verschillende leveranciers en meer details vinden waarop de leveranciers het embleem op de [ pagina van de Groep BIMI ](https://bimigroup.org/where-is-my-bimi-logo-displayed/){target="_blank"}  tonen.

## Wie is de BIMI-groep?

De BIMI-groep is een werkgroep die BIMI ontwikkelt, aangezien zij niet alleen het logo omvat, maar ook de technische, juridische en nalevingsvereisten.

De BIMI-groep bestaat uit verschillende belanghebbenden uit verschillende sectoren van de industrie: Google, Yahoo, Fastmail, Proofpoint, Mailchimp, Sendgrid, Valimail en Validity.

## Wie steunt BIMI?

De lijst van aanbieders van postvakken die BIMI ondersteunen, wordt gestaag uitgebreid. Een bijgewerkte lijst kan [ hier ](https://bimigroup.org/bimi-infographic/){target="_blank"}  voor zowel steunverleners als leveranciers worden gevonden die BIMI overwegen.

Vanaf april 2023 omvat de lijst Gmail, Yahoo, La Poste, Fastmail, Onet.pl en Zone, Proofpoint als antispamtoestel en Apple Mail (vanaf iOS 16).

De meest prominente namen op die lijst zijn natuurlijk Yahoo, Gmail en een recente adopter: Apple met iOS 16. Apple speelt een speciale rol in de mix, omdat ze geen postvakaanbieder zijn, maar ze hebben wel BIMI-ondersteuning toegevoegd aan hun eigen postapp. Post die voldoet aan BIMI wordt weergegeven als &quot;digitaal gewaarmerkte e-mail&quot; die het vertrouwen in het merk versterkt.

## Implementatie

De implementatie van BIMI gebeurt in verschillende stappen:

1. DMARC (Op domein gebaseerde Authentificatie van het Bericht, het Melden en de Conformiteit) implementatie op handhavingsniveau voor zowel het verzendende domein als zijn organisatorisch domein - [ leer meer ](#dmarc)

1. Creatie van uw merkembleem in het formaat van SVG TinyPS - [ leer meer ](#create-brand-logo)

1. Ondertekenend omhoog voor een Geverifieerd Certificaat van het Teken (slechts nodig voor sommige leveranciers) - [ leer meer ](#vmc)

1. Publish a BIMI DNS verslag met het embleem en het certificaat - [ Leer meer ](#publish-bimi-record)

1. Het hebben van een goede reputatie - [ leer meer ](#good-reputation)

>[!NOTE]
>
>Alle stappen moeten worden uitgeschakeld.


### DMARC {#dmarc}

DMARC is een norm die het merk toestaat om te beslissen wat een brievenbusleverancier met e-mail zou moeten doen die [ authentificatie ](../additional-resources/authentication.md) ontbreekt. Het zogenaamde beleid varieert van &quot;niets&quot;over &quot;quarantaine&quot; (de omslagplaatsing van Spam) aan &quot;verwerpen&quot; (direct blok de post). Alleen de laatste twee beleidsvormen worden &quot;handhaving&quot; genoemd en komen in aanmerking voor BIMI. De post die door Adobe wordt verzonden gaat authentificatie over, aangezien SPF (het Kader van het Beleid van de Afzender) en DKIM (de Sleutels van het Domein Identified Mail) opstelling per gebrek zijn. Adobe stelt DMARC op uw verzendend domein op verzoek in.

Naast DMARC op het verzendende domein, moet DMARC ook op handhavingsniveau voor het organisatorische domein worden gebruikt (als het verzendende domein news.example.com is, example.com is het organisatorische domein).

### Het logo van uw merk maken {#create-brand-logo}

Het maken van het logo moet aan de vereisten voldoen tot 100%. Gelieve te verwijzen altijd naar de [ richtlijnen van de Groep BIMI ](https://bimigroup.org/creating-bimi-svg-logo-files/){target="_blank"} .

Het logo moet op een beveiligde locatie (HTTPS) worden opgeslagen, voor het geval dat een CDN (content delivery network) wordt gebruikt om het even welke bescherming te voorkomen die postbusproviders ervan weerhoudt het logo te verkrijgen (bv. Bot Protection), moet worden uitgeschakeld.

Naast de technische vereisten zijn er enkele praktische aanbevelingen, zoals een vierkant logo, een effen kleur als achtergrond en andere. Deze aanbevelingen zijn bedoeld voor een optimale visualisatie. Sommige aanbieders hebben hun eigen vereisten die een aanvulling vormen op die van de BIMI-werkgroep. [ Gmail ](https://support.google.com/a/answer/10911027?sjid=903725605955621707-EU){target="_blank"}  bijvoorbeeld vereist het embleem om minstens 96 x 96 pixel te zijn.
Niet-naleving kan ertoe leiden dat het logo niet wordt weergegeven.

### Verified Mark Certificate (VMC) {#vmc}

Een gecontroleerd Certificaat van het Teken (VMC) is slechts nodig voor sommige brievenbusleveranciers zoals Gmail en Apple, en daarom is facultatief. We raden echter wel aan een VMC te krijgen om BIMI echt te benutten.

Een geverifieerd markeringscertificaat is een geldige validering waarmee het merk het logo kan gebruiken. Een certificeringsinstantie zal dit controleren via het merkenbureau waar het merklogo is geregistreerd. Dit proces omvat verschillende wettelijke validaties en controles en kan enige tijd in beslag nemen. Momenteel geven twee CA&#39;s (certificeringsinstanties) VMC&#39;s uit: Digicert en Entrust. De eerste reeks merkenkantoren zijn VS, Canada, EU, Verenigd Koninkrijk, Duitsland, Japan, Australië en Spanje.

Als algemene regel hebt u één VMC per logo nodig. Het hebben van VMC voor uw organisatorisch domein zal subdomeinen, en met een toegevoegde eigenschap zelfs verschillende domeinen behandelen. Als u verschillende logo&#39;s hebt, hebt u meer dan één VMC nodig. De certificeringsinstantie of -partner waarmee u wilt werken, helpt u bij het instellen van deze functie.

>[!NOTE]
>
>VMC&#39;s hebben een jaarlijkse vergoeding.

### Publicatie van het BIMI-bestand {#publish-bimi-record}

Zodra de andere stappen zijn uitgevoerd, kan het BIMI DNS-record worden gepubliceerd. De record ziet er als volgt uit:

```
default._bimi.[domain] IN TXT "v=BIMI1; l=[SVG URL]; a=[PEM URL]
```

&quot;PEM URL&quot; is de bestandslocatie van het geverifieerde Mark Certificate.

Voor uw verzendend domein, moet dit door Adobe worden gedaan.

### Goede reputatie {#good-reputation}

Vertrouwen is de sleutel voor BIMI. De gebruiker vertrouwt op hun brievenbusleverancier om het embleem voor wettige afzenders slechts te tonen, zodat moet de brievenbusleverancier het merk vertrouwen, en dit wordt gedaan door uw afzenderreputatie. Als je een goede reputatie hebt, is alles goed, maar als je dat niet bent, wordt het logo niet weergegeven. Jammer genoeg, is er geen informatie of metrisch wij kunnen bekijken om te weten te komen als de reputatie hoog genoeg is.

Zelfs als je de moeite en kosten voor VMC doorloopt, wordt dit onderdeel niet verwijderd. Als de brievenbusleverancier niet het merk vertrouwt, zal het embleem niet worden getoond.

## Tips en trucs

* De BIMI-groep biedt een handig valideringsinstrument voor BIMI. Als u wilt controleren als alles opstelling en klaar is, of enkel willen zien of is het embleem volgzaam, ga [ deze verbinding ](https://bimigroup.org/bimi-generator/){target="_blank"} . Voor de laatste klikt u gewoon op **[!UICONTROL Generate BIMI]** en voert u een plaatsaanduidingsdomein in, maar wel de juiste URL voor het logo. De inspecteur zal u vertellen als het embleem volgzaam is.

* U kunt veilig zonder VMC beginnen, is er geen schade op uw reputatie als uw BIMI-verslag geen VMC URL omvat, maar het embleem kan reeds in Yahoo worden getoond.

* De organisatorische implementatie van DMARC is een grote onderneming. Sommige bedrijven zijn gespecialiseerd om merken te helpen een volledige goedkeuring DMARC bereiken.

* Een uitgebreide lijst van vaak gestelde vragen wordt gepubliceerd [ hier ](https://bimigroup.org/faqs-for-senders-esps/){target="_blank"} .

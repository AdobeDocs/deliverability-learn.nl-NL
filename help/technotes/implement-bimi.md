---
title: Gmail-merkindicatoren voor berichtidentificatie (BIMI) implementeren
description: Leer hoe u BIMI kunt implementeren
topics: Deliverability
exl-id: 6b911bcc-a531-466a-8bd3-7fa469b96cc7
source-git-commit: aca2bfff9f0315b735cf0a97f2177083c58e0875
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# Implementeren [!DNL Brand Indicators for Message Identification] (BIMI)

[!DNL Brand Indicators for Message Identification] (BIMI) is een industriestandaard waarmee een goedgekeurd logo naast de e-mail van een afzender op deelnemende platforms kan worden weergegeven.

Met deze norm, kan een merk een embleem bepalen dat in postvakjes van brievenbusleveranciers zou moeten worden getoond. Zodra gepubliceerd in een zogenaamd BIMI DNS (het Systeem van de Naam van het Domein) verslag, zou een brievenbusleverancier dit embleem omhoog kunnen halen en het tonen in inbox als bepaalde criteria worden vervuld.

Verschillende providers voeren verschillende implementaties uit, maar de voordelen zijn duidelijk: in de inbox staan , vertrouwen opbouwen en controleren wat er wordt getoond .

BIMI verbetert niet rechtstreeks de leverbaarheid of uw reputatie. Het kan helpen meer vertrouwen met uw ontvangers op te bouwen en daardoor ook meer betrokkenheid drijven.

## Hoe ziet het eruit?

U vindt enkele voorbeelden van implementaties van verschillende providers en meer informatie over welke providers het logo op het tabblad [Pagina van de BIMI-groep](https://bimigroup.org/where-is-my-bimi-logo-displayed/){target="_blank"}.

## Wie is de BIMI-groep?

De BIMI-groep is een werkgroep die BIMI ontwikkelt, aangezien zij niet alleen het logo omvat, maar ook de technische, juridische en nalevingsvereisten.

De BIMI-groep bestaat uit verschillende belanghebbenden uit verschillende sectoren van de sector: Google, Yahoo, Fastmail, Proofpoint, Mailchimp, Sendgrid, Valimail en Validity.

## Wie steunt BIMI?

De lijst van aanbieders van postvakken die BIMI ondersteunen, wordt gestaag uitgebreid. Een bijgewerkte lijst is te vinden [hier](https://bimigroup.org/bimi-infographic/){target="_blank"} voor zowel ondersteunende aanbieders als aanbieders die BIMI overwegen.

Vanaf april 2023 omvat de lijst Gmail, Yahoo, La Poste, Fastmail, Onet.pl en Zone, Proofpoint als antispamtoestel en Apple Mail (vanaf iOS 16).

De meest prominente namen op die lijst zijn natuurlijk Yahoo, Gmail en een recente adopter: Apple met iOS 16. Apple speelt een speciale rol in de mix, omdat ze geen postvakaanbieder zijn, maar ze hebben wel BIMI-ondersteuning toegevoegd aan hun eigen postapp. Post die voldoet aan BIMI wordt weergegeven als &quot;digitaal gewaarmerkte e-mail&quot; die het vertrouwen in het merk versterkt.

## Implementatie

De implementatie van BIMI gebeurt in verschillende stappen:

1. DMARC (Domain based Message Authentication, Reporting and Conformance)-implementatie op handhavingsniveau voor zowel het verzendende domein als zijn organisatiedomein - [Meer informatie](#dmarc)

1. Maak uw merklogo in de SVG TinyPS-indeling - [Meer informatie](#create-brand-logo)

1. Aanmelden voor een geverifieerd Mark Certificate (alleen nodig voor bepaalde providers) - [Meer informatie](#vmc)

1. Publiceer een BIMI DNS-record met het logo en het certificaat - [Meer informatie](#publish-bimi-record)

1. Een goede reputatie - [Meer informatie](#good-reputation)

>[!NOTE]
>
>Alle stappen moeten worden uitgeschakeld.


### DMARC {#dmarc}

DMARC is een norm die het merk toestaat om te beslissen wat een brievenbusleverancier met een e-mail zou moeten doen die ontbreekt [verificatie](../additional-resources/authentication.md). Het zogenaamde beleid varieert van &quot;niets&quot;over &quot;quarantaine&quot; (de omslagplaatsing van Spam) aan &quot;verwerpen&quot; (direct blok de post). Alleen de laatste twee beleidsvormen worden &quot;handhaving&quot; genoemd en komen in aanmerking voor BIMI. De post die door Adobe wordt verzonden gaat authentificatie over, aangezien SPF (het Kader van het Beleid van de Afzender) en DKIM (de Sleutels van het Domein Identified Mail) opstelling per gebrek zijn. Adobe stelt DMARC op uw verzendend domein op verzoek in.

Naast DMARC op het verzendende domein, moet DMARC ook op handhavingsniveau voor het organisatorische domein worden gebruikt (als het verzendende domein nieuws.example.com is, example.com is het organisatorische domein).

### Het logo van uw merk maken {#create-brand-logo}

Het maken van het logo moet aan de vereisten voldoen tot 100%. Raadpleeg altijd de [Richtsnoeren van de BIMI-groep](https://bimigroup.org/creating-bimi-svg-logo-files/){target="_blank"}.

Naast de technische vereisten zijn er enkele praktische aanbevelingen, zoals een vierkant logo, een effen kleur als achtergrond en andere. Deze aanbevelingen zijn bedoeld voor een optimale visualisatie.
Niet-naleving kan ertoe leiden dat het logo niet wordt weergegeven.

### Verified Mark Certificate (VMC) {#vmc}

Een gecontroleerd Certificaat van het Teken (VMC) is slechts nodig voor sommige brievenbusleveranciers zoals Gmail en Apple, en daarom is facultatief. We raden echter wel aan een VMC te krijgen om BIMI echt te benutten.

Een geverifieerd markeringscertificaat is een geldige validering waarmee het merk het logo kan gebruiken. Een certificeringsinstantie zal dit controleren via het merkenbureau waar het merklogo is geregistreerd. Dit proces omvat verschillende wettelijke validaties en controles en kan enige tijd in beslag nemen. Momenteel geven twee CA&#39;s (certificeringsinstanties) VMC&#39;s uit: Digicert en Entrust. De eerste reeks merkenkantoren zijn VS, Canada, EU, Verenigd Koninkrijk, Duitsland, Japan, Australië en Spanje.

Als algemene regel hebt u één VMC per logo nodig. Het hebben van VMC voor uw organisatorisch domein zal subdomeinen, en met een toegevoegde eigenschap zelfs verschillende domeinen behandelen. Als u verschillende logo&#39;s hebt, hebt u meer dan één VMC nodig. De certificeringsinstantie of -partner waarmee u wilt werken, helpt u dit instellen.

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

* De BIMI-groep biedt een handig valideringsinstrument voor BIMI. Als u wilt controleren of alles is ingesteld en klaar, of alleen wilt controleren of het logo voldoet, gaat u naar [deze koppeling](https://bimigroup.org/bimi-generator/){target="_blank"}. Voor de laatste klikt u op **[!UICONTROL Generate BIMI]** en voert u een plaatsaanduidingsdomein in, maar de juiste URL van het logo. De inspecteur zal u vertellen als het embleem volgzaam is.

* U kunt veilig zonder VMC beginnen, is er geen schade op uw reputatie als uw BIMI-verslag geen VMC URL omvat, maar het embleem kan reeds in Yahoo worden getoond.

* De organisatorische implementatie van DMARC is een grote onderneming. Sommige bedrijven zijn gespecialiseerd om merken te helpen een volledige goedkeuring DMARC bereiken.

* Een uitgebreide lijst met veelgestelde vragen wordt gepubliceerd [hier](https://bimigroup.org/faqs-for-senders-esps/){target="_blank"}.

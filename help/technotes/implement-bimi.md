---
title: Gmail-merkindicatoren voor berichtidentificatie (BIMI) implementeren
description: Leer hoe u BIMI kunt implementeren
topics: Deliverability
exl-id: 6b911bcc-a531-466a-8bd3-7fa469b96cc7
source-git-commit: 683ffd3c87a4849aa9fa48fbf50db9ade97991af
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Gmail&#39;s implementeren [!DNL Brand Indicators for Message Identification] (BIMI)

Gmail kondigde onlangs aan dat zij [algemene ondersteuning van BIMI](https://cloud.google.com/blog/products/identity-security/bringing-bimi-to-gmail-in-google-workspace){target=&quot;_blank&quot;}. Er zijn een aantal punten u zult moeten behandelen alvorens u uit dit kunt voordeel halen hoewel het omvatten: Gecontroleerde Mark Certificates, Trademarked Logos, correct opgemaakte Logo&#39;s, DMARC-instelling en ten slotte het publiceren van een BIMI-record naar uw DNS. We zullen al deze stappen in dit artikel bekijken.

[!DNL Brand Indicators for Message Identification] (BIMI) is een industriestandaard waarmee een goedgekeurd logo naast de e-mail van een afzender op deelnemende platforms kan worden weergegeven. Niet alleen is deze opvallende betrokkenheid mogelijk versterkt, het helpt ook de authenticiteit van de verzender te bevestigen en het risico van phishing en andere spammtactiek te verminderen.

## Certificaat van geverifieerde markering

Een van de belangrijkste onderdelen van het BIMI-programma van Gmail is de eis dat afzenders een VMC (Verified Mark Certificate) hebben dat is afgegeven door een geldige certificeringsinstantie. Momenteel zijn deze VMCs beschikbaar slechts bij Entrust en DigiCert, maar die lijst van leveranciers zal waarschijnlijk na de aankondiging van Gmail groeien.

VMCs zal aan SSL certificaten op sommige manieren gelijkaardig zijn. U zult één VMC voor elk embleem nodig hebben u wilt getoond, zodat als u veel merken hebt u op het nodig hebben van veelvoudige VMCs zou moeten plannen. Elke VMC kan geldig zijn over meerdere domeinen hoewel als u een VMC van Multi-SAN krijgt. Dus als u één logo op meerdere verzendende domeinen wilt weergeven, hebt u slechts één VMC nodig.

## Logohandelsmerk

Voordat u uw VMC kunt ophalen, moet u een andere belangrijke stap uitvoeren. Als u een VMC wilt ophalen, moet het logo dat u wilt weergeven, zijn geregistreerd bij een van de acht goedgekeurde wereldwijde handelsmerken en octrooibureaus.

* United States Patent and Trademark Office (USPTO)
* Canadian Intellectual Property Office
* Bureau voor intellectuele eigendom van de Europese Unie
* Britse dienst voor intellectuele eigendom
* Deutsches Patent- und Markenamt
* Japan Trademark Office
* Spaans Octrooi- en Handelsmerk Office o.a.
* IP Australia

Als het logo dat u wilt weergeven niet is geregistreerd of niet bij een van deze 8 organisaties is geregistreerd, moet u met uw juridische team samenwerken om dat te verhelpen voordat u een aanvraag voor VMC indient.

## Afbeeldingsindeling logo

Dit zou ook een goed moment zijn om ervoor te zorgen dat uw logo voldoet aan de vereisten voor het formaat van het BIMI-logo.

De notatie moet de SVG-indeling hebben en moet voldoen aan het profiel SVG Portable/Secure (SVG-P/S). Zie voor meer informatie over hoe u dit kunt doen de [BIMI-werkgroep](https://bimigroup.org/svg-conversion-tools-released){target=&quot;_blank&quot;}.

## DMARC

Zodra u hebt uw Vertaald Logo behoorlijk geformatteerd, en uw Geverifieerd Certificaat van het Merk, zult u ook moeten ervoor zorgen dat DMARC volledig op om het even welk verzendend domein wordt gevormd u BIMI wilt werken voor.

Dit omvat het ervoor zorgen P= aan of Quarantine of Weigeren wordt geplaatst. Als uw DMARC P=None gebruikt, komt deze niet in aanmerking voor BIMI. P=None het plaatsen wordt hoogst geadviseerd om u te verzekeren welke post uit een domein gaat en dat niets per ongeluk zou worden geblokkeerd als u of &quot;Quarantine&quot;of &quot;Afwijzen&quot;veranderde, denk het als het testen en informatie verzamelen fase. U moet verder gaan dan dat, maar voordat BIMI voor u beschikbaar wordt.

## DNS-vermelding

Met al het andere eindelijk in orde en klaar om te gaan, is het tijd om de DNS ingang met uw BIMI bij te werken.

Dit is een eenvoudige vermelding die er ongeveer als volgt uitziet:

```
default._bimi.[domain] IN TXT “v=BIMI1; l=[SVG URL] 
```

U kunt de details rond die ingang krijgen en zelfs een vrije controle BIMI gebruiken bij [Website van de werkgroep IMI](https://bimigroup.org/implementation-guide){target=&quot;_blank&quot;}.


## Key Takeaways

Als u een [!DNL Adobe Campaign], kan Adobe u helpen bij het maken van de BIMI DNS-update: Neem contact op met de klantenservice van Adobe om een aanvraag in te dienen. Adobe kan ook helpen bij het oplossen van problemen als BIMI niet correct voor u werkt.

Als u een Marketo-client bent, raadpleegt u [dit blogbericht](https://nation.marketo.com/t5/support-blogs/how-to-bimi/ba-p/296966){target=&quot;_blank&quot;} voor aanwijzingen bij het maken van uw BIMI-record.

Voor hulp met handelsmerken of Geverifieerde Certificaten van het Merk, werk met uw wettelijk team en een erkende verkoper VMC.

Het ophalen van de BIMI-instelling voor Gmail is wellicht geen snel proces, maar het is wel een proces dat aanzienlijke voordelen kan hebben vanuit het oogpunt van marketing en beveiliging.

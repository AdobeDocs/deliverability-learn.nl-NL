---
title: Gmail-merkindicatoren voor berichtidentificatie (BIMI) implementeren
description: Leer hoe u BIMI kunt implementeren
topics: Deliverability
role: Admin
level: Beginner
exl-id: f1c14b10-6191-4202-9825-23f948714f1e
source-git-commit: 2a78db97a46150237629eef32086919cacf4998c
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 8%

---

# Implementeren [!DNL Domain-based Message Authentication, Reporting and Conformance] (DMARC)

Het doel van dit document is om de lezer meer informatie te verschaffen over de methode voor e-mailverificatie, DMARC. Door uit te leggen hoe DMARC werkt en welke beleidsopties DMARC heeft, zullen lezers de invloed van DMARC op E-mailleverbaarheid beter begrijpen.

## Wat is DMARC? {#about}

De op domein-gebaseerde Authentificatie van het Bericht, Rapportering en Conformiteit, is een methode van de e-mailauthentificatie die domeineigenaars de capaciteit toestaat om hun domein tegen onbevoegd gebruik te beschermen. DMARC biedt ook feedback over de status van e-mailverificatie en biedt afzenders de mogelijkheid om te bepalen wat er gebeurt met e-mails waarvoor verificatie mislukt. Dit omvat opties om post te controleren, in quarantaine te plaatsen of te verwerpen afhankelijk van welk beleid DMARC is uitgevoerd.

DMARC heeft drie beleidsopties:

* **Monitor (p=none):** draagt de brievenbusleverancier/ISP op om te doen wat zij normaal aan het bericht zouden doen.
* **Quarantine (p=quarantaine):** draagt de brievenbusleverancier/ISP op om post te leveren die geen DMARC tot spam of junk omslag van de ontvanger overgaat.
* **Weigeren (p=verwerping):** draagt de brievenbusleverancier/ISP op om post te blokkeren die DMARC niet overgaat resulterend in een stuit.

## Hoe werkt DMARC? {#how}

SPF en DKIM worden allebei gebruikt om een e-mail met een domein te associëren en samen te werken om e-mail voor authentiek te verklaren. DMARC neemt deze één stap verder en helpt spoofing te verhinderen door het Domein aan te passen dat door DKIM en SPF wordt gecontroleerd. Om DMARC over te gaan, moet een bericht SPF of DKIM overgaan. Als deze beide niet worden geverifieerd, mislukt DMARC en wordt het e-mailbericht verzonden volgens het geselecteerde DMARC-beleid.

>[!NOTE]
>
>DMARC vereist groepering tussen het &quot;van&quot;en &quot;terugkeer-Weg&quot;adres.

## Waarom moet DMARC worden geïmplementeerd? {#why}

DMARC is optioneel, en hoewel dit niet verplicht is, is het gratis en biedt e-mailontvangers de mogelijkheid om de verificatie van e-mails gemakkelijk te identificeren, wat de levering mogelijk kan verbeteren. Een van de belangrijkste voordelen van DMARC is dat het rapportering aanbiedt over welke berichten SPF en/of DKIM ontbreken. Het geeft afzenders ook een graad van controle over wat met post gebeurt die één van beiden van deze authentificatiemethodes niet overgaat. Via DMARC-rapporten krijgen afzenders meer inzicht in welke berichten DMARC niet behalen, waardoor stappen kunnen worden ondernomen om verdere fouten te beperken.

>[!NOTE]
>
>Als u BIMI wilt implementeren, is een p=quarantaine- of p=afwijzend DMARC-beleid vereist.

## Beste praktijken voor het Uitvoeren DMARC {#best-practice}

Aangezien DMARC facultatief is, zal het niet door gebrek op om het even welk platform van ESP worden gevormd. Een DMARC- verslag moet in DNS voor uw domein worden gecreeerd opdat het werkt. Bovendien is een e-mailadres van uw keuze vereist om aan te geven waar DMARC-rapporten binnen uw organisatie moeten worden geplaatst. Als beste praktijk is het
Aanbevolen wordt om de implementatie DMARC langzaam uit te voeren door uw beleid DMARC van p=none, aan p=quarantaine, aan p=weiger te escaleren aangezien u DMARC inzicht van de potentiële invloed van DMARC krijgt.

1. Analyseer terugkoppelen u ontvangt en gebruikt (p=none), die de ontvanger vertelt om geen acties tegen berichten uit te voeren die authentificatie ontbreken, maar nog e-mailrapporten naar de afzender verzenden. Bekijk en los ook problemen met SPF/DKIM op als legitieme berichten niet kunnen worden geverifieerd.
1. Bepaal als SPF en DKIM worden gericht en authentificatie voor al wettige e-mail overgaan, en dan het beleid verplaatsen naar (p=quarantaine), dat de ontvangende e-mailserver aan quarantainemail vertelt die authentificatie ontbreekt (dit betekent over het algemeen het plaatsen van die berichten in de spamomslag).
1. Pas het beleid aan (p=afwijzen). Het beleid p=reject laat de ontvanger weten dat elke e-mail voor het domein dat niet door de verificatie komt, moet worden geweigerd (teruggestuurd). Als dit beleid is ingeschakeld, heeft alleen e-mail voor 100% is geverifieerd door uw domein, een kans op plaatsing in het postvak IN.

   >[!NOTE]
   >
   >Gebruik dit beleid voorzichtig en bepaal of het geschikt is voor uw organisatie.

## DMARC-rapportage {#reporting}

DMARC biedt de mogelijkheid om rapporten te ontvangen over e-mailberichten die niet voldoen aan SPF/DKIM. Er zijn twee verschillende rapporten die door ISP diensten als deel van het authentificatieproces worden geproduceerd dat de afzenders door de markeringen RUA/RUF in hun beleid kunnen ontvangen DMARC:

* **Samengevoegde Rapporten (RUA):** bevat geen PII (Persoonlijk Identificeerbare Informatie) die GDPR gevoelig zou zijn.
* **Forensische Rapporten (RUF):** bevat e-mailadressen die gevoelig GDPR zijn. Alvorens te gebruiken, is het best om intern te controleren hoe te om te gaan met informatie die GDPR volgzaam moet zijn.

Deze rapporten worden vooral gebruikt om een overzicht te krijgen van e-mails die spoofing proberen te maken. Dit zijn hoogst technische rapporten die het best door een derdehulpmiddel worden verteerd. Enkele bedrijven die gespecialiseerd zijn in DMARC-monitoring zijn:

* [ ValiMail ](https://www.valimail.com/products/#automated-delivery)
* [ Agari ](https://www.agari.com/)
* [ Dmarcier ](https://dmarcian.com/)
* [ Proofpoint ](https://www.proofpoint.com/us)

>[!CAUTION]
>
>Als de e-mailadressen die u toevoegt om rapporten te ontvangen, zich buiten het domein bevinden waarvoor de DMARC- record is gemaakt, moet u hun externe domein machtigen om bij de DNS op te geven dat u de eigenaar van dit domein bent. Voer hiervoor de stappen uit die worden beschreven in de [documentatie van dmarc.org](https://dmarc.org/2015/08/receiving-dmarc-reports-outside-your-domain)

### Voorbeeld-DMARC-record {#example}

```
v=DMARC1; p=reject; fo=1; rua=mailto:dmarc_rua@emaildefense.proofpoint.com;ruf=mailto:dmarc_ruf@emaildefense.proofpoint.co
```

## DMARC-tags en wat ze doen {#tags}

DMARC-records hebben meerdere componenten, DMARC-tags genoemd. Elke tag heeft een waarde die een bepaald aspect van DMARC opgeeft.

| Tagnaam | Vereist/optioneel | Functie | Voorbeeld | Standaardwaarde |
|  ---  |  ---  |  ---  |  ---  |  ---  |
| v | Vereist | Met deze DMARC-tag wordt de versie opgegeven. Er is momenteel slechts één versie, dus deze heeft een vaste waarde van v=DMARC1 | V=DMARC1 DMARC1 | DMARC1 |
| p | Vereist | Toont het geselecteerde beleid DMARC en geeft de ontvanger opdracht om post te melden, in quarantaine te plaatsen of te verwerpen die authentificatiecontroles ontbreekt. | p=none, quarantaine of afwijzen | - |
| fo | Optioneel | Staat de domeineigenaar toe om rapporteringsopties te specificeren. | 0: Genereer rapport als alles ontbreekt <br/> 1: Genereer rapport als om het even wat ontbreekt <br/> d: produceer rapport als DKIM ontbreekt <br/> het rapport als SPF ontbreekt | 1 (aanbevolen voor DMARC-rapporten) |
| pct | Optioneel | Vertelt het percentage berichten die aan het filtreren worden onderworpen. | pct=20 | 100 |
| ruw | Optioneel (aanbevolen) | Identificeert waar de samengevoegde rapporten zullen worden geleverd. | `rua=mailto:aggrep@example.com` | - |
| ruf | Optioneel (aanbevolen) | Identificeert waar forensische rapporten zullen worden geleverd. | `ruf=mailto:authfail@example.com` | - |
| sp | Optioneel | Specificeert beleid DMARC voor subdomeinen van het ouderdomein. | sp=deny | - |
| adkim | Optioneel | Kan strikt (s) of Ontspannen (r) zijn. Relaxed alignment betekent dat het domein dat wordt gebruikt in de DKIM-handtekening een subdomein kan zijn van het adres &#39;Van&#39;. Strikte uitlijning betekent dat het domein dat wordt gebruikt in de DKIM-handtekening een exacte overeenkomst moet zijn met het domein dat wordt gebruikt in het adres &#39;from&#39;. | adkim=r | r |
| aspf | Optioneel | Kan strikt (s) of Ontspannen (r) zijn. De opnieuw geconcentreerde groepering betekent dat het Domein ReturnPath een subdomein van Van Adres kan zijn. Strikte uitlijning houdt in dat het domein van het Return-Path een exacte overeenkomst moet zijn met het Van-adres. | aspf=r | r |

## DMARC en Adobe Campaign {#campaign}

>[!NOTE]
>
>Als uw instantie Campagne op AWS wordt ontvangen, kunt u DMARC voor uw subdomeinen met het Controlebord uitvoeren. [ Leer hoe te om Verslagen uit te voeren DMARC gebruikend Controlebord ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/txt-records/dmarc.html).

Een algemene reden voor DMARC-fouten is een onjuiste afstemming tussen het adres &#39;Van&#39; en &#39;Fouten naar&#39; of &#39;Return-Path&#39;. Om dit te voorkomen, wordt het aanbevolen om bij het instellen van DMARC de instellingen voor het adres &#39;Van&#39; en &#39;Fouten-naar&#39; in uw leveringssjablonen tweemaal te controleren.

1. Controleer in uw leveringssjabloon welk adres momenteel is ingesteld als het adres Van.

   ![](../assets/dmarc1.png)

1. Van hier, uitgezochte &quot;Eigenschappen&quot;die u zal toestaan om uw leveringsmalplaatje verder uit te geven. Selecteer in dit venster de optie SMTP en schakel de optie &quot;Het standaardfoutadres gebruiken dat voor het platform is gedefinieerd&quot; uit als deze optie is geselecteerd. Leveringssjablonen in Adobe Campaign selecteren dit selectievakje standaard. Het standaardadres van de Fout kan niet het adres verbonden aan Van Adres in dit leveringsmalplaatje zijn.

   ![](../assets/dmarc2.png)

1. Wanneer dit vakje niet wordt gecontroleerd, verschijnt een tekstgebied dat u zal toestaan om een uniek Adres van de Fout in te gaan dat het zelfde domein gebruikt zoals die in Van Adres wordt geplaatst.

   ![](../assets/dmarc3.png)

Zodra deze veranderingen worden bewaard, zult u met uw implementatie DMARC met correcte domeingroepering kunnen vooruit gaan.

## Nuttige koppelingen {#links}

* [ DMARC.org ](https://dmarc.org/) {target="_blank"}
* [ M3AWG e-mailAuthentificatie ](https://www.m3aawg.org/sites/default/files/document/M3AAWG_Email_Authentication_Update-2015.pdf) {target="_blank"}

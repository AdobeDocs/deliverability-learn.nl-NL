---
title: Richtsnoeren voor de aangekondigde wijzigingen [!DNL Google] en [!DNL Yahoo]
description: Richtsnoeren voor de aangekondigde wijzigingen [!DNL Google] en [!DNL Yahoo]
role: Admin
level: Experienced
doc-type: Article
last-substantial-update: 2023-11-06T00:00:00Z
jira: KT-14320
thumbnail: KT-14320.jpeg
source-git-commit: 0aeff034f6ca2a3dce065240384d1b0e7922fa31
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 0%

---


# Richtsnoeren voor de aangekondigde wijzigingen [!DNL Google] en [!DNL Yahoo]

Op 3 oktober beide [!DNL Google] en [!DNL Yahoo] gezamenlijk via hun blogs aangekondigde wijzigingen . Deze wijzigingen zijn bedoeld om hun gebruikers veiliger te houden en een betere e-mailervaring te bieden door een aantal gangbare best practices uit de branche te handhaven als nieuwe vereisten vanaf februari 2024.

[https://blog.google/products/gmail/gmail-security-authentication-spam-protection/](https://blog.google/products/gmail/gmail-security-authentication-spam-protection/){target="_blank"}

![[!DNL Google] Aankondiging](/help/assets/Gmail.png)

[https://blog.postmaster.yahooinc.com/post/730172167494483968/more-secure-less-spam](https://blog.postmaster.yahooinc.com/post/730172167494483968/more-secure-less-spam){target="_blank"}

![[!DNL Yahoo] Aankondiging](/help/assets/Yahoo.png)

De experts op het gebied van e-maillevering in Adobe hebben deze blogberichten en alle bijbehorende documentatie gelezen, zodat u ze niet hoeft te lezen. Hier zijn de belangrijkste reisroutes.

## Dus wat precies zijn [!DNL Google] en [!DNL Yahoo] doen?

In de wereld van e-mail zijn er wettelijke vereisten, praktische vereisten, en algemene beste praktijken. De wettelijke vereisten variëren sterk van plaats aan plaats en zijn geen deel van dit onderwerp. In plaats daarvan, [!DNL Google] en [!DNL Yahoo] best practices gebruiken en omzetten in praktische vereisten. Geen items [!DNL Google] en [!DNL Yahoo] In februari zullen nieuwe eisen worden gesteld, die al jaren vaak aanbevelingen voor beste praktijken zijn, maar in de sector is de adoptie traag en ongelijk verlopen. Dit is [!DNL Google] en [!DNL Yahoo]Wij helpen dat adoptieproces te bevorderen door te zeggen: &quot;Als u e-mail aan onze gebruikers wilt opstellen (dit kan een belangrijk deel van uw e-maillijst, in sommige gevallen zelfs tot 70%, afhankelijk van regio en industrie vertegenwoordigen) moet u deze dingen doen.&quot;

## Wat zijn de details?

Als u een klant van de Adobe bent is het grootste deel van wat zij vereisen reeds een deel van uw opstelling, maar er zijn een paar zeer belangrijke punten die technisch facultatief zijn, en u zult zeker willen zijn uw organisatie heeft goedgekeurd en deze punten correct vóór Februari 2024 geïnstalleerd.

## DMARC:

[!DNL Google] en [!DNL Yahoo] vereisen beide dat u een DMARC-record hebt voor elk domein dat u gebruikt om e-mail naar hen te verzenden. Op dit moment hebben ze GEEN p=weiger- of p=quarantaine-instelling nodig. Een instelling van p=none, doorgaans de instelling &quot;Bewaking&quot; genoemd, is dus volkomen acceptabel. Dit zal niet veranderen hoe uw e-mails worden verwerkt, zij zullen doen wat zij normaal zonder DMARC zouden doen. Het instellen van deze instelling is de eerste stap om uzelf te beschermen met DMARC en het nieuwe voordeel om u te helpen e-mail te sturen naar [!DNL Google] en [!DNL Yahoo] het kan u ook helpen zien of zijn er authentificatiekwesties overal binnen uw e-mailecosysteem.
DMARC wordt momenteel volledig ondersteund in de Adobe, maar is niet vereist. Gebruik om het even welke vrije DMARC controleur om te zien of hebt u opstelling DMARC voor uw subdomeinen, en als u niet, praat aan uw team van de steun van de Adobe om te zien hoe het best om over het krijgen van die opstelling te gaan. U kunt ook meer informatie vinden over DMARC en hoe u het kunt implementeren [hier](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/technotes/implement-dmarc.html?lang=nl){target="_blank"} for Adobe Campaign and Adobe Journey Optimizer Adobe or [here](https://experienceleague.adobe.com/docs/marketo/using/getting-started-with-marketo/setup/configure-protocols-for-marketo.html){target="_blank"} voor Marketo Engage.

## 1-Klik (Lijst) op Abonnement opzeggen:

Geen paniek. [!DNL Google] en [!DNL Yahoo] hebben het niet over de afmeldingskoppelingen in uw e-mailtekst of voettekst waarop kan worden geklikt door een beveiliger die gewoon zijn werk doet of per ongeluk. Wat zij betekenen is de lijst-Unsubscribe kopbalfunctionaliteit voor of de &quot;mailto&quot;of &quot;http/URL&quot;versies. Dit is de functie binnen de [!DNL Yahoo] en Gmail UIs waar de gebruikers kunnen klikken unsubscribe. Gmail vraagt zelfs gebruikers die op &quot;Report Spam&quot;klikken om te zien of zij bedoeld in plaats daarvan zijn om af te melden, wat het aantal klachten kan verminderen u krijgt (klachten beschadigen uw reputatie) door hen in plaats daarvan in afmeldingsstukken te veranderen (doet uw reputatie niet beschadigen).
Het is belangrijk op te merken dat [!DNL Google] en [!DNL Yahoo] verwijzen beide naar de optie &quot;http/URL&quot; met de naam &quot;1-Click&quot; en dit is opzettelijk. Technisch gezien kunt u met de oorspronkelijke optie &quot;http/URL&quot; ontvangers omleiden naar een website. Dat is niet de focus van [!DNL Yahoo] en [!DNL Google], die beide verwijzen naar de bijgewerkte RFC8058, die zich richt op het verwerken van het afmelden via een HTTPS-verzoek voor POSTEN in plaats van een website, en die het &quot;1-Klik&quot; maakt.
Voor Marketo Engage heeft Adobe de optie &quot;mailto&quot; al ingeschakeld en biedt momenteel geen ondersteuning voor de optie &quot;http/URL&quot;. Verdere actualiseringen hierover.
Voor Adobe Campaign en Adobe Journey Optimizer wordt aangeraden zowel de optie &quot;mailto&quot; als de optie &quot;1-klik&quot; te gebruiken.
Als u meer informatie over hoe te om lijst-uit te voeren wenst, gelieve te controleren [hier] https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/acc-technical-recommendations.html?lang=en#list-unsubscribe){target="_blank"} for Adobe Campaign Classic, [here] (https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-14778.html?lang=en){target="_blank"} for Adobe Campaign Standard, and [here] (https://experienceleague.adobe.com/docs/journey-optimizer/using/email/email-opt-out.html?lang=en){target="_blank"} voor Adobe Journey Optimizer of u kunt op elk gewenst moment contact opnemen met het klantenondersteuningsteam van de Adobe.
De behoefte aan lijst-unsubscribe kopballen is niet op transactie e-mail van toepassing. Gelieve te merken op dat de teweeggebrachte berichten zoals Verlaten Kar en de gelijkaardige die mededelingen niet door de abonnee worden geproduceerd als marketing door brievenbusleveranciers zoals worden beschouwd [!DNL Google] en [!DNL Yahoo] en die zouden lijst-onderbreking nodig hebben.
![afbeelding](https://git.corp.adobe.com/storage/user/38257/files/a2da6bdb-524d-46a7-b765-718c1fe407b0)

## Abonnement binnen 2 dagen verwerken:

Dit is een aanbevolen werkwijze voor een tijdje, aangezien elke e-mail die u implementeert naar iemand die zich niet heeft geabonneerd, meestal leidt tot een spamklacht, dus hoe eerder u stopt met het verzenden van e-mail, hoe beter. Nogmaals, de wettelijke vereisten kunnen in sommige gevallen veel langer zijn, maar [!DNL Google] en [!DNL Yahoo] weet dat hun gebruiker zich heeft afgemeld via List-Unsubscribe en dat u hen nog steeds per e-mail verzendt op dag 3, en zij hebben verklaard dat afzenders die dat doen, niet zullen toestaan om e-mail naar om het even welk van hun gebruikers te blijven verzenden.
Deze eis van twee dagen is voor om het even welk afmelden door de diverse lijst-unsubscribe methodes. In sommige gevallen (zoals &quot;mailto&quot;) betekent dit dat Adobe ze zal verwerken. De Adobe verwerkt alle verzoeken tot opzeggen onmiddellijk na ontvangst van het verzoek, ruim binnen de termijn van twee dagen. In andere gevallen kunt u ze verwerken. Als u deze verzoeken verwerkt, moet u mogelijk wijzigingen aanbrengen om aan deze tijdlijn van twee dagen te voldoen.

## Klachttarieven:

Lage klachtenpercentages onder 0,2% houden is al lange tijd een goede praktijk. [!DNL Google] is van mening dat de lat gedurende langere tijd met 0 , 3 % hoger ligt , maar heeft duidelijk aangegeven dat het nuttig is om de lat onder de 0 , 1 % te houden . Hier volgen de details die ze deelden:
* Doel om de spamsnelheid onder 0,10% te houden.
* Vermijd een spamsnelheid van 0,30% of hoger, vooral gedurende een langere periode.
* Door een lage spamfrequentie te handhaven, kunnen afzenders beter bestand zijn tegen incidentele spikes in feedback van gebruikers.
* Op dezelfde manier zal het handhaven van een hoog spampercentage tot verhoogde spamclassificatie leiden. Het kan tijd vergen voor verbeteringen in de spamsnelheid om positief op de spamclassificatie te wijzen.
  [!DNL Yahoo] heeft verklaard dat hun klachtendrempel eveneens 0 , 30 % zal bedragen .
Als u hulp nodig hebt bij het controleren van uw klachtentarieven, of hulp bij het reduceren van klachten wilt, gelieve met uw Adobe te spreken Leverbaarheid Consultant, of met uw accountteam te spreken over het toevoegen van een Leverbaarheidsconsultant als u nog geen adviseur hebt.

## Hoe zal dit me als markteur beïnvloeden?

Niet voldoen aan deze nieuwe vereisten van Gmail en [!DNL Yahoo] wordt verwacht dat e-mailberichten in de spammap zullen landen of geblokkeerd zullen raken (zodat een stuitbericht van de MBP wordt ontvangen dat aangeeft dat het e-mailbericht niet is bezorgd).
Daarom beveelt de Adobe u ten zeerste aan de hierboven beschreven wijzigingen door te voeren en ervoor te zorgen dat u er zo snel mogelijk aan begint te voldoen. Nu is ook een groot moment om uw prestaties te vergelijken met [!DNL Yahoo] en [!DNL Google] om u toe te staan om te zien of zijn er om het even welke wezenlijke verandering in uw metriek komt Februari.
We zijn hier om u te helpen, dus als u vragen hebt of ondersteuning nodig hebt, kunt u contact opnemen met uw Adobe-leveringsconsultant of met uw accountteam om een leveringsconsultant toe te voegen als u nog geen consultant hebt.

## Zijn er manieren om dit te omzeilen?

Hoewel dit altijd een kwestie is die aan de orde komt, is de realiteit dat deze veranderingen zinvol zijn voor de eindgebruikers van [!DNL Google] en [!DNL Yahoo]-platforms. Zij worden gemotiveerd door de verwachtingen van die gebruikers om deze regels af te dwingen. We raden u niet aan deze wijzigingen te omzeilen, maar een stap terug te zetten en na te denken over de manier waarop deze wijzigingen kunnen worden aangebracht.

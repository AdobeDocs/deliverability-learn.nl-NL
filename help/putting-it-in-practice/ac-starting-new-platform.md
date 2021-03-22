---
title: Een nieuw platform starten
description: Meer informatie over het beheren van de leverbaarbaarheid bij het starten van een nieuw platform met Adobe Campaign.
feature: In de praktijk brengen
topics: Deliverability
kt: null
thumbnail: null
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: 96ed84da391faaabd3001ddd6a411ddc1f46b033
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---


# Een nieuw platform starten {#starting-new-platform}

Het behoud van uw domein en IP adresreputatie is essentieel wanneer vestiging een nieuw platform aan gebruik met Adobe Campaign.

## Een gevoelige stap

U zou zeer voorzichtig moeten zijn wanneer het beginnen om e-mail op een nieuw platform te verzenden, omdat het platform geen geschiedenis van gebruik heeft, en geen reputatie wanneer het verzenden IPs nooit voor dit doel is gebruikt.

ISPs is natuurlijk verdacht van IP adressen die nooit zijn gebruikt om e-mail te verzenden en die plotseling beginnen grote volumes van e-mailverkeer te verzenden. Spammers gebruiken over het algemeen &quot;onbekende&quot;IP adressen (adressen die nooit op lijst van gewezen personen zijn geweest) om het grootste mogelijke aantal berichten vóór opsporing te verzenden.

Je kunt niet verwachten dat je aan het begin van de productiefase een operationele snelheid bereikt in termen van productie. Bovendien zou u niet moeten proberen om berichten aan dit tarief te verzenden aangezien het ISPs zou kunnen leiden om de verzendende adressen te blokkeren en de rest van de aanloopfase ernstig te compromitteren.

## Belangrijkste beginselen

Hieronder staan de belangrijkste beginselen die moeten worden gevolgd bij het opstarten van een nieuw platform.

* Vorm een specifiek subdomein dat voor e-mailcampagnes specifiek is die van Adobe worden verzonden.

* Als u deze informatie hebt, **importeer ongeldige adressen in de quarantainetabel**.
Het beginnen van een platform gebeurt vaak wanneer het gebruiken van een lijst van adressen voor het eerst en die niet volledig gekwalificeerd kunnen zijn. Als u naar ongeldige adressen of naar honingpotadressen verzendt, zal dit tot het verminderen van de reputatie van het platform bijdragen.

   * Als u een lijst van ongeldige adressen hebt, is het in uw beste belang om het in de quarantainetabel in te voeren alvorens voor het eerst te verzenden. De quarantainetabel is beschikbaar via de menu&#39;s **[!UICONTROL Administration > Campaign Management > Non deliverables Management > Non deliverables and addresses]** (Campaign Classic) en **[!UICONTROL Administration > Channels > Quarantines > Addresses]** (Campaign Standard).

   * Als, allen het zelfde, u wenst om de ongeldige adressen opnieuw te kwalificeren, is het verreweg verkieslijk om dit te doen zodra de reputatie van het platform en beetje door beetje wordt gevestigd om het gebruik van slechte adressen in tijd &quot;te &quot;verwateren&quot;.

* **Beperk de doorvoer** door het aantal tapes te beperken. Neem contact op met de Adobe Campaign-beheerder voor meer informatie over het aanpassen van deze technische instelling.

* **De** verkorte volumes geleidelijk verhogen om te voorkomen dat ze als spam worden gemarkeerd. Wijs niet de hele database vanaf het begin aan, maar voeg een extra fractie van de lijst toe telkens als u de gegevens verzendt. Dit zou u moeten toelaten om het volume bij elke stap te verhogen terwijl het verminderen van het algemene tarief van ongeldige adressen. U kunt golven gebruiken om een vloeiende ontwikkeling van de opstartfase te garanderen.

* **Verzend regelmatig**. Tot op zekere hoogte is het beter om regelmatig kleine opnamen te sturen in plaats van sporadisch grote campagnes.
* **Let goed op de leveringsrapporten**. De hoge foutenindicatoren kunnen betekenen een technisch plaatsen slecht gevormd is.

## Aanvullende bronnen

Raadpleeg de volgende secties voor meer informatie over de bovenstaande beginselen en de toepassing ervan op Adobe Campaign:

* [Verhoog uw e-mailreputatie met opwarming van IP](../../help/additional-resources/increase-reputation-with-ip-warming.md)
* [Alles over spamovervullingen](../../help/additional-resources/all-about-spam-traps.md)

**Adobe Campaign Classic**

* [De levering optimaliseren via quarantines](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html#optimizing-your-delivery-through-quarantines)
* [Identificeer quarantined adressen voor het volledige platform](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html#identifying-quarantined-addresses-for-the-entire-platform)
* [Verzenden met meerdere golven](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/key-steps-when-creating-a-delivery/steps-sending-the-delivery.html#sending-using-multiple-waves)
* [Aflevering](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/about-delivery-monitoring.html#sending-messages)

**Adobe Campaign Standard**

* [De levering optimaliseren via quarantines](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html#optimizing-your-delivery-through-quarantines)
* [Identificeer quarantined adressen voor het volledige platform](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html)
* [Een levering controleren](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/monitoring-a-delivery.html)

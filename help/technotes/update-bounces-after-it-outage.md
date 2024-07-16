---
title: Bounce-kwalificatie bijwerken na Italia Online-uitgang
description: Leer hoe u de stuiterkwalificatie bijwerkt na Italia Online-storing
feature: Deliverability
exl-id: a11e88cf-bf37-42cc-9c09-1d58360459b7
hide: true
hidefromtoc: true
role: Admin
level: Beginner
source-git-commit: 6b312cdbba496818337c97ec4f42962aea757901
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 2%

---

# Onjuiste hard bounces bijwerken na Italia Online-storing {#update-bounce-italia}

## Context{#outage-context}

Vanaf 22 januari (lokale tijd) heeft Italia Online een stroomstoring doorgemaakt die tot verschillende vertragingen heeft geleid en e-mailberichten heeft afgewezen. De service begon op 26 januari met beperkte capaciteit te worden hervat.

De beïnvloede domeinen zijn: **libero.it**, **virgilio.it**, **inwind.it**, **iol.it**, en **blu.it**.

Dit probleem heeft zich voorgedaan van 22-1-2023 tot 26-11-2023, maar het grootste deel van de ten onrechte in quarantaine gehouden dieren vond plaats op 26 januari.

Leer meer in de officiële mededeling [ hier ](https://tecnologia.libero.it/avviato-il-ritorno-online-di-libero-mail-e-virgilio-mail-66832) {_blank}.


## Gevolgen{#outage-impact}

Net als in de meeste gevallen waarin een internetprovider (ISP) buiten bedrijf is, zijn sommige e-mails die via Campagne of Journey Optimizer zijn verzonden, ten onrechte gemarkeerd als beloften. Dit was niet alleen van invloed op de Adobe, maar iedereen probeerde om via e-mail aan Italia Online te worden bezorgd tijdens de periode van de storing.

Symptomen waren:

* **zachte grenzen** met het bericht `452 requested action aborted: try again later` - deze werden automatisch opnieuw geprobeerd, en geen acties zijn nodig.

* **de Vaste stuitingen** met het bericht `550 <email address> recipient rejected` zijn teruggekeerd door ISP op 26 Januari, tussen 8am - 2 pm lokale tijd, om afzenders te verhinderen overladend hun servers. Zoals bevestigd door de Italia Online Postmaster, zijn dit geen echte harde bochten, dus raden we aan om alle e-mailadressen die op 26 januari 2023 zijn uitgesloten, uit de quarantaine te halen vanwege dat bericht.

## Proces voor bijwerken{#outage-update}

### Adobe Campaign{#ac-update}

Volgens de standaardlogica voor stuitverwerking heeft Adobe Campaign deze ontvangers automatisch toegevoegd aan de quarantainelijst met een **[!UICONTROL Status]** instelling van **[!UICONTROL Quarantine]** . U kunt dit corrigeren door uw quarantainetabel in Campagne bij te werken door deze ontvangers te zoeken en te verwijderen of door hun **[!UICONTROL Status]** in **[!UICONTROL Valid]** te wijzigen zodat deze tijdens de nachtelijke opschoonworkflow worden verwijderd.

Om de ontvangers te vinden die door deze kwestie werden beïnvloed, of in het geval dit opnieuw met een andere ISP gebeurt, gelieve de instructies hieronder te zien:

* Voor Campaign Classic v7 en Campagne v8, verwijs naar [ deze pagina ](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html?lang=en#unquarantine-bulk) {_blank}.
* Voor Campaign Standard, verwijs naar [ deze pagina ](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html?lang=en#unquarantine-bulk) {_blank}.

### Adobe Journey Optimizer{#ajo-update}

Adobe Journey Optimizer heeft deze e-mailadressen automatisch, met de instelling **[!UICONTROL Reason]** van **[!UICONTROL Invalid Recipient]** , toegevoegd aan de suppressielijst. U kunt dit corrigeren door de onderdrukkingslijst bij te werken door deze e-mailadressen te zoeken en te verwijderen.

Zodra geïdentificeerd, kunnen deze adressen manueel uit de onderdrukkingslijst worden verwijderd gebruikend de **[!UICONTROL Delete]** knoop. Deze adressen kunnen dan in toekomstige e-mailcampagnes worden omvat.

Leer meer in [ deze sectie ](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list.html#remove-from-suppression-list) {_blank}.


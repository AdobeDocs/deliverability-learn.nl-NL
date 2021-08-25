---
title: Realtimelijsten van zwarte gaten
description: Leer over organisaties die lijsten van IP adressen en domeinen handhaven waarschijnlijk om door spammers worden gebruikt.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 4155b89f-a636-404c-8951-563c1b4d0289
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---

# Realtimelijsten van zwarte gaten

Verscheidene organisaties handhaven gegevensbestanden van IP adressen en domeinen die worden genoemd om door spammers worden gebruikt. Het raadplegen van deze sites kan nuttig zijn om te begrijpen waarom bepaalde berichten zijn afgewezen als spam. Over het algemeen is het mogelijk te verzoeken dat een adres wordt verwijderd dat ten onrechte aan deze lijsten is toegevoegd.

Deze databases worden RBL&#39;s (Real-Time Blackgat Lists) genoemd en ze worden via een DNS-mechanisme geraadpleegd. Er zijn drie soorten RBLs:

* Op IP-adres: maakt een lijst IP adressen die spam verzenden of waarschijnlijk spam opnieuw zal afspelen.
* Op senderdomein: maakt een lijst van afzenderdomeinen (volledig domein van het stuiterende postadres) die spam verzenden of verkeerd gevormd.
* Op webdomein: geeft een lijst weer van de domeinen (domeinen op hoog niveau zoals geregistreerd met de registrars) die in URLs van de verbindingen en beelden worden gevonden bevat in spaminhoud. In de oplossingen van Adobe, is het te overwegen domein over het algemeen het adres dat voor het volgen wordt gebruikt.

Hieronder volgt een lijst van de meest gebruikte RBL&#39;s. Voor een uitgebreidere lijst kunt u [https://www.dnsstuff.com/](https://tools.dnsstuff.com/) raadplegen.

* **Spamhaus**

   Zie [https://www.spamhaus.org/](https://www.spamhaus.org/)

   De database is belangrijker. De indeling op deze lijst is over het algemeen een ernstige situatie. Als dit gebeurt, moet u ONMIDDELLIJK handelen en de commerciële diensten, de leverbaarheid, en [Adobe klantenZorg ](https://helpx.adobe.com/nl/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) waarschuwen.

* **SpamCop**

   Zie [https://www.spamcop.net/](https://www.spamcop.net/)

   Het is een van de bekendste databases. Als één van uw IP adressen op deze lijst wordt geplaatst, betekent dit over het algemeen dat de gebruikers SpamCop uw berichten als spam hebben verklaard of dat u berichten naar een honeypot SpamCop hebt verzonden.

* **URIBL**

   Zie [https://www.uribl.com/](https://www.uribl.com/)

   Deze lijst identificeert de domeinen die regelmatig in berichten verschijnen die als spam worden verklaard. Als uw domein in deze lijst wordt weergegeven, kan dit van invloed zijn op de leesbaarheid. U moet de services voor de levering en [Adobe Customer Care](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) onmiddellijk op de hoogte stellen.

* **SURBL**

   Zie [http://www.surbl.org/](http://www.surbl.org/)

   De SURBL identificeert de websites die regelmatig in spam verschijnen. Als uw domein in deze lijst wordt weergegeven, kan dit van invloed zijn op de leesbaarheid. U moet de services voor de levering en [Adobe Customer Care](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) onmiddellijk op de hoogte stellen.

* **iX Manitu**

   Dit is een lijst van IP&#39;s en wordt in Duitsland op grote schaal gebruikt. Zie [https://www.heise.de/ix/nixspam/](https://www.heise.de/ix/nixspam/)

<!--* SORBS

  [https://www.nl.sorbs.net](https://www.nl.sorbs.net) compiles a list of IP addresses that are reputed to be dynamic IP address (i.e. attributed temporarily to ISP subscribers) or "open relay" addresses. Certain domains check whether the IP address of a sender is not listed on this site before accepting email. Checking the IP addresses on this site can prove useful.-->

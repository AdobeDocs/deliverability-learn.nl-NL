---
title: Realtimelijsten van zwarte gaten
description: Leer over organisaties die lijsten van IP adressen en domeinen handhaven waarschijnlijk om door spammers worden gebruikt.
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 4155b89f-a636-404c-8951-563c1b4d0289
source-git-commit: e7427d6109f3201affa58decde36294d1631bf5b
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 2%

---

# Realtimelijsten van zwarte gaten

Verscheidene organisaties handhaven gegevensbestanden van IP adressen en domeinen die worden genoemd om door spammers worden gebruikt. Het raadplegen van deze sites kan nuttig zijn om te begrijpen waarom bepaalde berichten zijn afgewezen als spam. Over het algemeen is het mogelijk te verzoeken dat een adres wordt verwijderd dat ten onrechte aan deze lijsten is toegevoegd.

Deze databases worden RBL&#39;s (Real-Time Blackgat Lists) genoemd en ze worden via een DNS-mechanisme geraadpleegd. Er zijn drie soorten RBLs:

* Door IP adres: lijsten IP adressen die spam verzenden of waarschijnlijk spam opnieuw zullen afspelen.
* Door afzenderdomein: maakt een lijst van afzenderdomeinen (volledig domein van het stuiterende postadres) die spam verzenden of verkeerd gevormd.
* Op webdomein: geeft een lijst weer van de domeinen (domeinen op hoog niveau die zijn geregistreerd bij de registrars) die worden gevonden in de URL&#39;s van de koppelingen en afbeeldingen in spaminhoud. In oplossingen van de Adobe, is het domein dat moet worden overwogen over het algemeen het adres dat voor het volgen wordt gebruikt.

Hieronder volgt een lijst van de meest gebruikte RBL&#39;s. Voor een uitvoerigere lijst, kunt u naar [ https://www.dnsstuff.com/ ](https://tools.dnsstuff.com/) verwijzen.

* **Spamhaus**

  Verwijs naar [ https://www.spamhaus.org/](https://www.spamhaus.org/)

  De database is belangrijker. De indeling op deze lijst is over het algemeen een ernstige situatie. Als dit gebeurt, moet u ONMIDDELLIJK handelen en commerciële diensten, leverbaarheid, en [ de Zorg van de Klant van de Adobe ](https://helpx.adobe.com/nl/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) waarschuwen.

* **SpamCop**

  Verwijs naar [ https://www.spamcop.net/](https://www.spamcop.net/)

  Het is een van de bekendste databases. Als één van uw IP adressen op deze lijst wordt geplaatst, betekent dit over het algemeen dat de gebruikers SpamCop uw berichten als spam hebben verklaard of dat u berichten naar een honeypot SpamCop hebt verzonden.

* **URIBL**

  Verwijs naar [ https://www.uribl.com/](https://www.uribl.com/)

  Deze lijst identificeert de domeinen die regelmatig in berichten verschijnen die als spam worden verklaard. Als uw domein in deze lijst wordt weergegeven, kan dit van invloed zijn op de leesbaarheid. U zou de leverbaarheidsdiensten en ](https://helpx.adobe.com/nl/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) onmiddellijk de Zorg van de Klant van de Adobe moeten informeren [.

* **SURBL**

  Verwijs naar [ https://surbl.org/](https://surbl.org/)

  De SURBL identificeert de websites die regelmatig in spam verschijnen. Als uw domein in deze lijst wordt weergegeven, kan dit van invloed zijn op de leesbaarheid. U zou de leverbaarheidsdiensten en ](https://helpx.adobe.com/nl/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) onmiddellijk de Zorg van de Klant van de Adobe moeten informeren [.

* **iX Manitu**

  Dit is een lijst van IP&#39;s en wordt in Duitsland op grote schaal gebruikt. Verwijs naar [ https://www.heise.de/ix/nixspam/](https://www.heise.de/ix/nixspam/)

<!--* SORBS

  [https://www.nl.sorbs.net](https://www.nl.sorbs.net) compiles a list of IP addresses that are reputed to be dynamic IP address (i.e. attributed temporarily to ISP subscribers) or "open relay" addresses. Certain domains check whether the IP address of a sender is not listed on this site before accepting email. Checking the IP addresses on this site can prove useful.-->

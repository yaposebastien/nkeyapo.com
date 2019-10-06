---
title: Envoyer un sms chaque deux minutes
author: Nke Yapo
tags: GNU/Linux, Gammu
subtitle: Tutoriel
---


L'objet de ce tutoriel est clair. Comment envoyer un SMS chaque deux minutes avec Gammu et Cron?. Pour rappel Gammu est un utilitaire en ligne de commande qui permet de controler son telephone. Par contre CRON est un programme qui permet aux utilisateurs des systèmes Unix d’exécuter automatiquement des scripts, des commandes ou des logiciels à une date et une heure spécifiées à l’avance, ou selon un cycle défini à l’avance.
[source wikipedia](https://fr.wikipedia.org/wiki/Cron)

 Edition de notre tache CRON.
 ---

 Se connecter en tant que root et excecuter cette commande.

 `# crontab -e`

 Et saisir cette ligne suivante qui definit la periode et la commande gammu

 `*/2 * * * * echo" Ce message envoit un sms chaque deux miniutes" | gammu --sendsms TEXT +22547304645`

Ensuite lancer notre daemon gammu-smsd via la commande ci-dessous:
		
`# gammu-smsd`

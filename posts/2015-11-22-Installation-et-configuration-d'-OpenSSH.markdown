---
title: Installation et configuration d'un serveur OpenSSH
author: Nke Yapo
tags: GNU/Linux, OpenSSH, Security
subtitle: Tutoriel
---

![Architecture](https://s3.us-east-2.amazonaws.com/images.nkeyapo.com/images/openssh/tutoriel_openssh.png)


**Etape 1 : Installation openssh-server and openssh-client**

`# apt-get install openssh-server openssh-client`

**Etape 2 : Test de la connexion en local**

Avant de tester la connexion sur le serveur, créer votre utilisateur (dans notre cas attecoube).

`# ssh -l attecoube 192.168.1.81`

Repondre “yes” à la question au prompt

**Etape 3 : Test de connexion sur l'ordinateur distant.**

exit 

`# ssh -p 22 attecoube@192.168.1.81` (l'option -p spécifie le port du service ssh, 22 est le port par defaut)

Astuce : Pour renforcer la sécurité, la modification du port est fortement recommandée. 

*Edition du fichier /etc/ssh/sshd_config
*Rechercher la ligne Port et modifier cette valeur (Exple: 2020)
*Configurer votre routeur afin d'autoriser cette connexion

**Etape 4 : Vérification de la clé Hash de chiffrement.**

La Vérification de cette clé se fait en consultant le contenu du fichier known_hosts dans le repertoire de l'utilisateur côté serveur(attecoube dans notre cas). Le contenu de fichier texte permet d'établir la correspondance entre le serveur et l'ordinateur distant. Celui-ci ne peut être édité, mais en cas d'éventuel redeploiement du serveur son contenu peut être supprimé. 

`$ cat .ssh/known_hosts`

La type d'encryption supporté par le serveur est vérifié à travers cette commande suivante :

`# ssh -vp 2020 attecoube@192.168.1.81`

**Etape 5 : Génération des clés de chiffrement RSA et DSA**

Le serveur OpenSSH supporte la combinaison des deux clés RSA et DSA pour des raisons sécuritaires. Par exemple, l'utilisation de la seule clé DSA peut être hacker par une force brute. En revanche, RSA génère un chiffrement aléatoire qui la rend moins vulnerable aux attques.

Generation de la clé DSA

`# ssh-keygen -t dsa`

Vous pouvez valider cette action par la touche entrée et confirmer par la meme occasion l'emplacement de cette clé.Ensuite, ajouter votre passphrase.La clé id_dsa_pub sera transmise du serveur a l'ordinateur lors de la tentative de connexion, et permet ainsi au systeme de decrypter la clé privé.

Generation de la clé RSA

`# ssh-keygen -t RSA`

Nous allons maintenant copier nos identifiants à partir de l'utilitaire ssh-copy-id.

    $ eval 'ssh-agent -s'
    # ssh-copy-id -p 2020 attecoube@192.168.1.81
    $ ssh-add et saisir votre passphrase
    $ ssh-add -l

**Etape 6: connexion a partir de l'ordinateur client.**

`$ ssh -p 2020 attecoube@192.168.1.81`



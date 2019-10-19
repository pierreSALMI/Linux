# tp-dns

Ce petit TP permet de jouer avec une architecture DNS 

## Présentation 

Nous construisons via le vagrantfile :
 
- Deux serveur DNS de récurssion accessible que depuis le réseaux interne (192.168.33.0/24)
- Deux serveurs autoritatifs avec une interface web d’administration accessible sur le reseaux interne et le service dns exposer sur le réseaux publique (192.168.56.0/24)
- Le domaine lab.local est povisionné sur les serveur dns authoritatifs et les serveurs récursifs `forward` les requêtes pour ce domaine vers les serveurs autoritatifs.
- Un reverse proxy accessible depuis le réseaux publique (192.168.56.0/24)
- deux serveurs web wiki et back accessible que depuis le réseaux privé (192.168.33.0/24)

Une interface web est disponible sur les deux serveurs autoritatif via les urls :  http://192.168.33.31/poweradmin/ et http://192.168.33.32/poweradmin/ 
Login : admin ; mot de passe xxxxxx

> attention après avoir récupèrer le dépot, une seule commande à passer "vagrant up" mais les traitements peuvent être long, ne les interrompez pas.

## Question

* Connectez vous au host "proxy" avec vagrant et vérifier Comment est configuré le resolver dns du système ?

Le fichier resolv.conf est configuré pour redirigé vers les serveurs recursifs


* Retrouvez l'adresse ip du host wiki.lab.local avec la commande dig.
```
;; ANSWER SECTION:
wiki.lab.local.         3600    IN      A       192.168.56.11
```
l'adresse ip de wiki.lab.local est 192.168.56.11

* Connectez vous au host auth-1, quels sont les services réseaux qui sont en fonctionnement actuellement quels sont leur socket d'écoute ?
Les services réseaux qui fonctionnent sont http, mysql[3306] et pdns

* Connectez vous au host recursor-1,  quels sont les services réseaux qui sont en fonctionnement actuellement quels sont leur socket d'écoute ?
Le service réseaux qui fonctionent sont pdns 

* Où sont configuré chacuns de ces composants ?
```
/etc/pdns-recursor/recursor.conf
/etc/NetworkManager/NetworkManager.conf
/etc/httpd/conf/httpd.conf
/etc/my.cnf
```

* Qu'est ce qui est configuré sur les serveurs recursifs pour le domaine lab.local ? (Important pour les Actions qui suivent)
Un forward vers les serveurs authoritatifs est configuré pour lab.local sur les serveurs recursif
```
'147aforward-zones=lab.local=192.168.56.31;192.168.56.32'
```

* Comment mettre en évidence le fait que le récurseurs ne répondent que sur l’interface du réseaux back (192.168.33.0/24) 
En faisant la commande `dig wiki.lab.local @192.168.56.21` `dig wiki.lab.local @192.168.56.21`
ou en regardant l'interface d'écoute avec la commande `ss -4l` 
` tcp   LISTEN     0      128                                                                       192.168.33.21:domain                                                                                              *:*     `

* Comment est sécurisé l’accès à mysql ?

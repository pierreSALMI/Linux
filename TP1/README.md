# TP1 - Vagrant

## Installation Dokuwiki

Dasn un premier temps on installe apache2, et PHP7
```
  apt-get -y -qq install apache2
  apt-get install libapache2-mod-php7.0
  apt-get install php7.0-mbstring
```

Puis on télécharge Dokuwiki

```
 wget -q -O /opt/src/dokuwiki-stable.tgz https://download.dokuwiki.org/src/dokuwiki/dokuwiki-stable.tgz
  tar zxf /opt/src/dokuwiki-stable.tgz -C /var/www/html
  mv /var/www/html/dokuwiki-2018-04-22b /var/www/html/dokuwiki
```

On créé l'utilisateur wiki et lui affectons les droits requis pour Dokuwiki
```
  useradd -m -G www-data wiki
  chown -R wiki:www-data /var/www/html/dokuwiki/
  chmod -R g+w /var/www/html/dokuwiki
```

Restart
`systemctl restart apache2`

## Installation Rsync + Crontab

Telechargement
`apt-get install rsync`

Sauvegarde du dossier dokuwiki
`*/5 * * * * rsync -ap --chown=wiki:www-data --chmod-ug+w -e "ssh -o StrictHostKayChacking=no" wiki@192.168.56.12:/var/www/html/dokuwiki /var/www/html/dokuwiki/' | sudo -u wiki crontab`

## Relation d'aprobation

Création premierement de ` id_rsa_wiki` et `id_rsa_wiki.pub` sur notre machine puis copie
```
  cp /vagrant/id_rsa_wiki /home/wiki/.ssh
  cat /vagrant/id_rsa_wiki.pub > /home/wiki/.ssh/authorized_keys
```

Création des clées pour l'authentification
```
  ssh-keyscan 192.168.56.11 >> /home/wiki/.ssh/authorized_keys
  ssh-keyscan 192.168.56.12 >> /home/wiki/.ssh/authorized_keys
```

Affectation des droits pour l'utilisateur
```
  chown -R wiki:wiki /home/wiki/.ssh
  chmod 600 /home/wiki/.ssh/*
```
# Linux
## Le jeux du plus ou moins
Le but du script est de jouer au jeux du plus ou moins. On sauvegarde un chiffre random entre 0 et 1000. Il faut retrouver le chiffre random pour pouvoir finir le jeux.
Je n'ais pas eu de probleme pour ce script
```
#!/bin/bash

let random=($RANDOM%1000)
a=0
b=0
echo "la reponse est" $random
# la réponse est donné pour pouvoir sortir du jeux

trap "echo ' Aled, tu peux pas ctrl_c'" 2 3

while [ $a != $random ]; do
        read a
        if [ $a -eq $a 2>/dev/null ]
        then
                let b=b+1
                if [ $a -lt $random ]
                then
                        echo "c +"
                elif [ $a -gt $random ]
                then
```

## Un outils de sauvegarde
Le but du script est de sauvegarder un dossier défini quand on est vendredi.
Je n'ais pas réussi à faire la sauvegarde partielle pour ce script et ne possede plus ma version d'essaie.
```
#!/bin/bash

date=$(date +"%a")
backup=~/Desktop/backup.tar
cd ~/Desktop

if [ $date == "ven." ]
then
        tar -rvf $backup $1
fi
```

## youtube-dl
Le but du script est de télécharger l'audio d'une vidéo youtube dans le dossier musique crée auparavant.
Je n'ais pas eu de probleme pour ce script
```
#!/bin/bash

mkdir -p ~/Desktop/musique
cd ~/Desktop/musique
youtube-dl -f 140 $1
```

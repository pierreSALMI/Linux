# Linux
## Le jeux du plus ou moins
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
```
#!/bin/bash

mkdir -p ~/Desktop/musique
cd ~/Desktop/musique
youtube-dl -f 140 $1
```

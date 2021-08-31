# Linux

## Sommaire

### [Cours 1 - Les commandes du terminal](#cours-1-:-les-commandes-du-terminal)

1. [Créer des liens symboliques](#creer-des-liens-symboliques)

2. [Visualiser le contenu d'un fichier](#visualiser-le-contenu-dun-fichier)
   1. [Commande `cat`](#commande-cat)
   2. [Commande `less`](#commande-less)
   3. [Commande `tail`](#commande-tail)
   4. [Commande `head`](#commande-head)
   5. [Commande `strings`](#commande-strings)

3. [Afficher les stats d'un fichier](#afficher-les-stats-dun-fichier)
   1. [Commande `stat`](#commande-stat)
   2. [Commande `wc`](#commande-wc)
   3. [Commande `du`](#commande-du)
   4. [Commande `df`](#commande-df)
4. [Manipuler les permissions](#manipuler-les-permissions)
   1. [Les permissions](#les-permissions)
   2. [Commande `chmod`](#commande-chmod)
   3. [Exécuter des commandes en tant que superuser](#exécuter-des-commandes-en-tant-que-superuser)
5. [Effectuer des recherches et autres opérations](#effectuer-des-recherches-et-autres-operations)
   1. [Commande `find`](#commande-find)
   2. [Commande `grep`](#commande-grep)
   3. [Remplacement par "globbing"](#le-remplacement-"par-globbing")
   4. [La redirection](#la-redirection)
   5. [Le pipe](#le-pipe)
   6. [Aller plus loin avec `find`](#aller-plus-loin-avec-find)
   7. [Compresser et décompresser avec `tar`](#compresser-et-décompresser-avec-tar)

---

## Cours 1 : Les commandes du terminal

### CREER DES LIENS SYMBOLIQUES

```bash
ln -s {fichier ou dossier pointé} {nom_du_lien}
```



### VISUALISER LE CONTENU D'UN FICHIER

#### Commande `cat`

```bash
cat {nom_du_fichier}
```

##### Options

`-n`: numéroter les lignes du fichier

`-b`: supprimer les lignes vides

`-s`: regrouper les lignes vides successives en une seule ligne vide

> Le problème de `cat`c'est que l'ensemble du fichier est affiché (pose souci pour les fichiers très longs ... )



#### 	Commande `less`

> La commande `less` lance d'une certaine façon, un éditeur de texte en lecture seule pour lire le fichier et y naviguer, en commançant par le haut du fichier

```bash
less {nom_du_fichier}
```

##### Commandes :

`ESPACE` : faire défiler le fichier

`q`: quitter la commande `less`

`f` : _forward_ - pour avancer dans le fichier

`b`: _backward_ - pour revenir en arrière dans le fichier

`/{recherche}`: lancer une recherche

`n`: _next_ - continuer la recherche



#### Commande `tail`

> Affiche les 10 dernières lignes du fichier (par défaut)

```bash
tail {nom_du_fichier}
```

##### Options

`-f`: garder le fichier ouvert et affiche en temps réel les modifications

`-n{integer}`: afficher le nombre de ligne passé en paramètre (au lieu des 10 lignes par défaut )



#### Commande `head`

> Affiche les 10 premières lignes du fichier (par défaut)

```bash
head {nom_du_fichier}
```



#### Commande `strings`

> Extrait les chaînes de caractère compilés d'un fichier ou même d'un exécutable et les affiche à l'écran

```bash
strings {nom_du_fichier}
```



### AFFICHER LES STATS D'UN FICHIER

#### Commande `stat`

```bash
stat {nom_du_fichier}
```

```bash
pi@rpidemanu:/var $ stat log/syslog
  Fichier : log/syslog
   Taille : 25077     	Blocs : 64         Blocs d'E/S : 4096   fichier
Périphérique : b302h/45826d	Inœud : 6545        Liens : 1
Accès : (0640/-rw-r-----)  UID : (    0/    root)   GID : (    4/     adm)
 Accès : 2021-08-27 00:00:34.758559207 +0400
Modif. : 2021-08-27 13:24:02.846841408 +0400
Changt : 2021-08-27 13:2
```



#### Commande `wc`

```bash
wc {nom_du_fichier}
pi@rpidemanu:/var $ wc log/syslog
  305  3289 25077 log/syslog
```

> Les trois nombre renvoyés sont respectivement :
>
> - Le nombre de ligne (305)
> - Le nombre de mots (3289)
> - Le nombre d'octets (25077)



#### Commande `du`

> _**D**isk **U**sage_ : affiche une taille en nombre de blocs.. pas très pratique en l'état, on utilisera donc les options ci-dessous

##### Options

`-b`: afficher le nombre d'octets

`-h` : _Human Readable_ - convertir en Ko, Mo, Go, etc.

`-H`: équivalent à `-h`minuscule mais divise les multiples par 1000 et non 1024 octets

`-s` : afficher uniquement le total



#### Commande `df`

> Affiche le taille des périphériques montés sur la machine

```bash
pi@rpidemanu:~/Documents/raspberry-script $ df -H
Sys. de fichiers Taille Utilisé Dispo Uti% Monté sur
/dev/root           16G    5,2G  9,6G  35% /
devtmpfs           1,9G       0  1,9G   0% /dev
tmpfs              2,1G       0  2,1G   0% /dev/shm
tmpfs              2,1G    9,0M  2,1G   1% /run
tmpfs              5,3M    4,1k  5,3M   1% /run/lock
tmpfs              2,1G       0  2,1G   0% /sys/fs/cgroup
/dev/mmcblk0p1     265M     52M  213M  20% /boot
tmpfs              403M    4,1k  403M   1% /run/user/1000
```



### MANIPULER LES PERMISSIONS

```ba
pi@rpidemanu:~ $ ls -l
total 36
drwxr-xr-x 2 pi pi 4096 mai    7 18:52 Bookshelf
drwxr-xr-x 2 pi pi 4096 mai    7 19:07 Desktop
drwxr-xr-x 4 pi pi 4096 août  25 15:38 Documents
drwxr-xr-x 2 pi pi 4096 mai    7 19:07 Downloads
drwxr-xr-x 2 pi pi 4096 mai    7 19:07 Music
drwxr-xr-x 2 pi pi 4096 mai    7 19:07 Pictures
drwxr-xr-x 2 pi pi 4096 mai    7 19:07 Public
drwxr-xr-x 2 pi pi 4096 mai    7 19:07 Templates
drwxr-xr-x 2 pi pi 4096 mai    7 19:07 Videos
```

#### Les permissions

r : read

w : write

x : execute

Il y a trois blocs :

- Le propriétaire
- Le groupe propriétaire
- Tout le monde

#### Commande `chmod`

> Modifie les permissions d'un fichier

Deux possibilités :

**1 - En octal**

Chaque « groupement » de droits (pour user, group et other) sera représenté par un chiffre et à chaque droit correspond une valeur :

r (read) = 4

w (write) = 2

x (execute) = 1

= 0

Par exemple,

- Pour **rwx**, on aura : 4+2+1 = 7

- Pour **rw-**, on aura : 4+2+0 = 6
- Pour **r--**, on aura : 4+0+0 = 4

Ce qui permet de faire toutes les combinaisons :

- 0 : **`- - -`** (aucun droit)
- 1 : **`- - x`** (exécution)
- 2 : **`- w -`** (écriture)
- 3 : **`- w x`** (écriture et exécution)
- 4 : **`r - -`** (lecture seule)
- 5 : **`r - x`** (lecture et exécution)
- 6 : **`r w -`** (lecture et écriture)
- 7 : **`r w x`** (lecture, écriture et exécution)

Reprenons le répertoire `Documents`. Ses permissions sont :

```bash
drwxr-x---
```

En octal, on aura **750** :

```bash
   rwx        r-x        ---
 7(4+2+1)   5(4+0+1)   0(0+0+0)
```

Pour mettre ces permissions sur le répertoire on taperait donc la commande :

```bash
chmod 750 Documents
```



**2 - En gérant chaque droit séparément**

1. À qui s'applique le changement
   - **u** (**u**ser, utilisateur) représente la catégorie "propriétaire" ;
   - **g** (**g**roup, groupe) représente la catégorie "groupe propriétaire" ;
   - **o** (**o**thers, autres) représente la catégorie "reste du monde" ;
   - **a** (**a**ll, tous) représente l'ensemble des trois catégories.
2. La modification que l'on veut faire
   - **+** : ajouter
   - **-** : supprimer
   - **=** : affectation
3. Le droit que l'on veut modifier
   - **r** : **r**ead ⇒ lecture
   - **w** : **w**rite ⇒ écriture
   - **x** : e**x**ecute ⇒ exécution

Par exemple :

```bash
chmod o-w fichier3
```

enlèvera le droit d'écriture pour les autres.

```bash
chmod a+x
```

ajoutera le droit d'exécution à tout le monde.

On peut aussi combiner plusieurs actions en même temps :

- On ajoute la permission de lecture, d'écriture et d'exécution sur le fichier `fichier3` pour le **propriétaire** ;
- On ajoute la permission de lecture et d'exécution au **groupe propriétaire**, on retire la permission d'écriture ;
- On ajoute la permission de lecture aux **autres**, on retire la permission d'écriture et d'exécution.

```bash
chmod u+rwx,g+rx-w,o+r-wx fichier3
```



#### Exécuter des commandes en tant que superuser

`sudo` : _Super User Do_ : exécute une commande en tant que superutilisateur

`sudo su` : permet de rester superutilisateur pendant un laps de temps déterminé par le système



### EFFECTUER DES RECHERCHES ET AUTRES OPERATIONS

#### Commande `find`

```bash
find {repertoire_de_recherche} {-option} {critere_de_recherche} {action}
```

> Contrairement aux autres commandes, les options sont nommés par leur nom complet et non pas par une seule lettre. De plus, même si on le nomme par son nom complet, on ne mettra qu'un tiret devant l'option



```bash
pi@rpidemanu:~ $ find /home/pi/Documents/raspberry-script/ -name fan* -print
/home/pi/Documents/raspberry-script/fanoff
/home/pi/Documents/raspberry-script/fanon
```

> {repertoire_de_recherche} : `/home/pi/Documents/raspberry-script/`
>
> {-option} : `-name` - recherche par nom
>
> {critere_de_recherche} : `fan*` - soit tous les fichiers commençant par "fan[...]"
>
> {action} : `-print` - affiche tous les résultats de la recherche



##### Options de recherche

`-name` : recherche par nom

`-path` : recherche par dossier

```bash
pi@rpidemanu:~ $ find /home/pi/ -path /home/pi/*/cputemp -print
/home/pi/Documents/raspberry-script/cputemp
```

`-lname` : recherche dans les cibles de lien symbolique

`-iname` : recherche par expressions régulières (RegExp)

`-type` : recherche par type

- f : file - fichier
- d : directory - dossier
- l : link - lien symbolique

`-atime` : recherche le(s) fichiers **a**ccédé(s) depuis x _jours_

```bash
 sudo find / -atime 1
/var/log/kern.log
/var/log/user.log
/var/log/daemon.log
/var/log/auth.log
/var/log/messages
/var/log/debug
/var/log/syslog.1
/var/log/cups/access_log.1
/var/cache/cups/job.cache.O
```

>ci-dessus, on recherche tous les fichiers qui ont été accédé depuis **1** jour

`-ctime` :  recherche le(s) fichiers **c**hangé(s) depuis x _jours_

`-mtime` : recherche le(s) fichiers **m**odifié(s) depuis x _jours_

`-[a-c-m]min` : idem que time - on ne compte plus en jours mais en _minutes_

`-[a-c-'']newer` : recherche les fichiers accédés / changés / modifiés (ne pas préciser le -m !!!) plus récemment que le fichier passé en paramètres

```bas
pi@rpidemanu:~/Documents $ find / -anewer /home/pi/Documents/raspberry-script/cputemp
```

> recherche tous les fichiers accédés après le fichier `/home/pi/Documents/raspberry-script/cputemp`

`-size` : recherche par taille

`-empty` : recherche les fichiers vides

> les critères de recherche sont cumulables !
>
> on aurait très bien pu écrire
>
> ` find / -anewer /home/pi/Documents/raspberry-script/cputemp -empty -type d`
>
> recherche tous les **répertoires**, **vides** accédés après `/home/pi/Documents/raspberry-script/cputemp`



#### Commande `grep`

```bash
grep {RegExp} {fichier_repertoire}
```

> filtre les lignes correspondantes à l'expression régulière (sensible à la casse)

##### Options

`-i` : insensible à la casse

`-v` : inverse la recherche

`-c` : renvoie le nombre de lignes trouvés

`-n` : affiche le numéro de la ligne

`-l` : renvoie uniquement le nom du fichier

`-r` : prend en compte les sous-dossiers de manière récursive

```bash
pi@rpidemanu:~ $ grep "gpio" -rl ./Documents/raspberry-script
./Documents/raspberry-script/fanoff
./Documents/raspberry-script/cputemp
./Documents/raspberry-script/fanon
```

> affiche les fichiers (`-l`) qui contiennent le mot "gpio" dans le dossier courant, ainsi que les sous-dossiers (`-r`)



#### Le remplacement par "globbing"

`*` : remplace par n'importe quel(s) caractère(s)

`?` : remplace par un caractère

`\` : échappe un caractère "réservé"

> `ls \???` : liste les fichiers commençant par ? et ayant trois caractères au total

`[..]` : remplace par une liste définie

> `ls [ws]??` : liste les fichiers commençant par w ou s et ayant trois caractères au total
>
> on peut utiliser une RegExp
>
> `ls [^ws]??` : liste les fichiers ne commençant pas par w ou s et ayant trois caractères au total



#### La redirection

`STDIN`: entrée standard

`STDOUT` : sortie standard

`STDERR` : sortie 'erreur'

`>` : redirige la sortie standard

```bash
ls -l > /home/pi/resultat
```

> au lieu d'afficher à l'écran le résultat de `ls`, créé ou le remplace un fichier 'resultat' et y insère le retour de `ls`

`>>` : redirige la sortie à la fin du fichier

> contrairement à `>`, la double redirection ne va pas remplacer le fichier si ce dernier existe mais insère le résultat de la commande à la fin du fichier dans modifier le contenu précédent

`2>` ou `2>>`: redirige les erreurs

#### Le pipe

> avec le 'pipe' on peut "rediriger" la sortie `STDOUT` d'une commande vers le `STDIN` d'une autre commande

```bash
pi@rpidemanu:~ $ ls | sort -r
Videos
Templates
Public
Pictures
Music
Downloads
Documents
Desktop
Bookshelf
```

> `ls`renvoie la liste des fichiers/dossiers présents dans le répertoire courant, envoie le résultat vers la commande `sort`qui se charge d'inverser le résultat grâce à l'option `-r`



#### Aller plus loin avec `find`

`-exec` : exécute une commande pour chaque résultat trouvé

```bash
pi@rpidemanu:~ $ find ~/Documents/raspberry-script/ -type f -exec grep -il 'gpio' {} \;
/home/pi/Documents/raspberry-script/fanoff
/home/pi/Documents/raspberry-script/cputemp
/home/pi/Documents/raspberry-script/fanon
```

> `{}`sera remplacé par chaque résultat de `find` 
>
> `;` sert à prévenir la commande `find`que la boucle est terminée. On l'échappe pour éviter que le caractère `;` soit interprété : `\;`



On pourrait utiliser un pipe au lieu d'option `-exec`

```bash
pi@rpidemanu:~ $ find ~/Documents/raspberry-script/ -type f -print0 | xargs -0 grep -il 'gpio'
/home/pi/Documents/raspberry-script/fanoff
/home/pi/Documents/raspberry-script/cputemp
/home/pi/Documents/raspberry-script/fanon
```

> on privilégie la commande `-print0`à `-print`
>
> `xargs`récupère comme argument chaque résultat précédent le pipe (la sortie `STDOUT`)



On pourrait ensuite supprimer les fichiers trouvés par la commande

```bash
pi@rpidemanu:~ $ find ~/Documents/raspberry-script/ -type f -print0 | xargs -0 grep -il 'gpio' | xargs rm
```



#### Compresser et décompresser avec `tar`

```bash
tar -czvf mon-fichier.tar.gz .
```

##### Options

`-c`: créer l'archive

`-t` : afficher le contenu d'une archive

`-z`: utiliser l'algorithme de compression 'gzip'

`-v`: afficher un résultat visuel

`-f` : pour nommer le fichier d'archive

```bash
tar -czvf scripts.tar.gz .
```

> crée une archive 'scripts.tar.gz' à partir des fichiers présents dans le répertoire courant



```bash
tar -tzvf scripts.tar.gz
```

> affiche le contenu de mon archive



```bash
tar -xvzf ../scripts.tar.gz 
```

> décompresse mon archive qui est situé dans le répertoire parent, dans le répertoire courant

---

## Cours 2 : Administration Linux

### RAPPELS

#### Les métacaractères

|         Caractère          |            Interprétation             |
| :------------------------: | :-----------------------------------: |
| Blanc (espace, tabulation) |              Séparateur               |
|             *              |        Joker de nom de fichier        |
|             $              |        Contenu d'une variable         |
|             \              | Protection de caractère (échappement) |
|     'xxx' (apostrophe)     |          Bloc de protection           |



#### Les différents types de fichier

| Symbôle |        Type de fichier        |
| :-----: | :---------------------------: |
|    -    |       Fichier régulier        |
|    d    |          Répertoire           |
|    l    |        Lien symbolique        |
| c ou b  |    Fichiers périphériques     |
|    p    | 'pipe' - fichier de transfert |
|    s    |           'socket'            |



#### L'arborescence de la racine `/`de la machine

```bash
pi@rpidemanu:~ $ ls /
bin   dev  home  lost+found  mnt  proc  run   snap  sys  usr
boot  etc  lib   media       opt  root  sbin  srv   tmp  var
```

`/bin`: programmes essentiels accessibles par l'ensemble des utilisateurs

`/boot`: programmes nécessaires au démarrage de la machine

`/dev`: périphériques

`/etc`: fichiers de configuration système

`/home`: répertoire domicile utilisateur

`/lib`: bibliothèques partagées par les programmes essentiels à la machine

`/media & /mnt`: supports de stockage amovibles

`/opt`: arborescences de fichiers de programme optionnels

`/proc`: représentation des programmes qui s'exécute dans la mémoire, sous forme de fichiers

`/root`: répertoire domicile de l'utilisateur administrateur `root`

`/run`: répertoire de données volatiles qui s'effacent au redémarrage liées à l'exécution des programmes

`/sbin` : idem que `/bin`mais plutôt adressé à l'utilisateur `root`

`/srv`: lié au réseau. Fichiers partagée par les serveurs

`/sys`: évolution du dossier `/proc`

`/tmp` : répertoire temporaire

`/usr`: mis à disposition à tous les utilisateurs

`/var`: fichiers utilisés par les programmes qui tournent en tâche de fond



### LES PAQUETS LOGICIELS

On utilise un gestionnaire de paquet pour mettre à jour, supprimer ou rajouter de nouveaux logiciels.

Les plus connus sont `apt` sur Debian/Ubuntu, `dnf`ou `yum`sur CentOs.



> Toutes modifications sur les paquets installés sur la machine sont des tâches d'administration. Il est nécessaire d'identifier en tant que *Super User* via la commande `sudo`ou `su`si vous connaissez le mot de passe de l'utilisateur `root`



#### Mettre à jour les paquets

```bash
sudo apt update #mets à jour la liste des paquets et leur version
sudo apt upgrade #télécharge et installe les paquets à mettre à jour
```

#### Chercher un paquet

```bash
sudo apt search {paquet_recherché}
```

#### Installer un paquet

```bash
sudo apt install {paquet_à_installer}
```

#### Supprimer un paquet

```bash
sudo apt remove {paquet_à_désinstaller}
```



> Sur certaines distributions, on peut aussi utiliser le gestionnaire `snap`. Certains éditeurs de logiciels préférent ce gestionnaire pour héberger eux-même leurs paquets



#### Installer les logiciels depuis les sources

On lance le programme `configure`qui est présent dans le code source du programme téléchargé. `configure`vérifie que l'ensemble des dépendances nécessaires au programme soient bien installées sur la machine. Sinon, il renvoie la liste des dépendances manquantes.

```bash
sudo ./configure #vérifie les dépendances installées
sudo make #compile le code source
sudo make install #installe le programme sur la machine
```








































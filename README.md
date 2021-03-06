# LINUX

https://github.com/emmanuel-sarpedon/cours-linux

---

## 1. <a name='Tabledesmatires_'></a>_Table des matières_

<!-- vscode-markdown-toc -->

- 1. [_Table des matières_](#Tabledesmatires_)
- 2. [Cours 1 : Les commandes du terminal](#Cours1:Lescommandesduterminal)
  - 2.1. [CREER DES LIENS SYMBOLIQUES](#CREERDESLIENSSYMBOLIQUES)
  - 2.2. [VISUALISER LE CONTENU D'UN FICHIER](#VISUALISERLECONTENUDUNFICHIER)
    - 2.2.1. [Commande `cat`](#Commandecat)
    - 2.2.2. [ Commande `less`](#Commandeless)
    - 2.2.3. [Commande `tail`](#Commandetail)
    - 2.2.4. [Commande `head`](#Commandehead)
    - 2.2.5. [Commande `strings`](#Commandestrings)
  - 2.3. [AFFICHER LES STATS D'UN FICHIER](#AFFICHERLESSTATSDUNFICHIER)
    - 2.3.1. [Commande `stat`](#Commandestat)
    - 2.3.2. [Commande `wc`](#Commandewc)
    - 2.3.3. [Commande `du`](#Commandedu)
    - 2.3.4. [Commande `df`](#Commandedf)
  - 2.4. [MANIPULER LES PERMISSIONS](#MANIPULERLESPERMISSIONS)
    - 2.4.1. [Les permissions](#Lespermissions)
    - 2.4.2. [Commande `chmod`](#Commandechmod)
    - 2.4.3. [Exécuter des commandes en tant que superuser](#Excuterdescommandesentantquesuperuser)
  - 2.5. [EFFECTUER DES RECHERCHES ET AUTRES OPERATIONS](#EFFECTUERDESRECHERCHESETAUTRESOPERATIONS)
    - 2.5.1. [Commande `find`](#Commandefind)
    - 2.5.2. [Commande `grep`](#Commandegrep)
    - 2.5.3. [Le remplacement par "globbing"](#Leremplacementparglobbing)
    - 2.5.4. [La redirection](#Laredirection)
    - 2.5.5. [Le pipe](#Lepipe)
    - 2.5.6. [Aller plus loin avec `find`](#Allerplusloinavecfind)
    - 2.5.7. [Compresser et décompresser avec `tar`](#Compresseretdcompresseravectar)
- 3. [Cours 2 : Administration Linux](#Cours2:AdministrationLinux)
  - 3.1. [RAPPELS](#RAPPELS)
    - 3.1.1. [Les métacaractères](#Lesmtacaractres)
    - 3.1.2. [Les différents types de fichier](#Lesdiffrentstypesdefichier)
    - 3.1.3. [L'arborescence de la racine `/`de la machine](#Larborescencedelaracinedelamachine)
  - 3.2. [LES PAQUETS LOGICIELS](#LESPAQUETSLOGICIELS)
    - 3.2.1. [Mettre à jour les paquets](#Mettrejourlespaquets)
    - 3.2.2. [Chercher un paquet](#Chercherunpaquet)
    - 3.2.3. [Installer un paquet](#Installerunpaquet)
    - 3.2.4. [Supprimer un paquet](#Supprimerunpaquet)
    - 3.2.5. [Installer les logiciels depuis les sources](#Installerleslogicielsdepuislessources)
  - 3.3. [LE STOCKAGE](#LESTOCKAGE)
    - 3.3.1. [Commande `lsblk`](#Commandelsblk)
    - 3.3.2. [Commande `fdisk`](#Commandefdisk)
    - 3.3.3. [Commande `mkfs`](#Commandemkfs)
    - 3.3.4. [Commande `mount`](#Commandemount)
  - 3.4. [LE RESEAU](#LERESEAU)
    - 3.4.1. [Le Network Manager](#LeNetworkManager)
    - 3.4.2. [Les fichiers de configuration](#Lesfichiersdeconfiguration)
  - 3.5. [LES SERVICES](#LESSERVICES)
    - 3.5.1. [Le programme `systemd` via `systemctl`](#Leprogrammesystemdviasystemctl)
    - 3.5.2. [Analyse du temps de démarrage des services](#Analysedutempsdedmarragedesservices)
  - 3.6. [LE GESTIONNAIRE DE LOGS : `syslog`](#LEGESTIONNAIREDELOGS:syslog)
    - 3.6.1. [Configurer `rsyslog`](#Configurerrsyslog)
  - 3.7. [AUTOMATISER LES COMMANDES](#AUTOMATISERLESCOMMANDES)
    - 3.7.1. [Le service `cron`](#Leservicecron)
    - 3.7.2. [Le service `at`](#Leserviceat)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=false
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

---

## 2. <a name='Cours1:Lescommandesduterminal'></a>Cours 1 : Les commandes du terminal

### 2.1. <a name='CREERDESLIENSSYMBOLIQUES'></a>CREER DES LIENS SYMBOLIQUES

```bash
ln -s {fichier ou dossier pointé} {nom_du_lien}
```

### 2.2. <a name='VISUALISERLECONTENUDUNFICHIER'></a>VISUALISER LE CONTENU D'UN FICHIER

#### 2.2.1. <a name='Commandecat'></a>Commande `cat`

```bash
cat {nom_du_fichier}
```

##### Options

`-n`: numéroter les lignes du fichier

`-b`: supprimer les lignes vides

`-s`: regrouper les lignes vides successives en une seule ligne vide

> Le problème de `cat`c'est que l'ensemble du fichier est affiché (pose souci pour les fichiers très longs ... )

#### 2.2.2. <a name='Commandeless'></a> Commande `less`

> La commande `less` lance d'une certaine façon, un éditeur de texte en lecture seule pour lire le fichier et y naviguer, en commançant par le haut du fichier

```bash
less {nom_du_fichier}
```

##### Commandes

`ESPACE` : faire défiler le fichier

`q`: quitter la commande `less`

`f` : _forward_ - pour avancer dans le fichier

`b`: _backward_ - pour revenir en arrière dans le fichier

`/{recherche}`: lancer une recherche

`n`: _next_ - continuer la recherche

#### 2.2.3. <a name='Commandetail'></a>Commande `tail`

> Affiche les 10 dernières lignes du fichier (par défaut)

```bash
tail {nom_du_fichier}
```

##### Options

`-f`: garder le fichier ouvert et affiche en temps réel les modifications

`-n{integer}`: afficher le nombre de ligne passé en paramètre (au lieu des 10 lignes par défaut )

#### 2.2.4. <a name='Commandehead'></a>Commande `head`

> Affiche les 10 premières lignes du fichier (par défaut)

```bash
head {nom_du_fichier}
```

#### 2.2.5. <a name='Commandestrings'></a>Commande `strings`

> Extrait les chaînes de caractère compilés d'un fichier ou même d'un exécutable et les affiche à l'écran

```bash
strings {nom_du_fichier}
```

### 2.3. <a name='AFFICHERLESSTATSDUNFICHIER'></a>AFFICHER LES STATS D'UN FICHIER

#### 2.3.1. <a name='Commandestat'></a>Commande `stat`

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

#### 2.3.2. <a name='Commandewc'></a>Commande `wc`

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

#### 2.3.3. <a name='Commandedu'></a>Commande `du`

> _**D**isk **U**sage_ : affiche une taille en nombre de blocs.. pas très pratique en l'état, on utilisera donc les options ci-dessous

##### Options

`-b`: afficher le nombre d'octets

`-h` : _Human Readable_ - convertir en Ko, Mo, Go, etc.

`-H`: équivalent à `-h`minuscule mais divise les multiples par 1000 et non 1024 octets

`-s` : afficher uniquement le total

#### 2.3.4. <a name='Commandedf'></a>Commande `df`

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

### 2.4. <a name='MANIPULERLESPERMISSIONS'></a>MANIPULER LES PERMISSIONS

```bash
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

#### 2.4.1. <a name='Lespermissions'></a>Les permissions

r : read

w : write

x : execute

Il y a trois blocs :

- Le propriétaire
- Le groupe propriétaire
- Tout le monde

#### 2.4.2. <a name='Commandechmod'></a>Commande `chmod`

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

#### 2.4.3. <a name='Excuterdescommandesentantquesuperuser'></a>Exécuter des commandes en tant que superuser

`sudo` : _Super User Do_ : exécute une commande en tant que superutilisateur

`sudo su` : permet de rester superutilisateur pendant un laps de temps déterminé par le système

### 2.5. <a name='EFFECTUERDESRECHERCHESETAUTRESOPERATIONS'></a>EFFECTUER DES RECHERCHES ET AUTRES OPERATIONS

#### 2.5.1. <a name='Commandefind'></a>Commande `find`

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

> ci-dessus, on recherche tous les fichiers qui ont été accédé depuis **1** jour

`-ctime` : recherche le(s) fichiers **c**hangé(s) depuis x _jours_

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

#### 2.5.2. <a name='Commandegrep'></a>Commande `grep`

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

#### 2.5.3. <a name='Leremplacementparglobbing'></a>Le remplacement par "globbing"

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

#### 2.5.4. <a name='Laredirection'></a>La redirection

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

#### 2.5.5. <a name='Lepipe'></a>Le pipe

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

#### 2.5.6. <a name='Allerplusloinavecfind'></a>Aller plus loin avec `find`

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

> On privilégie la commande `-print0`à `-print`
>
> `xargs`récupère comme argument chaque résultat précédent le pipe (la sortie `STDOUT`)

On pourrait ensuite supprimer les fichiers trouvés par la commande

```bash
pi@rpidemanu:~ $ find ~/Documents/raspberry-script/ -type f -print0 | xargs -0 grep -il 'gpio' | xargs rm
```

#### 2.5.7. <a name='Compresseretdcompresseravectar'></a>Compresser et décompresser avec `tar`

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

## 3. <a name='Cours2:AdministrationLinux'></a>Cours 2 : Administration Linux

### 3.1. <a name='RAPPELS'></a>RAPPELS

#### 3.1.1. <a name='Lesmtacaractres'></a>Les métacaractères

|         Caractère          |            Interprétation             |
| :------------------------: | :-----------------------------------: |
| Blanc (espace, tabulation) |              Séparateur               |
|             \*             |        Joker de nom de fichier        |
|             $              |        Contenu d'une variable         |
|             \              | Protection de caractère (échappement) |
|     'xxx' (apostrophe)     |          Bloc de protection           |

#### 3.1.2. <a name='Lesdiffrentstypesdefichier'></a>Les différents types de fichier

| Symbôle |        Type de fichier        |
| :-----: | :---------------------------: |
|    -    |       Fichier régulier        |
|    d    |          Répertoire           |
|    l    |        Lien symbolique        |
| c ou b  |    Fichiers périphériques     |
|    p    | 'pipe' - fichier de transfert |
|    s    |           'socket'            |

#### 3.1.3. <a name='Larborescencedelaracinedelamachine'></a>L'arborescence de la racine `/`de la machine

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

### 3.2. <a name='LESPAQUETSLOGICIELS'></a>LES PAQUETS LOGICIELS

On utilise un gestionnaire de paquet pour mettre à jour, supprimer ou rajouter de nouveaux logiciels.

Les plus connus sont `apt` sur Debian/Ubuntu, `dnf`ou `yum`sur CentOs.

> Toutes modifications sur les paquets installés sur la machine sont des tâches d'administration. Il est nécessaire d'identifier en tant que _Super User_ via la commande `sudo`ou `su`si vous connaissez le mot de passe de l'utilisateur `root`

#### 3.2.1. <a name='Mettrejourlespaquets'></a>Mettre à jour les paquets

```bash
sudo apt update #mets à jour la liste des paquets et leur version
sudo apt upgrade #télécharge et installe les paquets à mettre à jour
```

#### 3.2.2. <a name='Chercherunpaquet'></a>Chercher un paquet

```bash
sudo apt search {paquet_recherché}
```

#### 3.2.3. <a name='Installerunpaquet'></a>Installer un paquet

```bash
sudo apt install {paquet_à_installer}
```

#### 3.2.4. <a name='Supprimerunpaquet'></a>Supprimer un paquet

```bash
sudo apt remove {paquet_à_désinstaller}
```

> Sur certaines distributions, on peut aussi utiliser le gestionnaire `snap`. Certains éditeurs de logiciels préférent ce gestionnaire pour héberger eux-même leurs paquets

#### 3.2.5. <a name='Installerleslogicielsdepuislessources'></a>Installer les logiciels depuis les sources

On lance le programme `configure`qui est présent dans le code source du programme téléchargé. `configure`vérifie que l'ensemble des dépendances nécessaires au programme soient bien installées sur la machine. Sinon, il renvoie la liste des dépendances manquantes.

```bash
sudo ./configure #vérifie les dépendances installées
sudo make #compile le code source
sudo make install #installe le programme sur la machine
```

### 3.3. <a name='LESTOCKAGE'></a>LE STOCKAGE

#### 3.3.1. <a name='Commandelsblk'></a>Commande `lsblk`

> Liste l'ensemble des périphériques de stockage

```bash
pi@rpidemanu:/dev $ lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
mmcblk0     179:0    0 14,9G  0 disk
├─mmcblk0p1 179:1    0  256M  0 part /boot
└─mmcblk0p2 179:2    0 14,6G  0 part /
```

#### 3.3.2. <a name='Commandefdisk'></a>Commande `fdisk`

> Utilitaire pour partionner son disque dur

```bash
pi@rpidemanu:/dev $ sudo fdisk /dev/mmcblk0

Welcome to fdisk (util-linux 2.33.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help):
```

##### Commandes

`m`: affiche l'aide

```bash
Help:

  DOS (MBR)
   a   toggle a bootable flag
   b   edit nested BSD disklabel
   c   toggle the dos compatibility flag

  Generic
   d   delete a partition
   F   list free unpartitioned space
   [...]
```

`p` : affiche l'état actuel de la table de partition (print)

```bash
Disk /dev/mmcblk0: 14,9 GiB, 15931539456 bytes, 31116288 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x41349f83

Device         Boot  Start      End  Sectors  Size Id Type
/dev/mmcblk0p1        8192   532479   524288  256M  c W95 FAT32 (LBA)
/dev/mmcblk0p2      532480 31116287 30583808 14,6G 83 Linux
```

`n`: ajoute une partition (new)

```bash
Command (m for help): n
Partition type
   p   primary (2 primary, 0 extended, 2 free)
   e   extended (container for logical partitions)
Select (default p): p # 1 - le type de partition
Partition number (3,4, default 3): # 2 - le numéro de la partition (laissez vide pour garder la valeur par défaut)
First sector (2048-31116287, default 2048): # 3 - le secteur où ma partition doit commencer (laissez vide pour garder la valeur par défaut)
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-8191, default 8191): +1M # 4 - la taille de la partition

Created a new partition 3 of type 'Linux' and of size 1 MiB.
```

Voici la nouvelle table de partition :

```bash
Device         Boot  Start      End  Sectors  Size Id Type
/dev/mmcblk0p1        8192   532479   524288  256M  c W95 FAT32 (LBA)
/dev/mmcblk0p2      532480 31116287 30583808 14,6G 83 Linux
/dev/mmcblk0p3        2048     4095     2048    1M 83 Linux
```

`t`: modifier le type de partition (type)

```bash
Command (m for help): t
Partition number (1-3, default 3):
Hex code (type L to list all codes): 82

Changed type of partition 'Linux' to 'Linux swap / Solaris'.
```

> Tous les changements opérés sont enregistrés en mémoire mais ne sont pas encore réellement pris en compte par nos disques. Il faut maintenant enregistrer nos changements avec la commande ci-après

`w`: sauvegarder nos changements (write)

```bash
Command (m for help): w
The partition table has been altered.
Syncing disks.
```

Si je relance la commande `lsblk`, ma partition est cette fois présente

```bash
pi@rpidemanu:/dev $ lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
mmcblk0     179:0    0 14,9G  0 disk
├─mmcblk0p1 179:1    0  256M  0 part /boot
├─mmcblk0p2 179:2    0 14,6G  0 part /
└─mmcblk0p3 179:3    0    1M  0 part
```

`g` : transforme une table de partitions `DOS`en table de partitions `GPT`

> Le format `DOS` ne sait pas gérer les partitions et disques d'une taille > 2To. Pour cette raison, nous devons utiliser dans certains cas le format `GPT`

```bash
Command (m for help): g
Created a new GPT disklabel (GUID: 56935816-52FA-5B4C-80B8-2182DEB1B8D7).
The old dos signature will be removed by a write command.

Command (m for help): p

Disk /dev/mmcblk0: 14,9 GiB, 15931539456 bytes, 31116288 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 56935816-52FA-5B4C-80B8-2182DEB1B8D7
```

> Le concept de partitons primaires et élémentaires n'existent plus sous le format `GPT`. La seule limitation est celle du nombre de partitions possible qui est de 128

#### 3.3.3. <a name='Commandemkfs'></a>Commande `mkfs`

> Créer un système de fichier

```bash
sudo mkfs -t {type} {volume}
```

```bash
pi@rpidemanu:/dev $ sudo mkfs -t ext4 /dev/mmcblk0p3
mke2fs 1.44.5 (15-Dec-2018)

Filesystem too small for a journal
Discarding device blocks: done
Creating filesystem with 1024 1k blocks and 128 inodes

Allocating group tables: done
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
```

> Il existe le format ext4, xfs, et d'autres

#### 3.3.4. <a name='Commandemount'></a>Commande `mount`

> Monter un périphérique de stockage ou une partition sur un répertoire

```bash
sudo mount {partition_à_monter} {cible}
```

```bash
pi@rpidemanu:/ $ sudo mount /dev/mmcblk0p3 /data-test/
```

Maintenant, toutes les données enregistrées sur `/data-test`seront aussi enregistrées dans ma partition `/mmcblk0p3`

> Le montage n'est pas conservé après un redémarrage. Pour que le montage se fasse à chaque démarrage, il faut modifier le fichier `/etc/fstab`

```bash
GNU nano 3.2                            /etc/fstab

proc            /proc           proc    defaults          0       0
PARTUUID=41349f83-01  /boot           vfat    defaults          0       2
PARTUUID=41349f83-02  /               ext4    defaults,noatime  0       1
/dev/mmcblk0p3        /data-test      ext4    defaults        0 0
# a swapfile is not a swap partition, no line here
#   use  dphys-swapfile swap[on|off]  for that

```

Si on relance la commande `lsblk`, on remarque que ma partition est montée dans le répertoire `/data-test`

```bash
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
mmcblk0     179:0    0 14,9G  0 disk
├─mmcblk0p1 179:1    0  256M  0 part /boot
├─mmcblk0p2 179:2    0 14,6G  0 part /
└─mmcblk0p3 179:3    0    1M  0 part /data-test
```

### 3.4. <a name='LERESEAU'></a>LE RESEAU

#### 3.4.1. <a name='LeNetworkManager'></a>Le Network Manager

```bash
pi@rpidemanu:/etc/network $ systemctl status NetworkManager
● NetworkManager.service - Network Manager
   Loaded: loaded (/lib/systemd/system/NetworkManager.service; enabled; vendor preset: ena
   Active: active (running) since Tue 2021-08-31 14:31:57 +04; 1h 10min ago
     Docs: man:NetworkManager(8)
 Main PID: 3738 (NetworkManager)
    Tasks: 3 (limit: 4915)
   CGroup: /system.slice/NetworkManager.service
           └─3738 /usr/sbin/NetworkManager --no-daemon

août 31 14:32:42 rpidemanu NetworkManager[3738]: <error> [1630405962.5830] sup-iface[0x127
août 31 14:32:42 rpidemanu NetworkManager[3738]: <info>  [1630405962.5832] device (wlan0):
août 31 14:32:53 rpidemanu NetworkManager[3738]: <warn>  [1630405973.2474] device (wlan0):
août 31 14:32:53 rpidemanu NetworkManager[3738]: <error> [1630405973.5337] sup-iface[0x127
août 31 14:32:53 rpidemanu NetworkManager[3738]: <info>  [1630405973.5339] device (wlan0):
août 31 14:32:53 rpidemanu NetworkManager[3738]: <info>  [1630405973.5340] device (wlan0):
août 31 14:44:26 rpidemanu NetworkManager[3738]: <info>  [1630406666.8182] agent-manager:
août 31 14:44:26 rpidemanu NetworkManager[3738]: <info>  [1630406666.8401] audit: op="conn
août 31 14:44:39 rpidemanu NetworkManager[3738]: <info>  [1630406679.9556] agent-manager:
août 31 14:44:39 rpidemanu NetworkManager[3738]: <info>  [1630406679.9657] audit: op="conn
lines 1-19/19 (END)
```

##### Commande `nmtui`

> **N**etwork **M**anager **T**ext **U**ser **I**nterface = gestionnaire de réseau avec interface en mode texte

![nmtui-screenshot](https://res.cloudinary.com/manu-sarp/image/upload/v1630410690/screenshots/nmtui_bxjnyn.png)

##### Commande `nmcli`

> **N**etwork **M**anager **C**ommand **L**ine **I**nterface = gestionnaire de réseau en ligne de commandes

```bash
pi@rpidemanu:/etc/network $ nmcli connection show
NAME                 UUID                                  TYPE      DEVICE
Connexion filaire 1  cf521997-c08a-3968-91c9-c9a693ef2340  ethernet  --
```

#### 3.4.2. <a name='Lesfichiersdeconfiguration'></a>Les fichiers de configuration

> Sous Debian, le fichier de configuration réseau se trouve dans `/etc/network/interfaces`

### 3.5. <a name='LESSERVICES'></a>LES SERVICES

> Un 'daemon' ou service est un programme qui s'exécute indépendamment de l'utilisateur et en tâche de fond

#### 3.5.1. <a name='Leprogrammesystemdviasystemctl'></a>Le programme `systemd` via `systemctl`

> C'est une pièce maîtresse de l'architecture [GNU](https://doc.ubuntu-fr.org/gnu)/[Linux](https://doc.ubuntu-fr.org/linux). En effet, c'est le premier programme lancé par le noyau (il a donc le PID N°1) et il se charge de lancer tous les programmes suivants en ordre jusqu'à obtenir un système opérationnel pour l'utilisateur, selon le mode déterminé (single user, multi-user, graphique). C'est également à lui qu'incombe la tache de redémarrer ou arrêter votre ordinateur proprement. [SOURCE: https://doc.ubuntu-fr.org/systemd]

On utilisera l'interface `systemctl` pour communiquer avec `systemd`

```bash
pi@rpidemanu:~ $ systemctl -t service
UNIT                                       LOAD   ACTIVE SUB     DESCRIPTION
alsa-restore.service                       loaded active exited  Save/Restore Sound Card [...]
```

##### Commandes `systemctl`

Pour savoir si un service est en train de tourner

```bash
systemctl is-active {service}
```

```bash
pi@rpidemanu:~ $ systemctl is-active alsa-state.service
active
pi@rpidemanu:~ $ systemctl is-active httpd
inactive
```

Pour connaître l'état d'un service

```bash
systemctl status {service}
```

```bash
pi@rpidemanu:~ $ systemctl status alsa-state.service
● alsa-state.service - Manage Sound Card State (restore and store)
   Loaded: loaded (/lib/systemd/system/alsa-state.service; static; vendor preset: enabled)
   Active: active (running) since Tue 2021-08-31 14:12:41 +04; 20h ago
     Docs: man:alsactl(1)
 Main PID: 389 (alsactl)
    Tasks: 1 (limit: 4915)
   CGroup: /system.slice/alsa-state.service
           └─389 /usr/sbin/alsactl -E HOME=/run/alsa -s -n 19 -c rdaemon

août 31 14:12:41 rpidemanu systemd[1]: Started Manage Sound Card State (restore and store).
août 31 14:12:41 rpidemanu alsactl[389]: alsactl 1.1.8 daemon started
```

Pour **arrêter** un service

```bash
systemctl stop {service}
```

Pour **démarrer** un service

```bash
systemctl start {service}
```

Pour **redémarrer** un service

```bash
systemctl restart {service}
```

Pour **empêcher** un service de démarrer en même temps que le boot de la machine

```bash
systemctl disable {service}
```

Pour **permettre** un service de démarrer en même temps que le boot de la machine

```bash
systemctl enable {service}
```

Pour **connaître** l'état du système

```bash
systemctl is-system-running
```

Pour identifier le(s) système(s) qui pose(ent) problème

```bash
systemctl --failed
```

Pour remettre le système dans son état normal malgré un service en échec (dans le cas où l'administrateur estime que le service n'est pas critique)

```bash
systemctl reset-failed
```

#### 3.5.2. <a name='Analysedutempsdedmarragedesservices'></a>Analyse du temps de démarrage des services

```bash
pi@rpidemanu:~ $ systemd-analyze
Startup finished in 2.420s (kernel) + 8.269s (userspace) = 10.690s
graphical.target reached after 8.184s in userspace
```

Pour avoir le détail du temps de démarrage de chaque service

```bash
pi@rpidemanu:~ $ systemd-analyze blame
         31.376s apt-daily.service
         31.343s apt-daily-upgrade.service
          2.522s man-db.service
          2.193s dev-mmcblk0p2.device
          2.155s udisks2.service
          1.881s logrotate.service
          1.699s rpi-eeprom-update.service
          1.588s snapd.service
           801ms lightdm.service
           754ms dphys-swapfile.service
           736ms plymouth-quit-wait.service
          [...]
```

Pour un affichage graphique

```bash
pi@rpidemanu:~ $ systemd-analyze plot > boot.svg
```

> Noter la redirection vers un fichier
>
> La commande `plot` va générer un SVG inutilisable si on l'affiche sur la sortie standard, raison pour laquelle on demande la création d'un fichier

### 3.6. <a name='LEGESTIONNAIREDELOGS:syslog'></a>LE GESTIONNAIRE DE LOGS : `syslog`

`Syslog` est un canal de communication pour les programmes et les services n'utilisant pas le terminal et donc ne pouvant pas envoyer des informations dans la sortie standard.

En fonction de l'importance et de la gravité du message, on choisira soit d'enregistrer le log dans un fichier ou de l'afficher dans le terminal d'un utilisateur connecté, par l'intermédiaire d'un programme tiers comme `rsyslog`

Les critères de sélection dépendant de la structure des messages :

- 1- Horodatage
- 2- Provenance : _kernel, user, mail, daemon, syslog, lp, ntp, uucp, ftp, etc._

- 3- Importance : _par ordre d'importance_

  - debug
  - info
  - notice
  - warn : attention
  - err : erreur
  - crit : erreur critique
  - alert : alerte
  - emerg : urgent

- 4- Message

#### 3.6.1. <a name='Configurerrsyslog'></a>Configurer `rsyslog`

Dans la plupart des distribution, le fichier de configuration se trouve dans le répertoire `/etc/rsyslog.conf`

On s'intéressera à la partie du fichier qui se nomme `#### RULES ####`

```bash
###############
#### RULES ####
###############

#
# First some standard log files.  Log by facility.
#
#PROVENANCE.IMPORTANCE			DESTINATION
auth,authpriv.*                 /var/log/auth.log
*.*;auth,authpriv.none          -/var/log/syslog
#cron.*                         /var/log/cron.log
daemon.*                        -/var/log/daemon.log
kern.*                          -/var/log/kern.log
lpr.*                           -/var/log/lpr.log
mail.*                          -/var/log/mail.log
user.*                          -/var/log/user.log

#
# Logging for the mail system.  Split it up so that
# it is easy to write scripts to parse these files.
#
mail.info                       -/var/log/mail.info
mail.warn                       -/var/log/mail.warn
mail.err                        /var/log/mail.err

[...]
```

|     Définition des règles de sélection     |                                                       Explication                                                       |
| :----------------------------------------: | :---------------------------------------------------------------------------------------------------------------------: |
|                  `mail.*`                  |                                       Provenance : `mail`, Importance: quelconque                                       |
|                 `mail.err`                 |                                        Provenance : `mail`, Importance: >= `err`                                        |
| `*.info;mail.none;authpriv.none;cron.none` | Tous les messages dont l'importance est `info` ou supérieur, sauf les messages provenant de `mail`, `authpriv` et`cron` |

> Pour que le système prend en compte la modification du fichier de configuration de `rsyslog`, il faudra redémarrer le service
>
> `systemctl restart rsyslog`

### 3.7. <a name='AUTOMATISERLESCOMMANDES'></a>AUTOMATISER LES COMMANDES

#### 3.7.1. <a name='Leservicecron'></a>Le service `cron`

Le service `cron` nous permet d'automatiser cette tâche périodique (tous les jours, toutes les heures, tous les 20 du mois, tous les dimanches, etc.)

On peut interdire ou autoriser les utilisateurs d'utiliser `cron`

##### Configurer les permissions

Pour interdire un ou plusieurs d'utilisateur d'utiliser le service `cron`, il faut créer un fichier `cron.deny` dans le répertoire `/etc/` et y insérer la liste des utilisateurs concernés.

A contrario, pour autoriser un ou plusieurs d'utilisateur d'utiliser le service `cron`, il faut créer un fichier `cron.allow` dans le répertoire `/etc/` et y insérer la liste des utilisateurs concernés.

> Attention, si le fichier `cron.allow` est existant, seul les utilisateurs présents dans cette liste seront autorisés à utiliser le service `cron` mais s'ils ne sont pas présents dans le fichier `cron.deny`

##### Commande `crontab`

La commande `crontab` nous permet de programmer des tâches

`-l` : liste les programmations pour l'utilisateur courant

```bash
pi@rpidemanu:~ $ crontab -l
no crontab for pi
```

`-r` : supprime tous les programmations pour l'utilisateur courant

`-e` : lance l'édition de la `crontab` pour l'utilisateur courant

Pour programmer une tâche, on doit respecter le pattern ci-dessous :

| minute | heure | jour du mois | mois | jour de la semaine | tâche à exécuter |
| :----: | :---: | :----------: | :--: | :----------------: | :--------------: |

> Pour les jours de la semaine, dimanche correspond à 0, lundi à 1, mardi à 2, etc...
>
> Si on précise le jour de la semaine, on ne peut pas préciser le jours du mois, ni le mois (et vice-versa)

Par exemple, le code ci-dessous lancera une mise à jour de la liste des paquets toutes les 30 minutes :

```bash
30 * * * * sudo apt update
```

On peut séparer plusieurs valeurs par une virgule `,`. Cette tâche se lancera toutes les 30 et 45 min de chaque heure (12h30, 12h45 ; 13h30, 13h45; etc...).

```b
30,45 * * * * sudo apt update
```

On peut lancer une tâche toutes les 2 heures

```bash
* */2 * * * sudo apt update
```

#### 3.7.2. <a name='Leserviceat'></a>Le service `at`

Le service `at` nous permet de programmer une tâche à exécuter une seule fois (pas de périodicité - le cas échéant on utilisera `cron`)

```bash
pi@rpidemanu:~ $ at 14:30 #1 - on programme une tâche à 14h30
warning: commands will be executed using /bin/sh
at> sudo reboot #2 - on tape la commande à exécuter à 14h30 (ici redémarrage du système)
at> <EOT> #3 - pour terminer on utilise la combinaise de touche CTRL + D (ou CMD + D sur Mac)
job 1 at Wed Sep  1 14:30:00 2021 #4 - confirmation
```

Pour les lister les "jobs" ou tâches à venir : `atq`

```bash
pi@rpidemanu:~ $ atq
2       Wed Sep  1 15:00:00 2021 a pi
```

Pour supprimer une tâche : `atrm {numero_du_job}`

```bash
pi@rpidemanu:~ $ atrm 2
```

Quelques commandes supplémentaires

```bash
pi@rpidemanu:~ $ at 14:00 010122 #Le 01 janvier 2022, à 14heures

pi@rpidemanu:~ $ at midnight 	 #A minuit

pi@rpidemanu:~ $ at noon		 #A midi

pi@rpidemanu:~ $ at teatime		 #A l'heure du thé (dépend de la configuration de la machine)

pi@rpidemanu:~ $ at now + 5min	 #Dans 5 minutes

pi@rpidemanu:~ $ at now + 2days	 #Dans 2 jours
```

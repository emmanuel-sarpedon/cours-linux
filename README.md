# Linux

---

## Cours 1 : Les commandes du terminal

### - Créer des liens symboliques (équivalent aux raccourcis)

```bash
ln -s {fichier ou dossier pointé} {nom_du_lien}
```



### - Visualiser le contenu d'un fichier

#### Commande `cat`

```bash
cat {nom_du_fichier}
```

##### Options :

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



### - Afficher les statistiques d'un fichier ou d'un répertoire

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



### - Manipuler les permissions et propriétaires

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



### - Effectuer une recherche avec la commande `find`


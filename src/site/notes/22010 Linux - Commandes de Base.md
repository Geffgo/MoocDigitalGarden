---
{"dg-publish":true,"permalink":"/22010-linux-commandes-de-base/"}
---

# Linux - Commandes de Base
# Fiches Liées
- [[Accueil\|Accueil]]
---
## Navigation et exploration

|Commande|Description|Options principales|Exemples|
|---|---|---|---|
|`pwd`|Affiche le répertoire courant|-|`pwd`|
|`ls`|Liste le contenu d'un répertoire|`-l` (long), `-a` (cachés), `-h` (lisible), `-R` (récursif)|`ls -la`, `ls -lh`|
|`cd`|Change de répertoire|-|`cd ~`, `cd ..`, `cd -`|
|`find`|Recherche de fichiers|`-name`, `-type`, `-size`|`find /path -name "*.txt"`|
|`locate`|Recherche rapide dans base de données|`-i` (insensible casse)|`locate filename`|
|`which`|Localise une commande|-|`which python`|
|`whereis`|Localise binaires, sources, manuels|-|`whereis gcc`|

## Manipulation de fichiers et répertoires

|Commande|Description|Options principales|Exemples|
|---|---|---|---|
|`touch`|Crée un fichier vide ou met à jour la date|-|`touch file.txt`|
|`mkdir`|Crée un répertoire|`-p` (parents manquants)|`mkdir -p /path/to/dir`|
|`rmdir`|Supprime un répertoire vide|-|`rmdir emptydir`|
|`rm`|Supprime des fichiers|`-r` (récursif), `-f` (force)|`rm -rf directory/`|
|`cp`|Copie des fichiers|`-r` (récursif), `-p` (préserve attributs)|`cp -r dir1 dir2`|
|`mv`|Déplace/renomme des fichiers|-|`mv file1 file2`|
|`ln`|Crée des liens|`-s` (symbolique)|`ln -s target link`|
|`rsync`|Synchronisation avancée|`-a` (archive), `-v` (verbose)|`rsync -av source/ dest/`|

## Visualisation et édition de fichiers

|Commande|Description|Options principales|Exemples|
|---|---|---|---|
|`cat`|Affiche le contenu complet|`-n` (numéroter lignes)|`cat file.txt`|
|`less`|Affichage paginé avec navigation|-|`less file.txt`|
|`more`|Affichage paginé simple|-|`more file.txt`|
|`head`|Affiche les premières lignes|`-n` (nombre de lignes)|`head -n 20 file.txt`|
|`tail`|Affiche les dernières lignes|`-f` (suivi temps réel), `-n` (nombre)|`tail -f /var/log/syslog`|
|`nano`|Éditeur simple|-|`nano file.txt`|
|`vim`|Éditeur avancé|-|`vim file.txt`|

## Recherche et filtrage

|Commande|Description|Options principales|Exemples|
|---|---|---|---|
|`grep`|Recherche de motifs|`-i` (insensible casse), `-r` (récursif), `-n` (numéros), `-v` (inverser)|`grep -i "pattern" file.txt`|
|`sort`|Trie les lignes|`-n` (numérique), `-r` (inverse)|`sort -n numbers.txt`|
|`uniq`|Supprime les doublons|`-c` (compte occurrences)|`sort file.txt|
|`cut`|Extrait des colonnes|`-d` (délimiteur), `-f` (champs)|`cut -d: -f1 /etc/passwd`|
|`awk`|Traitement de texte avancé|-|`awk '{print $1}' file.txt`|
|`sed`|Édition de flux|`s/old/new/g` (substitution)|`sed 's/old/new/g' file.txt`|

## Gestion des permissions

|Commande|Description|Options principales|Exemples|
|---|---|---|---|
|`chmod`|Change les permissions|`-R` (récursif)|`chmod 755 file`, `chmod +x script.sh`|
|`chown`|Change le propriétaire|`-R` (récursif)|`chown user:group file`|
|`chgrp`|Change le groupe|`-R` (récursif)|`chgrp group file`|
|`umask`|Masque de permissions par défaut|-|`umask 022`|

### Valeurs numériques des permissions

|Valeur|Permissions|Signification|
|---|---|---|
|7|rwx|Lecture, écriture, exécution|
|6|rw-|Lecture, écriture|
|5|r-x|Lecture, exécution|
|4|r--|Lecture seule|
|3|-wx|Écriture, exécution|
|2|-w-|Écriture seule|
|1|--x|Exécution seule|
|0|---|Aucune permission|

## Gestion des processus

|Commande|Description|Options principales|Exemples|
|---|---|---|---|
|`ps`|Liste les processus|`aux` (tous détaillés), `-ef` (format complet)|`ps aux`|
|`top`|Processus en temps réel|-|`top`|
|`htop`|Version améliorée de top|-|`htop`|
|`pgrep`|Trouve des processus par nom|-|`pgrep apache`|
|`pidof`|PID d'un processus|-|`pidof firefox`|
|`kill`|Termine un processus|`-9` (brutal), `-15` (propre)|`kill -9 1234`|
|`killall`|Termine par nom|-|`killall firefox`|
|`pkill`|Termine par motif|-|`pkill -f "python script"`|
|`jobs`|Liste les tâches actives|-|`jobs`|
|`bg`|Met une tâche en arrière-plan|-|`bg %1`|
|`fg`|Ramène une tâche au premier plan|-|`fg %1`|
|`nohup`|Exécute sans accrochage au terminal|-|`nohup command &`|

## Archivage et compression

|Commande|Description|Options principales|Exemples|
|---|---|---|---|
|`tar`|Archivage de fichiers|`-c` (créer), `-x` (extraire), `-v` (verbose), `-f` (fichier), `-z` (gzip)|`tar -czvf archive.tar.gz files/`|
|`gzip`|Compression gzip|`-d` (décompresse)|`gzip file.txt`|
|`gunzip`|Décompression gzip|-|`gunzip file.txt.gz`|
|`zip`|Compression zip|`-r` (récursif)|`zip -r archive.zip files/`|
|`unzip`|Décompression zip|-|`unzip archive.zip`|

### Options tar courantes

|Option|Description|
|---|---|
|`-c`|Créer une archive|
|`-x`|Extraire une archive|
|`-t`|Lister le contenu|
|`-v`|Mode verbose|
|`-f`|Spécifier le fichier|
|`-z`|Compression gzip|
|`-j`|Compression bzip2|

## Redirection et tubes

|Opérateur|Description|Exemples|
|---|---|---|
|`>`|Redirection de sortie (écrase)|`command > file.txt`|
|`>>`|Redirection de sortie (ajoute)|`command >> file.txt`|
|`<`|Redirection d'entrée|`command < input.txt`|
|`2>`|Redirection d'erreur|`command 2> error.log`|
|`&>`|Redirection sortie et erreur|`command &> output.log`|
|`|`|Tube (pipe)|
|`tee`|Écrit dans fichier et stdout|`command|

## Gestion du système

|Commande|Description|Options principales|Exemples|
|---|---|---|---|
|`uname`|Informations système|`-a` (tout), `-r` (kernel)|`uname -a`|
|`whoami`|Utilisateur actuel|-|`whoami`|
|`id`|Identité utilisateur|-|`id`|
|`groups`|Groupes de l'utilisateur|-|`groups`|
|`uptime`|Durée de fonctionnement|-|`uptime`|
|`date`|Date et heure|`+%Y-%m-%d` (format)|`date +%Y-%m-%d`|
|`cal`|Calendrier|-|`cal`|
|`df`|Espace disque des systèmes|`-h` (lisible)|`df -h`|
|`du`|Utilisation de l'espace|`-h` (lisible), `-s` (résumé)|`du -sh /path`|
|`free`|Mémoire disponible|`-h` (lisible)|`free -h`|
|`lscpu`|Informations CPU|-|`lscpu`|
|`lsblk`|Périphériques de bloc|-|`lsblk`|

## Gestion des utilisateurs

|Commande|Description|Options principales|Exemples|
|---|---|---|---|
|`su`|Changer d'utilisateur|`-` (environnement complet)|`su -`|
|`sudo`|Exécuter en tant qu'autre utilisateur|`-u` (utilisateur)|`sudo command`|
|`passwd`|Changer le mot de passe|-|`passwd`|
|`who`|Utilisateurs connectés|-|`who`|
|`w`|Utilisateurs et leur activité|-|`w`|
|`last`|Historique des connexions|-|`last`|
|`finger`|Informations utilisateur|-|`finger user`|

## Variables d'environnement

|Commande|Description|Exemples|
|---|---|---|
|`env`|Affiche toutes les variables|`env`|
|`echo $VAR`|Affiche une variable|`echo $HOME`|
|`export VAR=value`|Définit une variable|`export PATH=$PATH:/new/path`|
|`unset VAR`|Supprime une variable|`unset TEMP_VAR`|
|`set`|Variables du shell|`set`|

### Variables importantes

|Variable|Description|
|---|---|
|`$HOME`|Répertoire personnel|
|`$PATH`|Chemins des commandes|
|`$USER`|Nom d'utilisateur|
|`$PWD`|Répertoire courant|
|`$SHELL`|Shell actuel|
|`$PS1`|Invite de commande|

## Historique et alias

|Commande|Description|Exemples|
|---|---|---|
|`history`|Affiche l'historique|`history`|
|`!n`|Exécute la commande n|`!42`|
|`!!`|Répète la dernière commande|`!!`|
|`!string`|Dernière commande commençant par string|`!ls`|
|`alias`|Affiche/crée des alias|`alias ll='ls -la'`|
|`unalias`|Supprime un alias|`unalias ll`|

## Aide et documentation

|Commande|Description|Options principales|Exemples|
|---|---|---|---|
|`man`|Manuel des commandes|`-k` (mot-clé)|`man ls`|
|`info`|Documentation GNU|-|`info gcc`|
|`whatis`|Description courte|-|`whatis ls`|
|`apropos`|Recherche dans les descriptions|-|`apropos copy`|
|`command --help`|Aide de la commande|-|`ls --help`|
|`help`|Aide des commandes intégrées|-|`help cd`|

## Raccourcis clavier utiles

|Raccourci|Description|
|---|---|
|`Ctrl+C`|Interrompt la commande courante|
|`Ctrl+D`|Fin de fichier / Déconnexion|
|`Ctrl+Z`|Suspend la commande courante|
|`Ctrl+L`|Efface l'écran|
|`Ctrl+R`|Recherche dans l'historique|
|`Ctrl+A`|Début de ligne|
|`Ctrl+E`|Fin de ligne|
|`Ctrl+U`|Efface du curseur au début|
|`Ctrl+K`|Efface du curseur à la fin|
|`Tab`|Autocomplétion|
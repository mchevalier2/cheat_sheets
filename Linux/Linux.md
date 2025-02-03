---
title: "Linux cheat sheet"
author: "Manuel"
date: "2025-02-03"
output:
  html_document:
      toc: true
      toc_float: true
---

## Naviguer sous Linux
* `whoami` —> palaeosaurus
* `pwd` —> print working directory
* `ls (-a)` —> list tous les fichiers dispo (inclue les fichiers cachés)
* `ls -h` donne la taille des fichiers en format lisible
* `ls -lt` —> trier par date de modif
* `ls -lS` —> trier par taille
* `touch filename` —> create an empty file, modifie le timestamp as well
* `touch file{1..42}` will create 42 files called file1, file2, …, file42
* `cd` —> change directory (cd ..  —>  returns to the previous folder)
* `useradd` —> create a user


## Manipulation de fichiers et dossiers
* `echo ‘hello’ > est.txt` will write to est.txt. The single > overwrite the fichier
* `echo ‘hello’ >> est.text` . The double >> adds to existing files
* `rm remove files` (irréversibles)
* `rm file -i` (asks for confirmation)
* `mkdir test_folder`
* `mkdir -p folder/subfolder`
* `rm -r folder`
* `cp file address`
* `cp -r folder address`
* `mv file/folder address`


## Exécuter un script
* `which bash` —> Tells where bash is. This can be added at the beginning of scripts
* `which python*`
* `ls -la | grep script`
* `chmod +x script.sh` —> everybody can use the script
* `chmod -x script.sh`
* `chmod u+x script.sh` —> Only the user can use the script
* `ls /usr/bin.python*` —> list tous les pythons disponibles
* `#! /usr/bin/python3` —> if added at the beginning, makes the script executable with python 3


## Environnements
* `ls > /dev/null` —> redirige the STDOUT vers le vide intersidéral
* `ls -w 1> /devl/null` —> strictement equivalent. Renvoie le STDOUT. Le flag w n’existe pas sous linux, mais ici ne crée pas d’erreur
* `ls -w 2> /dev/nill` —> renvoie le STDERR


## Utilitaires
* `history`
* `ping www.google.com`
* `zip dest.zip file_to_zip`
* `man zip` (long et verbeux)
* `tldr zip` (comme man mais simplifié) #TooLongDidntRead
* `(sudo) reboot`
* `sudo apt install tldr` // `brew install tldr`
* `apt update`
* `update install pkg`


## vim
* to start typing, your need to get in insert mode. To do so, type ‘i’.
* To leave ‘insert mode’, hit ‘ESC’
* To save ‘:w’ (for write)
* To save and quit ‘:wq’ or ‘:x’
* To quit without saving ‘:q!’ (for quit)


## La variable PATH
* echo $PATH | tr ":" "\n”
* export ENV=“dev”
* export PATH=~/Workspace/:$PATH
* export ne fonctionne que pour la session en cours
* alis hist=‘hist | grep’ —> combiens history and grep. hist sudo


## Lister et killer les process
* ctrl Z pauses the process. It still exists and can be restarted as is wi ‘fg’ (for foreground)
* ctrl C kills the process, which cannot be restarted
* htop lists all processes. You can navigate the list with the arrows and kill the desired processes with k
    * Equivalent to top and kill PID

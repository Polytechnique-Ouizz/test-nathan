# Tutoriel github

Ceci est une premiere version du tutoriel github du Workshop web de l'X
Vous pouvez trouver une version beaucoup plus complète (en anglais) sur https://git-scm.com/book/en/v2

## Introduction

git est un logiciel de versionnement, c'est à dire un outil qui vous permet d'enregistrer un dossier contenant des fichiers textes (souvent du code) et de suivre les modifications dans le temps. Il fonctionne comme la fonction sauvegarder d'un logiciel de traitement de texte, et permet, en plus, de partager les fichiers et les modifications avec d'autres utilisateur.

Il utilise plusieurs concepts principaux:

Les repository (repo pour les intimes): ce sont des serveurs sur lesquels réside une version du code (des fichiers). Votre ordinateur constitue un repo. Le repo `github.com` qui est le repo central s'appelle communémant `origin`

Les commits : ce sont des états des fichiers à un instant donné. Faire un commit correspond à enregistrer des modifications des fichiers.

Les diff(s) : différences entre deux commits. Ils rendent compte des modifications effectuées à différents fichiers pour passer d'une version à une autre

Les branches : correspondent à différentes versions d'un projet vivant en parallèles. Elles permettent de faire des modifications en parallèle sans se marcher sur les pieds et de les fusionner à la fin.
La branche principale s'appelle `master` on peut créer des branches, effectuer des commits au sein de ces branches et fusionner les modifications avec `master` pour obtenir le résultat final

## Creation des comptes github

* Créer un compte sur http://github.com si ce n'est pas déjà fait.
* Installez aussi un client git et ajoutez vos clés SSH à votre compte
* Pour votre équipe, créer un unique repository `WorkshopGit` et récupérez son adresse, quelquechose comme :
git@github.com:Utilisateur/WorkshopGit.git

## Récupération du code

Sur votre ordinateur faites chacun

    git clone git@github.com:Organization/WorkshopGit.git
    cd WorkshopGit

Vous récupérez ainsi le répertoire WorkshopGit (pour l'instant il est vide) contenant les futurs fichiers
Les commandes suivantes sont intéressantes à connaitre :

### git remote

    git remote -v
    >>> origin  git@github.com:Organization/WorkshopGit.git (fetch)
    >>> origin  git@github.com:Organization/WorkshopGit.git (push)

Pour lister les repos comportant une copie du code (ici deux fois github.com pour le fetch et le push - la récupération et l'envoi donc) `origin` est le nom de la remote par défaut

### git branch

    git branch -a
    >>> * master
    >>> remotes/origin/master

Pour lister les branches (versions parallèles des fichiers présents). Celle avec une étoile est la branche active, ici `master` par défaut.
`remotes/origin/master` est son alter-ego sur le repo `origin`

## Création d'un fichier et premier commit

Chacun crée dans le dossier un fichier à son nom

    echo "blob" > monNom.txt

On peut voir avec `git status` que ce fichier est nouveau (en rouge), on l'ajoute alors au prochain commit avec :

    git add monNom.txt

Et on crée un commit avec tous les fichiers précédemment ajouté (`git status` donne la liste en vert)

    git commit -m 'ceci est le commit par lequel j ajoute le fichier monNom.txt'

Ensuite on synchronise nos modifications avec le serveur github (la remote `origin`) sur la branche `master`

    git push origin master

Si l'on a une erreur (! [rejected] ... non fast forward) cela signifie que l'on essaie d'envoyer des modifications alors que quelqu'un d'autre l'a fait avant nous. Il faut donc récupérer lesdites modifications, les merger avec notre code et renvoyer le résultat. On fait donc

    git pull origin master
    git push origin master

On récupère les données (pull) et on en envoit de nouvelles

## Modifications conflictuelles

Créez maintenant un fichier commun

    echo "Ceci est un fichier commun" > common.txt

Ajoutez le et créez un commit 
    
    git add common.txt
    git commit -m 'Ajout d un fichier commun'

Au moment de pusher sur origin/master (la remote origin, la branche master) vous allez certainement avoir un conflit (non fast forward) si quelqu'un d'autre a fait des modifications avant vous.

Il vous faut alors effectuer un `git pull origin master` qui va lui aussi vous retourner une erreur : des modifications simultanées sur le même fichier ne permettent pas à git de savoir lesquelles sont les plus récentes.

Dans `git status` vous verrez alors marqué d'un <M> le fichier `common.txt` , signe que ce fichier a besoin d'être modifié. Il vous faut alors l'éditer à la main, et rétablir la version qui vous semble la plus correcte.

Une fois vos modifications enregistrées il ne vous restera plus qu'a effectuer :

    git add common.txt
    git commit -m 'Merging file common.txt'
    git push origin master





# M1S1 Analyse de Données: Projet Final Cétacés

Dépôt de code / réflexions / ébauches / etc pour le projet Cétacés, Analyse des Données M1S1 Sciences de la Mer

## Organisation du dépôt

* Les jeux de données du projet
* Un sous-dossier propre à chaque membre pour les explorations indépendantes
* Les ressources communes
* [Plus tard] les résultats globaux, les interprétations et le code final

Petite note: Je te conseille vraiment d'essayer le format RMarkdown (.rmd) plutôt que du R standard ! Ça permet de mélanger du texte, des cartes, et du code dans un fichier agréable à lire. Tutoriel [ici](https://rmarkdown.rstudio.com/lesson-2.html) ou regarder mon dossier pour voir un exemple !  

## Qu'est-ce que Git/GitHub ?

Git est un système de gestion du code qui permet d'étier et de partager du code entre plusieurs personnes, notamment grâce à la gestion des changements. GitHub (et GitLab) est une plateforme en ligne qui sert d'hébergement pour le dépôt (et bien plus aussi).

Pour nous, il n'est pas nécessaire de tout savoir sur l'utilisation de git: une poignée de commandes devrait suffire. 

Les explications ci-dissous sont abrégées pour nos besoins. Il existe quelques ressources en bas de page pour approfondir ces concepts si besoin ( ou si mes explications sont nulles )!

### Dépôt: version Locale vs version distante (origine)

Le dépôt sur GitHub est « l'origine » (parfois appélé « remote »), c'est-à-dire la version du code qui est partagée par nous tous. Chacun de nous crée une copie du dépôt sur son propre ordinateur (la version locale). On utilise git pour communiquer entre ces deux versions. 

Un flux de travail typique consiste à:

1. faire un `pull` / récupérer les changements depuis l'origine pour mettre à jour la version locale
2. Modifier le code
3. faire un `push` / envoyer les changements vers l'origine

Note qu'on ne modifie pas directement l'origine ! Tout changement est d'abord fait sur une version locale.

**La communication entre la version locale et l'origine n'est pas automatique!** Il faut toujours utiliser les commandes git pour mettre à jour l'origine et la version locale.

### Changements du code

Les changements au code se font sous la forme des « commits », c'est-à-dire un groupe d'un ou plusieurs fichiers contenant des modifications, accompagné d'une description du changement.

Par exemple, si tu ajoutais une nouveau calcul pour la moyenne, tu créerais un commit contenant les changements concernés et tu l'intitulerais « Calcul de la moyenne » ou qqch de similaire.

Le système des commits permet de catégorizer les changements de manière claire pour tout le monde. Idéalement, chaque commit ne devrait correspondre qu'à un seul changement: « Calcul de la moyenne » est bien, « Calcul de la moyenne, cartes de distribution et corrections de bugs » est moins bien. Pour nous c'est moins important, mais c'est une bonne habitude à prendre.

Il vaut mieux faire souvent de petits commits que de gros commits occasionneles ! Si un changement n'est pas dans un commit, il reste uniquement sur la version locale et ne peut pas être envoyé vers l'origine pour que tout le monde puisse y accéder.

Ce n'est pas forcément nécessaire pour nous puisque R éxécute le code ligne par ligne, mais en général, un commit devrait **toujours** correspondre à du code qui marche! Ce principe est surtout important pour les organisations qui ont besoin que leur application reste fonctionnelle.

## Premiers pas avec Git/GitHub

Avant de commencer le tutoriel, crée un compte GitHub et communique-moi ton nom d'utilisateur pour que je puisse t'inviter comme contributeur au dépôt !

## Cloner le dépôt

1. Télécharge Git: https://git-scm.com/install/.

*Après avoir obtenu l'accès au dépôt...*

2. Clique sur le bouton vert « Code » sur la page d'accueil du dépôt sur GitHub et copie le lien HTTPS. *SSH est plus sécurisé, mais c'est plus compliqué de créer une clé SSH.*

3. Ouvre soit le terminal d'ordi, soit la terminal de RStudio (l'onglet « terminal » en bas). Navigue jusqu'au dossier parent dans lequel tu veux mettre ta version locale (par exemple, `cd /usr/M1S1/ADD` ).

4. Utilise git ! Tape `git clone [lien_https_ici]`. Le dossier devrait alors apparaître. 

5. Maintenant, tu peux créer un nouveau projet RStudio avec ce dossier ! *Note que le fichier ".Rproj"" et d'autres fichiers qui n'ont pas besoin d'être envoyés sur GitHub restent uniquement en local. Le fichier `.gitignore` contient une liste des extensions à ignorer.*

6. Vérifie que tu es connecté à l'origine: dans le terminal RStudio, avec le projet ouvert, tape `git remote -v`. Tu devrais voir deux URL. Si rien ne s'affiche, vérifie que t'es dans le bon dossier.

### Les commandes essentielles de Git

Prérequis: Ouvre le projet dans RStudio et clique sur l'onglet « terminal » en bas.

Ces commandes sont présentées dans l'ordre qui correspond à un flux de travail typique pour nous. **Sauf dans des cas exceptionnels, ce sont toutes les commandes dont nous avons besoin.**

`git pull origin main`

* Faire un `pull` / récupérer les changements depuis l'origine et mettre à jour ta version locale.

**C'est ici que tu peux faire tes modifications ! Pour commencer, je te conseille de créer un nouveau fichier dans ton propre dossier et, jsp, d'écrire `"Hello World"` ou qqch de simple dedans.**

`git status` 

* Permet de vérifier l'état actuel de la version locale. Tu peux voir quels fichiers ont été modifiés, quels fichiers sont « staged », etc.

`git add [path/to/file]` ou `git add .` (ajouter tous les fichiers)

* Désigne les fichiers qui seront ajoutés à ton commit (« staged »). Par exemple, si tu as modifié trois fichiers – `calculer_moyenne.r`,  `calculer_mediane.r` et `images/whale_picture.r` – et que tu veux faire un commit pour tes changements concernant le calcul des statistiques, tu ferais `git add calculer_moyenne.R calculer_mediane.R`. 

`git commit -m "ton message ici"`

* Crée un nouveau commit avec tous les fichiers « staged ». N'oublie pas d'avoir un message de commit informatif, mais succinct (~ 5-20 mots)

`git push origin main`

* Faire un `push` / envoyer ton commit vers l'origine. Il sera désormais intégré à la version d'origine et tout le monde pourra y accéder. *Il faudra peut-être saisir tes identifiants GitHub.*

### Conflits de fusion ( Merge Conflicts )

Le point fort de git est sa capacité de gérer les « merge conflicts »: lorsque deux personnes font des changements différents sur la même partie du code. 

Par exemple, imagine le scénario suivant: 

1) À 10h30, émile et moi faisons tous les deux un `pull` depuis l'origine.

2) Dans le fichier `README.md`, je modifie le titre pour qu'il devienne « Omi est hyper cool. » Je fais un commit et je le `push` vers l'origine à 10h45.

3) Emile prend son temps avec d'autres travaux, mais il modifie lui aussi le titre du README.md en « Emile est stylé. » Il fait un commit à 11h30, mais lorsqu'il essaie de faire un `push` vers l'origine, il reçoit une erreur. Puisqu'il n'a pas fait de `pull` depuis mon changement, il y a maintenant deux modifications différentes sur la même ligne de code !

En général, on veut éviter les merge conflicts autant que possible !! C'est une nuisance à gérer. Pour l'instant, la meilleure solution est de séparer notre travail: c'est-à-dire de travailler chacun dans son propre sous-dossier et d'éviter autant que possible les conflits. On pourra revenir sur le sujet quand on commencera à travailler sur les fichiers communs du code final (we'll cross that bridge when we get to it). Il existe beaucoup de ressources en ligne pour nous aider avec tout ça.

*Si vraiment besoin, le flux de travail pour le moment pour résoudre un merge conflict: `git stash` (cacher tes changements), `git pull origin main`, `git stash pop` (restaurer tes changements, chaque conflit avec l'origine sera souligné), modifier le code et enfin faire un nouveau `push`* 

### Branches

Si tu cherches des informations sur git en ligne, tu verras sûrement des informations sur les « branches ». Git permet d'avoir plusieurs branches, ou versions parallèles, d'un dépôt en même temps. Il est courant de créer des branches pour des « sous-projets » ou pour séparer la version stable d'une version en développement d'un logiciel.

Pour le moment, on n'a pas besoin des branches ni des « Pull requests/Requêtes de fusion », qui permettent de fusionner une branche avec une autre. 

## Plus de ressources

https://www.w3schools.com/git/default.asp

https://www.datacamp.com/fr/tutorial/github-and-git-tutorial-for-beginners

Vraiment il existe tellement de guides en ligne !! C'est hyper simple de trouver de l'aide. ChatGBT est doué pour le codage aussi mais tu ne devrais normalement pas avoir besoin de lui.

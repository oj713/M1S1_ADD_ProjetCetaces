# M1S1 Analyse de Données: Projet Final Cétacés

Dépôt de code / pensées / ébauches / etc pour le projet Cétacés, Analyse des Données M1S1 Sciences de la Mer

(Désolé d'avance si ma grammaire laisse à désirer , flemme de tout vérifier avec google translate mdr)

## Organisation du dépôt

* Le jeux de donnees du projet
* Dossiers propre à chaque membre pour les explorations independantes
* Ressources communes
* [Plus tard] résultats globals, interprétations, code final

Petite note: Je te conseille tellement d'essayer les fichiers RMarkdown (.rmd) au lieu de R standard ! Ça permet de mélanger le texte, les cartes, et le code dans un fichier agréable à regarder. Tutoriel [ici](https://rmarkdown.rstudio.com/lesson-2.html) ou tu peux voir mon dossier pour un exemple !  

## Qu'est-ce que c'est Git/GitHub ?

Git est un système de gestion du code qui permet l'édition et le partage du code entre plusieurs personnes, surout au niveau de gestion des changements. GitHub (et GitLab) est un plateforme en ligne qui sert comme l'hôte pour le dépôt (et beaucoup plus).

Pour nous, il ne faut pas tout savoir sur l'utilisation de git: une poignée de commandes suffira. 

Les explications ci-dissous sont abridgées pour nos fins, il y a quelques ressources en bas pour approfondir ces concepts si besoin ( ou si mes explications sont nulles )!

### Dépôt: la version Locale vs Remote/Origine

Le dépôt sur GitHub est "l'origine" (parfois appélé "remote"), ou le "vrai" code qui est partagé par nous tous. On fait, chacun, une "clone" de l'origine sur notre propre ordinateur (la version "locale"). On utilise git pour communiquer entre ces deux versions de code. Un flux de travail typique est de:

1. "pull" / récupérer tout changement de l'origine pour que la version locale soit mise à jour
2. Modifier le code
3. "push" / charger nos changements vers l'origine

Note qu'on ne modifie pas directement l'origine ! Tout changement est fait d'abord sur une version locale.

**La communication entre la version locale et l'origine n'est pas automatique!** Il faut toujours utiliser les commandes git pour mettre à jour l'origine et la locale.

### Changements de code

Changements au code se fait sous la forme des "commits", aka un groupe d'un ou plusieurs fichiers avec des modifications accompagné par une description du changement. Par exemple, si tu ajoutais une nouvelle calculation pour la moyenne, tu créerais un commit avec tout changement rélevant et l'intitulerais "Calculation de la moyenne" ou similaire.

Le système des commits permet de catégorizer les changements au code d'une manière claire pour tout le monde. Idéalement, chaque commit n'a qu'un seul changement: "Calculation de la moyenne" est bon, "Calculation de la moyenne et cartes de distribution et bugfixes" est mauvais. Pour nous c'est moins important, mais bon de garder comme but.

C'est meilleur de faire des petits commits souvent que les grands commits occasionnelement ! Si un changement n'est pas dans un commit, ça reste coincé sur la version locale et ne peut pas être chargé à l'origine pour que tout le monde ait l'accès.

C'est pas nécessaire pour nous puisque R éxécute ligne par ligne, mais en général un commit devrait toujours répresenter un code qui marche! Cette principe est surtout important pour les organisations qui ont besoin que leur application fonctionne.

## Premiers pas avec Git/GitHub

Avant de commencer le tutoriel, crée un compte GitHub et me la communiquer pour que je puisse t'inviter comme contributeur de dépôt !

## Cloner le dépôt

1. Télécharge Git: https://git-scm.com/install/.

*Après avoir débloqué l'accès...*

2. Cliquer sur le bouton vert « Code » dans l'accueil du dépôt sur GitHub et copier le lien HTTPS. *SSH est plus sécure, mais c'est compliqué de créer un clé SSH*

3. Ouvre soit le terminal, soit RStudio puis clique sur l'onglet "terminal" en bas. Navigue à le dossier parent où tu veux mettre ta version locale (e.g. `cd /usr/M1S1/ADD` )

4. Utilise git ! Tape `git clone [lien_https_ici]`. Le dossier devrait apparaître. 

5. Maintenant tu peux créer un nouveau projet RStudio avec ce dossier ! *Note que le fichier ".Rproj"" et d'autres fichiers qui n'ont pas besoin d'être charger à GitHub sont gardés que localement, ".gitignore" a une liste des extensions à ignorer.*

6. Vérifie que tu es connecté à l'origine: dans RStudio Terminal, avec le projet ouvert, tape `git remote -v`. Tu devrais voir deux URLs. Si ça ne se voit pas, vérifie que t'es dans le bon dossier.

### Les commandes essentielles en Git

Prérequis: Ouvre le projet dans RStudio et clique sur l'onglet "terminal" en bas.

Ces commandes sont présentées en un ordre qui corrépond à un flux de travail typique pour nous. **Sauf les cas exceptionnel, ce sont tous les commandes dont on a besoin.**

`git pull origin main`

* "Pull" / récupérer les changements à l'origine et mettre à jour ta version locale.

**Ici, fais des modifications ! Pour débuter, je te conseille de créer un nouveau fichier dans ton propre dossier et jsp, écrire `print("Hello World")` ou qqch simple dedans.**

`git status` 

* Permet de vérifier l'état actuel de la version locale. Tu peux voir quels fichiers ont des changements, quels fichiers sont "staged", etc.

`git add [path/to/file]` ou `git add .` (ajouter tous les fichiers)

* Designe les fichiers qui seront ajoutés à ton commit ("staged"). Par exemple, si tu as modifié deux fichiers – "calculer_moyenne.r", "calculer_mediane.r" et "images/whale_picture.r" – et tu veux faire un commit pour tes changements à la calculation des statistiques, tu ferais `git add calculer_moyenne.R calculer_mediane.R`. 

`git commit -m "ton message ici"`

* Crée un nouveau commit avec tous les fichiers staged. N'oublie pas d'avoir un message de commit informatif, mais succinct (5-20 mots, environ)

`git push origin main`

* "Push" / charge ton commit vers l'origine. Il sera désormais intégré dans la version origine et tout le monde peut l'accéder. *Il va falloir peut-être saissiser tes crédentiels GitHub*

### Merge Conflicts

Le point fort de git est sa capacité de gérer les "merge conflicts": quand il y a deux différents changements proposés pour le même morceau du code. 

Par exemple, considère cette scénario: 

1) À 10h30, moi et emile faisons tous les deux un pull de l'origine.

2) Dans le fichier "README.md", je modifie le titre d'être "Omi est hyper cool." Je fais un commit et je le push à l'origine à 10h45.

3) Emile prends son temps avec d'autre travail, mais il modifie aussi le titre du README.md à "Emile est stylé." Il fait lui aussi un commit à 11h30, mais quand il essaie de push à l'origine il va recevoir une erreur. Puisqu'il n'a pas fait un pull depuis mon changement, il y a maintenant deux différents changements au même ligne de code !

En général, on veut éviter les merge conflicts au maximum !! C'est une nuisance de les gérer. Pour l'instant, la meilleur solution est de séparer notre travail: c'est à dire on travaille chacun dans notre propre sous-dossier et évite toute possibilité d'un merge conflict. On peut revisiter le sujet quand on commence à avoir les fichiers communs pour le code final (we'll cross that bridge when we get to it). Il existe beaucoup de ressources en ligne pour nous aider avec tout ça.

### Branches

Si tu cherches git en ligne, tu verras surement des informations sur les "branches". Git te permet d'avoir plusieurs "branches", ou versions, d'un dépôt au même temps. C'est commun de créer des branches pour les "sous-projets" ou pour séparer la version stable/version en développement d'un logiciel.

Pour le moment on n'a pas besoin des branches, ni des "Pull requests/Requêtes de fusion" (la méthode pour rattacher une branche à sa parente). 

## Plus de ressources

https://www.w3schools.com/git/default.asp

https://www.datacamp.com/fr/tutorial/github-and-git-tutorial-for-beginners

Vraiment il existe tellement de guides en ligne !! Hyper simple de trouver de l'aide. ChatGBT y est doué aussi mais tu ne devrais pas avoir besoin de lui.

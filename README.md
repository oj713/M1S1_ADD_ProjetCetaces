## M1S1 Analyse de Données: Projet Final Cétacés

Dépôt de code / pensées / ébauches / etc pour le projet Cétacés, Analyse des Données M1S1 Sciences de la Mer

## Organisation du dépôt

* Le jeux de donnees du projet
* Dossiers propre à chaque membre pour les explorations independantes
* Ressources communes
* [Plus tard] résultats globals, interprétations, code final

## Introduction à Git/GitHub

(Désolé d'avance si ma grammaire laisse à désirer , flemme de tout vérifier avec google translate mdr)

Git est un système de gestion du code qui permet l'édition et le partage du code entre plusieurs personnes, surout au niveau de gestion des changements. GitHub (et GitLab) est un plateforme en ligne qui sert comme l'hôte pour le dépôt (et beaucoup plus).

Pour nous, il ne faut pas tout savoir sur l'utilisation de git: une poignée de commandes suffira. 

Les explications ci-dissouses sont abridgées pour nos fins, il y a quelques ressources en bas pour approfondir ces concepts si besoin.

### Dépôt: la version Locale vs Remote/Origine

Le dépôt sur GitHub est "l'origine" (parfois appélé "remote"), ou le "vrai" code qui est partagé par nous tous. On fait, chacun, une "clone" de l'origine sur notre propre ordinateur (la version "locale"). On utilise git pour communiquer entre ces deux versions de code. Un flux de travail typique est de:

1. "pull" / récupérer tout changement dans l'origine pour que la version locale soit mise à jour
2. Modifier le code
3. "push" / charger nos changements à l'origine

Note qu'on ne modifie pas directement l'origine ! Tout changement est fait d'abord sur une version locale.

**La communication entre la version locale et l'origine n'est pas automatique!** Il faut toujours utiliser les commandes git pour mettre à jour l'origine et la locale.

## Premiers Pas avec Git/GitHub

1. Crée un compte GitHub et me la communiquer pour que je puisse t'inviter comme contributeur !

2. Télécharge Git: https://git-scm.com/install/

*Après avoir débloqué l'accès*



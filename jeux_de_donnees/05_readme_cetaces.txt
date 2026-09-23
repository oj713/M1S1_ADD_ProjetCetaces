CÉTACÉS — TRANSECTS D'OBSERVATION DANS LE GOLFE DE GASCOGNE
Jeu de données n° 05

****************************************************************************************************
  ATTENTION — DONNÉES ENTIÈREMENT SIMULÉES
  Ce jeu de données a été généré à des fins pédagogiques (Master 1 Sciences de la Mer, Sorbonne
  Université). Aucune valeur ne provient d'une mesure réelle. Les toponymes cités ne servent qu'à
  fixer une emprise géographique et un système de coordonnées plausibles. Ces données ne doivent
  en aucun cas être citées comme observations.
****************************************************************************************************


CONTEXTE SCIENTIFIQUE
=====================

Le golfe de Gascogne abrite une communauté de cétacés parmi les plus diversifiées d'Europe :
dauphins communs sur le plateau, globicéphales et rorquals sur le talus, cachalots dans les canyons
profonds. Ces animaux ne sont pas répartis au hasard : ils suivent la ressource, elle-même
concentrée là où la topographie force la remontée d'eaux riches — talus continental, têtes de
canyons.

Recenser ces populations pose un problème méthodologique classique : on ne compte jamais les animaux
présents, seulement ceux que l'on a vus. Un transect long donne plus d'observations qu'un transect
court, et une mer agitée en fait manquer beaucoup. L'analyse doit donc démêler l'abondance réelle de
l'effort et des conditions d'observation.

Ce jeu rassemble 540 transects d'observation réalisés en bateau entre 43 et 52 °N, du plateau
continental à la plaine abyssale, sur les quatre saisons.


FICHIERS FOURNIS
================

- Cetaces_Transects.csv : le tableau de données (540 lignes, 15 colonnes).
- 05_cetaces.gpkg : la couche géographique des 540 transects (GeoPackage, à ouvrir dans QGIS).


LIRE LES DONNÉES SOUS R
=======================

La première ligne du fichier CSV est une ligne de commentaire (elle commence par #) qui rappelle le
caractère simulé des données. Le séparateur de colonnes est le point-virgule et le séparateur
décimal est le point :

    donnees <- read.table("Cetaces_Transects.csv", header = TRUE, sep = ";", dec = ".", comment.char = "#")

ATTENTION : read.csv2() et read.csv(..., sep = ";") échouent sur ce fichier, car ils ne savent pas
ignorer la ligne de commentaire. Utilisez la commande ci-dessus.


VARIABLES ÉTUDIÉES
==================

Le tableau contient les variables suivantes. Le type de chaque variable n'est volontairement pas
précisé : l'identifier, et en tirer les conséquences pour le choix de vos analyses, fait partie du
travail demandé.

- id : identifiant du transect (CET_0001 à CET_0540). Il sert à joindre le tableau à la couche
  géographique.
- secteur : secteur bathymétrique (Plateau, Talus, Canyon, Plaine abyssale).
- saison : saison de l'observation (Hiver, Printemps, Ete, Automne).
- espece_dominante : espèce dominante observée sur le transect (Aucune, Dauphin commun,
  Globicephale, Rorqual commun, Cachalot).
- effort_km (km) : longueur du transect parcouru en veille.
- etat_mer_beaufort (échelle de Beaufort, de 0 à 6) : état de la mer pendant l'observation.
- profondeur_m (m) : profondeur moyenne le long du transect.
- distance_cote_km (km) : distance à la côte.
- sst_c (°C) : température de surface de la mer.
- chlorophylle_mgm3 (mg/m³) : concentration en chlorophylle.
- nb_groupes_observes : nombre de groupes de cétacés détectés sur le transect.
- taille_groupe_moyenne (individus par groupe) : taille moyenne des groupes, renseignée uniquement
  si au moins un groupe a été vu.
- presence : au moins un groupe observé sur le transect (0, 1).
- lon, lat (degrés décimaux, WGS84, EPSG:4326) : position du centre du transect.

Les modalités sont écrites ci-dessus exactement comme dans le fichier (sans accents) : c'est sous
cette forme qu'il faut les utiliser dans vos scripts.


LA COUCHE GÉOGRAPHIQUE
======================

Le fichier 05_cetaces.gpkg contient les 540 transects sous forme de points (le point représente le
centre du transect), en WGS84 (EPSG:4326). L'emprise couvre environ 1 000 km de diagonale, du
plateau armoricain à la plaine abyssale du golfe.

Les transects ne sont pas répartis uniformément : la campagne a concentré son effort là où les
observations étaient attendues. La colonne id permet de rejoindre le tableau CSV et la couche.


EXEMPLES DE QUESTIONNEMENTS SCIENTIFIQUES
=========================================

1. Où sont les cétacés ? Comment le nombre de groupes observés varie-t-il avec la profondeur, la
   distance à la côte et la chlorophylle ? La relation à la profondeur est-elle monotone ?

2. Compter n'est pas observer. Les transects n'ont pas tous la même longueur, ni été réalisés par la
   même mer. Comment en tenir compte pour que votre modèle décrive l'abondance des animaux plutôt
   que l'intensité de la prospection ?

3. Choix du modèle. Quelle est la nature de la variable réponse nb_groupes_observes ? Ajustez le
   modèle qui vous paraît adapté, puis examinez ses résidus et sa dispersion. Le modèle décrit-il
   correctement la variabilité observée ? Si ce n'est pas le cas, qu'est-ce qui, dans la biologie de
   ces animaux, pourrait l'expliquer, et quelle alternative proposeriez-vous ?

4. Ségrégation entre espèces. Les cinq modalités d'espèce dominante occupent-elles les mêmes
   profondeurs et les mêmes secteurs ? Que signifie la modalité Aucune ?

5. Les valeurs manquantes. taille_groupe_moyenne est vide pour la moitié des transects. Pourquoi ?
   Faut-il les remplacer, les supprimer, ou les traiter autrement ? Votre choix change-t-il les
   conclusions ?

6. Saisonnalité. Y a-t-il un effet de saison, et si oui, passe-t-il par l'abondance des animaux ou
   par les conditions d'observation ?

7. Question cartographique. Cartographiez le taux de rencontre (groupes par kilomètre parcouru)
   plutôt que le nombre brut. La carte change-t-elle ? Les fortes valeurs se regroupent-elles, et le
   long de quelle structure du fond ?

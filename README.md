# Datavisualisation sur les prénoms des nouveaux-nés
NB : Ceci est une page Github réalisée dans le cadre du cours de datavisualisation en M2 Documents électroniques et flux d'informations (Université Paris Nanterre)
# Prénoms des nouveaux-nés des villes d'Antibes et de Paris
![Illustration nouveaux-nés](twins-1628843_1280(1).jpg) 
Téléchargé à partir de Pixabay
# Sommaire 
1. [Introduction : présentation du projet](#presentation)
2. [Jeux de données et Sprint qualité](#donnéesBrutes)
3. [Visualisation des données](#visualisation)
4. [Conclusion](#conclusion)

## Introduction : présentation du projet <a name="presentation"></a>
Ce travail porte sur les prénoms des nouveaux-nés déclarés dans les villes d'Antibes et de Paris pendant 10 ans. Nous cherchons ainsi à comprendre s'il y a une différence entre les prénoms données dans une ville en bord de mer et une ville en pleine terre. Les couvertures spatiales n'étant pas les mêmes, nous avons choisi de partir sur la tranche commune aux deux jeux de données et la plus récente d'où la sélection de la période de _2012 à 2022_.

## Jeux de données et Sprint qualité <a name="donnéesBrutes"></a>
**_ANTIBES :_**

Pour le jeu de données de la ville d'Antibes, nous avons procédé à un sprint qualité en nous basant sur 10 questions principales (soft sprint qualité : grille donnée par monsieur Antoine Courtin). Puis nous avons procédé à la rectification du fichier CSV de base pour respecter le schema destiné aux prénoms des nouveaux nés accessible via le lien ci-après : https://schema.data.gouv.fr/scdl/prenoms/.
Et enfin nous avons été sur : https://publier.etalab.studio/fr/ pour vérifier la conformité du fichier après avoir rectifié les erreurs détectées dans le rapport. 

Ci-joint, les détails de ce sprint qualité : 
+ Fichier de base mis à disposition par la ville d'Antibes : (Voir le fichier "antibes_prenoms_naissance.csv" dans le répertoire)

+ Sprint qualité :
  [SprintQualite_Soft_DieynabaKouyate_M2_DEFI_2024.pdf](https://github.com/DieynabaKOUYATE/Datavisualisation_Prenoms_Nouveaux-nes_Dieynaba_KOUYATE/files/13920336/SprintQualite_Soft_DieynabaKouyate_M2_DEFI_2024.pdf)

+ Processus de correction pour respect du schéma : 
  [SchemaDonnees_Prenoms_DieynabaKouyate_M2_DEFI_2024.pdf](https://github.com/DieynabaKOUYATE/Datavisualisation_Prenoms_Nouveaux-nes_Dieynaba_KOUYATE/files/13920341/SchemaDonnees_Prenoms_DieynabaKouyate_M2_DEFI_2024.pdf)
  
+ Fichier corrigé et respectant le schéma des prénoms : (Voir le fichier "antibes_prenoms_naissance_corrige.csv" dans le répertoire)



**_PARIS :_** 


Concernant ce deuxième jeu de données, nous estimons que le seul respect du schema est garant de cohérence et de qualité. Ainsi, nous n'avons pas appliqué la grille "soft sprint qualité" mais avons opté pour la correction des données en vue de respecter le schéma. 
Pour ce faire, nous avons été sur le site de la ville de paris pour télécharger le jeu de données des prénoms déclarés en CSV. Pour prémacher le travail de visualisation, nous avons fait un filtre sur les années en les reserrant sur la période de 2012-2022 https://opendata.paris.fr/explore/dataset/liste_des_prenoms/export/?disjunctive.annee&disjunctive.prenoms&q.timerange.annee=annee:%5B2012-01-01+TO+2022-12-31%5D.

 ![Paris_Filtre10ans](https://github.com/DieynabaKOUYATE/Datavisualisation_Prenoms_Nouveaux-nes_Dieynaba_KOUYATE/assets/151731756/93ca539e-2031-49a9-bda3-c6c18d2e7cd6)

Nous avons téléchargé le fichier CSV et l'avons rectifié :
+ Renommage des colonnes pour y mettre les intitulés listés dans le schéma 
+ Suppression de la colonne "Nombre total cumule par annee"
+ Sprint qualité du fichier CSV via https://publier.etalab.studio/fr/, nous avons détecté le non respect du schema car il y avait la colonne insee manquante
+ Ajout de la colonne "COLL_INSEE"
+ Nouvelle vérification sur  https://publier.etalab.studio/fr/ et le fichier est déclaré conforme.

Pour récupérer les 2 fichiers :
+ Fichier de base mis à disposition par la ville de paris : (voir le fichier "Paris_liste_des_prenoms.csv" dans le répertoire)
+ Fichier corrigé : (voir le fichier "Paris_liste_des_prenoms_corrige.csv" dans le répertoire)



Ensuite, nous avons été sur WTF CSV (https://databasic.io/en/wtfcsv/#upload), pour changer l'approche du "sanity check" et avoir quelques visualisations permettant d'avoir des informations générales. 

Ainsi, on sait que sur notre corpus de prénoms déclarés entre 2012 et 2022 dans la ville de paris :
+ Il y a 14201 lignes dans notre fichier
+ 5 prénoms se démarquent avec une occurrence de 22 : Alix, Andrea, Camille, Charlie et Eden
+ Il y a au moins 1270 prénoms de nouveaux nés déclarés dans la ville de paris sur chaque intervalle d'un an
+ Les occurrences les plus fréquentes varient de 5 à 43 : 12217 occurrences comprises dans l'intervalle 5-43
+ Il y a plus de filles déclarées que de garçons
+ Les valeurs 75056 et Paris sont répétés 14201 fois

![Debut_WTFCSV](https://github.com/DieynabaKOUYATE/Datavisualisation_Prenoms_Nouveaux-nes_Dieynaba_KOUYATE/assets/151731756/2cff2b95-041d-4575-93a1-aabc192bb03c)

  
![Visualisation_WTFCSV](https://github.com/DieynabaKOUYATE/Datavisualisation_Prenoms_Nouveaux-nes_Dieynaba_KOUYATE/assets/151731756/ff5f2e7c-f5bb-4cc7-8bdb-00eded4b6b74)


## Visualisation des données <a name="visualisation"></a>

Pour effectuer nos visualisations, nous avons assemblé les jeux de données dans un seul fichier en restant uniquement sur la période 2012-2022. Ensuite, nous avons utilisé OpenRefine pour enrichir les données avec wikidata (en y ajoutant la localisation) afin de pouvoir situer les 2 villes sur une carte à travers Umap. 
 https://umap.openstreetmap.fr/en/map/anonymous-edit/1009761:RYZ7hUddR1-MgxEubiB9JeYKvxFt9ML3m8QDribB0Pc

<iframe width="100%" height="500px" frameborder="0" allowfullscreen allow="geolocation" src="//umap.openstreetmap.fr/en/map/localisation-de-paris-et-antibes-sur-la-carte-de-f_1010185?scaleControl=false&miniMap=false&scrollWheelZoom=false&zoomControl=true&editMode=disabled&moreControl=true&searchControl=null&tilelayersControl=null&embedControl=null&datalayersControl=true&onLoadPanel=undefined&captionBar=false&captionMenus=true"></iframe><p><a href="//umap.openstreetmap.fr/en/map/localisation-de-paris-et-antibes-sur-la-carte-de-f_1010185?scaleControl=false&miniMap=false&scrollWheelZoom=true&zoomControl=true&editMode=disabled&moreControl=true&searchControl=null&tilelayersControl=null&embedControl=null&datalayersControl=true&onLoadPanel=undefined&captionBar=false&captionMenus=true">See full screen</a></p>

## Conclusion <a name="conclusion"></a>

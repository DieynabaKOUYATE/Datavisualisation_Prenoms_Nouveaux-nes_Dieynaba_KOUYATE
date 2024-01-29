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

Pour effectuer nos visualisations, nous avons assemblé les jeux de données dans un seul fichier en restant uniquement sur la période 2012-2022. Ensuite, nous avons utilisé OpenRefine pour enrichir les données avec wikidata (en y ajoutant les localisations) afin de pouvoir situer les 2 villes sur une carte à travers Umap. Mais avant, différentes manipulations ont été nécessaires. 

+ On a dû créer un fichier "assemblage.csv" où on a rassemblé les données des 2 villes dans un seul fichier CSV. On voulait le faire directement sur OpenRefine (car c'est possible si les jeux de données ont la même structure) mais il y avait un souci : le fichier de la ville de Paris était un "faux csv" le séparateur était le point virgule et non la virgule (comme sur le jeu de données de la ville d'Antibes). Pour palier à ce souci, nous avons créé le fichier "assemblage.csv" sur LibreOffice avant de faire le traitement et l'enrichissement sur OpenRefine.
  
+ Pour le traitement des jeux de données, on a d'abord réglé la question des clusters. Un même prénom pouvait avoir différentes orthographes. On a choisi l'orthographe qui nous semblait la plus correcte / la plus utilisée (voir image) .
![Capture des 256 Clusters](https://github.com/DieynabaKOUYATE/Datavisualisation_Prenoms_Nouveaux-nes_Dieynaba_KOUYATE/blob/main/Clusters.PNG)


Sur la carte ci-dessous : les localisations d'Antibes et de Paris

<iframe width="100%" height="800px" frameborder="0" allowfullscreen allow="geolocation" src="//umap.openstreetmap.fr/en/map/lieu-de-naissance-des-198-prenoms-qui-ont-le-plus-_1009761?scaleControl=false&miniMap=false&scrollWheelZoom=false&zoomControl=true&editMode=disabled&moreControl=true&searchControl=null&tilelayersControl=null&embedControl=null&datalayersControl=true&onLoadPanel=undefined&captionBar=false&captionMenus=true"></iframe><p><a href="//umap.openstreetmap.fr/en/map/lieu-de-naissance-des-198-prenoms-qui-ont-le-plus-_1009761?scaleControl=false&miniMap=false&scrollWheelZoom=true&zoomControl=true&editMode=disabled&moreControl=true&searchControl=null&tilelayersControl=null&embedControl=null&datalayersControl=true&onLoadPanel=undefined&captionBar=false&captionMenus=true">See full screen</a></p>

Nous avons voulu représenté les données sous une autre forme visuelle : des "Dots" dont les tailles varient en fonction des occurrences. Pour ce faire, on est parti sur un corpus très réduits avec uniquement les colonnes prénoms, sexe, nom de la commune, année. Pour arriver à ce résulat, il fallait faire des choix et la question principale était la suivante : sur quoi se baser pour choisir certains prénoms à la place d'autres? La réponse nous semblait évidante : partir sur les 3 premiers prénoms par années et par ville afin d'avoir un corpus réduit des Top 3. 
Nous avons entamé cette démarche sur OpenRefine et nous sommes rendus compte que cela n'était pas un critères suffisant : on pouvait avoir 4 prénoms qui ont le même nombre d'occurrence pour une même année. Afin d'éviter cet obstacle, on est plutôt parti sur les 3 plus grandes occurrences de prénoms par année et par ville. Autrement dit si on a plus de 3 prénoms qui ont néanmoins la même occurrence et que cette occurrence fait partie des 3 premières, on les sélectionne tous. 

Pour avoir un corpus Top 3 des occurrences, à partir de notre fichier "assemblage.csv" on a :
+ appliquer des facettes sur les noms de commune  
+ appliquer des facettes sur les années (par intervalle d'un an sauf pour la dernière année où on a "filtré le texte" pour rechercher la valeur exacte "2022" afin d'avoir les lignes correspondantes) 
+ trier par ordre décroissant les nombres d'occurrences afin de voir les plus grandes en premier (en restant sur les facettes précédentes car sinon la commune de était toujours première car c'est là-bas qu'on a les plus grandes occurrences)
+ étoiler les prénoms qui répondent aux critères
+ quitter les facettes pour retourner dans l'onglet "Défaire/Refaire"
+ appliquer une facette par étoile à la colonne "toutes" 
+ **au final on a eu un corpus de 213 prénoms au total à analyser: 66 à Paris et 147 à Antibes** 


En outre, on a décidé de faire 2 visuelles séparées pour les 2 villes afin que ce soit un peu plus digeste à regarder. On a décidé d'appliquer un filtre sur les années afin qu'on puisse visualiser pour chaque ville les différences/ressemblances en fonction des années. On a appliqué les couleurs pas en fonction des prénoms car on ne le trouve pas pertinent mais en fonction des sexes. 

**Antibes : les 147 prénoms les plus donnés aux nouveaux nés de 2012 à 2022**

<iframe src='https://flo.uri.sh/visualisation/16564724/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/16564724/?utm_source=embed&utm_campaign=visualisation/16564724' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>

**Paris : les 66 prénoms les plus donnés aux nouveaux nés de 2012 à 2022**
<iframe src='https://flo.uri.sh/visualisation/16554580/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/16554580/?utm_source=embed&utm_campaign=visualisation/16554580' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>

**Les 213 prénoms les plus donnés à Antibes et Paris**
<iframe src='https://flo.uri.sh/visualisation/16565616/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/16565616/?utm_source=embed&utm_campaign=visualisation/16565616' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>


**Paris : Les prénoms les plus donnés de 2012 à 2022 (les 3 plus grandes occurrences) chez les filles et les garçons**
> *Questionnement : quels sont les prénoms les plus donnés aux nouveaux-nés à Paris de 2012 à 2022 en fonction du sexe (en se basant sur les 3 plus grandes occurrences)?.*
<iframe title="[ Les prénoms les plus donnés à Paris de 2012 à 2022 (Top 3 des plus grandes occurrences chez les filles et les garçons)] (Copy)" aria-label="Bar Chart" id="datawrapper-chart-mCC05" src="https://datawrapper.dwcdn.net/mCC05/1/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="608" data-external="1"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r=0;r<e.length;r++)if(e[r].contentWindow===a.source){var i=a.data["datawrapper-height"][t]+"px";e[r].style.height=i}}}))}();</script>

**Antibes : Les prénoms les plus donnés de 2012 à 2022 (les 3 plus grandes occurrences) chez les filles et les garçons**
> *Questionnement : quels sont les prénoms les plus donnés aux nouveaux-nés à Antibes de 2012 à 2022 en fonction du sexe (en se basant sur les 3 plus grandes occurrences)?.*
<iframe src='https://flo.uri.sh/visualisation/16622371/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/16622371/?utm_source=embed&utm_campaign=visualisation/16622371' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div>

## Conclusion <a name="conclusion"></a>

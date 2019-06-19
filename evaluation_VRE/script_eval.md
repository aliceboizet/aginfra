# Présentation du VRE Food Security

## Qu'est ce qu'un VRE ?
Un VRE (Virtual Research Environment) est un environnement de travail virtuel et collaboratif à destination des chercheurs.
"Il est constitué par un ensemble d’outils et de ressources en ligne rendues interopérables dans l’objectif de faciliter les processus de recherche au sein et entre les institutions. La caractéristique essentielle d’un VRE est de faciliter la collaboration entre les scientifiques." [source IFB](https://www.france-bioinformatique.fr/en/groupes-de-travail/virtual-research-environment)

Le fait qu'il soit virtualisé permet tout d'abord au chercheur de travailler sur son environnement depuis n'importe quel machine : ses données sont stockées dans le VRE et des outils (tels que Rstudio) permettant d'analyser les données sont accessibles directement dans le VRE.

Un espace de travail partagé permet aux chercheurs de partager leurs données ou processus de traitement et ainsi de collaborer plus facilement.

## Projet AgINFRA+
AGINFRA + vise à exploiter les e-infrastructures telles que l'EGI et D4Science, pour fournir des VREs adaptés à certaines communautés de chercheurs autour de l' agriculture et  de l'alimentation.

À cette fin, le projet a mis en place plusieurs VRE pour 3 communautés :
- la communauté de la modélisation agro-climatique
- la communauté de la sûreté alimentaire
- la communauté de la sécurité alimentaire.

Le but du projet est d'alimenter ces VREs avec différents composants répondant aux besoins de chaque communauté. Ainsi, des fonctionnalités permettant le développement rapide et intuitif de workflows variés d’analyse de données ont été intégrées ainsi que des outils de visualisation de données.

## Food Security VRE

Le Food Security VRE est porté par la plateforme D4Science, développée par le CNR.
[https://aginfra.d4science.org/group/foodsecurity](https://aginfra.d4science.org/group/foodsecurity)
Pour la communauté "Food Security", le cas d'utilisation autour du phénotypage de plante haut-débit qui produit de gros volumes de données variées.

# Evaluation des fonctionnalités

## Objectifs et déroulement de l'évaluation
Le but de l'exercice est d'évaluer si un VRE et plus particulièrement le VRE "Food Security" est un outil qui peut faciliter les travaux de recherche en phénotypage.

Après la présentation des différentes fonctionnalités du VRE, vous allez être amenés à suivre un scénario utilisateur permettant de tester chacune de ces fonctionnalités.
Ensuite vous pourrez répondre à un questionnaire dans lequel il faudra noter chaque fonctionnalité suivant différents indicateurs.

##Scénario utilisateur

### Inscription/connexion au VRE
Rendez-vous sur [https://aginfra.d4science.org/group/foodsecurity](https://aginfra.d4science.org/group/foodsecurity).
Si vous êtes déjà inscrit, connectez-vous directement et passez directement à l'étape suivante. Sinon, inscrivez-vous au VRE (par la méthode de votre choix)

### Trouver des données

#### L'espace de travail
- Le workspace
Cliquez sur ![](./img/workspace_icone.png).
Dans le répertoire VRE Folders, vous accédez pour à l'espace commun de chaque VRE auquel vous êtes inscrit. Les fichiers que vous déposerez dans VRE Folders/Food Security VRE seront donc accessibles aux autres membres du VRE.
Les répertoires et fichiers créés à la racine du workspace sont privés.

- La messagerie
Cliquez sur ![](./img/mail_icone.png).
Vous avez la possibilité d'utiliser cette messagerie pour envoyer des messages privés aux membres du VRE.

- Le catalogue
Cliquez sur ![](./img/catalogue_icone.png){ width=50% }.
Le catalogue recense les ressources disponibles sur le VRE. Son utilisation sera expliquée dans une autre partie

#### Refindit
Allez dans Discovery/Refindit. Cherchez une publication (exemple : la publication sur PHIS : P. Neveu, A. Tireau, N. Hilgert, V. Nègre, J. Mineau-Cesari, N. Brichet, R. Chapuis, I. Sanchez, C. Pommier, B. Charnomordic, F. Tardieu, L. Cabrera-Bosquet, Dealing with multi-source and multi-scale information in plant phenomics: the ontology-driven Phenotyping Hybrid Information System, New Phytol., 221 (2019) 588-601. doi: 10.1111/nph.15385)

#### Récupérer des données depuis les Web Services BrAPI
BRAPI (pour Plant Breeding API) est une spécification d'un standard d'API pour les données en phénotypage et génotypage. Toutes les API respectant ce standard pourront donc être appelées de la même manière, ce qui facilite l'accès et l'échange des données.

1. Allez dans l'application Brapi Data Exploration  
*Non Disponible pour le moment*

2. Récupérer des données de PHIS grâce aux services BrAPI

Allez dans *Analytics/Data Miner*. Cliquez sur *Execute an experiment*.
Dans le menu sur la gauche, cliquez sur *Data Extraction* et *Brapi_Get_Studies_Observations*

Remplissez les différents champs avec les paramètres suivants et cliquez sur *Start Computation*
- DBServerURL : http://138.102.159.37:8080/openSilexTestAPI/rest 
- studies : http://www.phenome-fppn.fr/test/DMO2019-6 
- variables : all 
- login : admin@opensilex.org 
- password : 21232f297a57a5a743894a0e4a801fc3 


### Les environnements de développement
- Rstudio
Allez dans *Analytics/Rstudio*
Dans le cadre en bas à droite, parcourez les répertoires pour retrouver le fichier de données créé par Data Miner. 
Le répertoire *Workspace* correspond au workspace du VRE. Allez dans *Workspace/DataMiner/output_dataset

Ecrivez un script R court qui lit les données de ce fichier et qui crée un fichier en sortie (*ex : un fichier texte avec la moyenne des mesures*)


- JupyterLab
Allez dans *Analytics/Jupyter*

### Rendre ses scripts exécutables par n'importe qui (SAI)
Vous allez importer un script R dans le Data Miner afin de pouvoir l'exécuter comme une boîte noire
*exemple : un script qui prend comme paramètres un fichier csv et le nom de la colonne sur laquelle calculer une moyenne et qui renvoie un fichier avec la moyenne*



### Réaliser des workflows de traitement (Galaxy)

Allez dans *Analytics/Galaxy*
Dans la barre du haut, cliquez sur *workflow*, cliquez sur le + pour créer un nouveau workflow : renseignez un nom et cliquez sur *Save*.

Vous allez créer un workflow qui contient 3 étapes : donc 3 tools
La 1ère étape récupère les données d'observations de PHIS grâce à l'algorithme data miner utilisé auparavant.
Tous les algorithmes du dataminer sont convertis automatiquement en *"tool"* Galaxy : ceux-ci se trouvent dans la rubrique DataMiner. 
Cliquez sur le *"tool"* BRAPI_GET_STUDIES_OBSERVATIONS. Dans le panneau *Details* sur la droite, renseignez les différents paramètres : 
- DBServerURL : http://138.102.159.37:8080/openSilexTestAPI/rest 
- studies : http://www.phenome-fppn.fr/test/DMO2019-6 
- variables : all 
- login : admin@opensilex.org 
- password : 21232f297a57a5a743894a0e4a801fc3 


La 2ème étape consiste à convertir la sortie du dataminer en fichier CSV 
Cliquez sur le *tool* *CSV extractor* dans la rubrique Data Miner.

La 3ème étape va utiliser l'algorithme DataMiner que vous avez créé.
Cliquez sur le tool *test_data*.

Reliez les 3 noeuds.
Cliquez sur  puis *save* 
Cliquez sur   puis *run*

### Publier ses données dans le catalogue

#### Publier des données dans le catalogue  


#### Rechercher des données via le semantic search
*Non disponible pour le moment*

### Le partage de fichiers
Déplacer fichier dans espace commun

### L'envoi de messages
Informez les membres du VRE les membres du VRE de l'ajout d'un nouveau dataset en ajoutant un message dans le fil d'actualités. Vous pouvez taguer une personne en particulier en utilisant *@*

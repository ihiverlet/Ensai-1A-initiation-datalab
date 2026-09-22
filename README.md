
# Découverte du Datalab

⚠️

Ceci est une vieille version. pour la version la plus récente, rdv : https://ihiverlet.github.io/Ensai-1A-initiation-datalab/

⚠️



## Introduction 
<details>
Le Datalab permet aux statisticiens de découvrir, d'expérimenter, d'apprendre, de se former aux outils de la data.

### Pourquoi un Datalab ? 
#### Une réponse à un besoin
Dans le monde professionnel, plusieurs problèmes se posent au statisticien :

- sa machine n'est pas assez puissante
- des problèmes de réplicabilité (le fameux ça marche sur mon ordi!)
- besoin de connaissances spécifiques pour installer des logiciels
...

À l'INSEE, un projet est né pour pallier à ce besoin : [Onyxia](https://www.onyxia.sh/). L'Insee met une instance de ce projet à disposition des administrations publiques et écoles : le [SSP Cloud](https://datalab.sspcloud.fr/).
Vous avez également accès à une seconde instance d'Onyxia gérée par le GENES. N'hésitez pas à créer un compte sur ces deux plateformes. Ces instances sont administrées par différentes équipes et proposent une offre de service différente. En cas de problème vous avez différents canaux de communication :
pour le sspcloud : il faudra vous créer un compte slack
pour l'instance du denes: vous avez un canal teams dédié

A noter, tout le [code](https://github.com/InseeFrLab/onyxia). est opensource (ie: droit en lecture, libre redistribution du code, modification du code et utilisation du code). Ainsi, n'importe qui peut installer son propre datalab en se basant sur Onyxia ! 

#### Des concepts
Derrière Onyxia se cachent plusieurs concepts: l'utilisation de technologies cloud natives, avoir une infrastructures qui permet d'avoir des ressources de calculs (CPU, RAM, GPU) et de stockage à disposition, avoir une interface graphique pour simplifier la vie des utilisateurs... Grâce à Onyxia, un data scientists n'a pas besoin de connaissances spécifiques (Docker, Kubernetes, Helm, S3... ) pour obtenir un environnement de travail fonctionnel. La plateforme se présente comme un bac à sable et permet notamment de tester de nouvelles technologies et de se former en se concentrant sur le contenu plutôt que sur la configuration d'un environnement de travail. D'ailleurs vous utiliserez les datalabs au cours de vos prochains tp :)
Les datalabs donnent aux utilisateurs la possibilité de lancer de nombreux services préconfigurés à la demande (Jupyter, Rstudio, VSCode, PostgreSQL... et pleins d'autres n'hésitez pas à regarder !) avec une puissance de calcul adaptée aux besoins.
L'utilisateur n'a pas besoin de connaissances spécifiques pour lancer un service mais s'il le désire, il peut se former : toutes les commandes que vous pourriez exécuter en ligne de commande sont visibles dans l'interface. 
Les choix faits dans Onyxia sont conditionnés par le fait qu'il ne faut pas s'enfermer, le but est de rendre le logiciel facultatif. L'idée étant qu'il ne faut pas s'enfermer dans un choix technologique ni qu'il soit couteux d'en sortir.

:warning:
Ne déposez *jamais* de données sensibles sur le sspcloud ou l'instance du GENES ! D'ailleurs, il n'y a aucune garantie de service sur le sspcloud : la plateforme peut tomber en panne, il peut y avoir des attaques... donc soyez vigilants à vos usages.

Pour les fonctionnaires, une autre instance nommée LS3 (accessible en interne et coupée d'internet) permet l'utilisation de données sensibles.
Pour les ingénieurs, vous retrouverez peut-être d'autres instances d'onyxia sur vos futurs postes ;) 

NB: On distinguera 3 notions primordiales au cours du tp : l'environnement d'exécution du code, le stockage des données et la sauvegarde du code

</details>

## Objectifs 

Ce TP d'initiation vous permettra de faire vos premiers pas sur la plateforme :
 
- Lancer vos premiers services  
- Configurer votre compte sur le datalab  
- Vous familiariser avec l'espace de stockage S3  
- Sauvegarder votre code, vos données  
- Adopter de **bonnes pratiques** et **ne pas perdre votre travail** 😇

## Créer un compte

Vous pouvez réaliser ce TP soit sur :

- Le [Datalab du GENES](https://onyxia.lab.groupe-genes.fr/)
- Le [Datalab SSPCloud de l'INSEE](https://datalab.sspcloud.fr/)
  - Pour la création de compte, utilisez votre mail ENSAI prenom.nom@eleve.ensai.fr

## Lancer un service
<details>

### Différents catalogues de services

- [ ] Allez dans `Catalogue de services`

Vous trouverez différents catalogues : que ce soit pour les environnements de développement intéractifs (IDE), les bases de données, de la datavisualisation...
Cette année vous vous servirez principalement des services IDE et bases de données. Mais n'hésitez pas à faire un tour sur les autres catalogues tout au long de votre scolarité !

### Un premier service

- [ ] Sélectionnez le service de votre choix *Vscode-python* ou *Jupyter-python* puis cliquez sur `Lancer`

Vous obtiendrez un formulaire vous laissant de multiples options pour configurer votre service. Pour une expérience "de base", ne les modifiez pas et cliquez sur "lancer".
Attendez quelques secondes le temps que le service se lance. Lisez bien la note qui s'affiche à l'écran ! Elle contient des informations essentielles comme vos identifiants de connection par exemple.  

- [ ] Cliquez pour copier le mot de passe
- [ ] Cliquez sur `Ouvrir le service` :rocket:
  - password : collez le mot de passe

Votre service s'ouvre. Vous pouvez alors commencer à coder 😄
</details>

## Configurer son service
<details>

Maintenant que nous savons lancer un service, revenons un petit peu en arrière et intéressons nous au formulaire présent lors du lancement du service. (Onglet 'Catalogue de services' et sélectionner un service vscode-python par exemple)

* Onglet *Service* : Ici, vous disposez de la possibilité de choisir la version de python que vous souhaitez utiliser

* Onglet *Resources(CPU/RAM)* : vous choisissez les ressources dont disposera votre service. Notamment, vous choisissez les ressources qui seront garanties au lancement du service (requests) et les ressources qui pourront être utilisées au maximum par votre service (limits).  
CPU (processeur) : il s'agit de la puissance de calcul allouée au service. Les CPU exécutent les instructions (ouvrir un programme, calculer, afficher des résulats) 
RAM (mémoire vive): il s'agit de la mémoire de travail du service, elle garde temporairement ce que le service utilise pendant l'exécution: les dataframes, modèles, images... Elle n’est pas persistante : si le service s’arrête, la RAM est vidée (les fichiers survivent s’ils sont sur le volume persistant).

* Onglet *Configuration for persistence* : détermine la taille du disque de travail “qui survit” quand le service est "fermé". Sans persistance, les services tournent dans des conteneurs éphémères : tout ce qui est seulement dedans peut disparaître à l’arrêt. Avec la persistance, un volume de stockage est attaché à ta session et conserve tes fichiers jusqu'à la désinstallation du service.
</details>

## Premiers pas dans un service
<details>

- [ ] Créez un Notebook Python (fichier .ipynb)
- [ ] Vérifiez que tout fonctionne bien, écrivez et exécutez une fonction python de votre choix, créez des dossiers, des fichiers, les renommer, supprimer, déplacer...

Un terminal est un outil qui vous permet de communiquer avec votre machine en lignes de commande. Ainsi, vous écrivez des commandes (instructions) dans une fenêtre que la machine exécutera. Vous pouvez donc utiliser un terminal pour exécuter du code, manager vos fichiers, installer des outils, des packages, ...  

Sur le sspcloud, le terminal utilise Bash (un des langages les plus courants). Apprendre quelques commandes de base vous simplifiera la vie.

- [ ]  Ouvrir un terminal : dans le menu, View → Terminal 
  - savoir où vous vous situez: `pwd` (print work directory)
  - lister les fichiers : `ls` (list)
  - créer un dossier : `mkdir mon-dossier` (make directory)
  - se déplacer dans le fichier : cd `mon-dossier` (change directory)
  - créer un fichier : `touch mon-fichier`
  - suprimer un fichier: `rm mon-fichier` (remove)
  - installer un package : `uv add my-package`, `pip install my-package` ...

- [ ] Fermer la fenêtre, fermer le navigateur... Pas de panique, retrouvez votre service (dans le volet "Mes services" sur le datalab)

Imaginons que vous aviez des tâches spécifiques à réaliser et que votre travail est fini, vous supprimez votre service. Cela libère les ressources de calcul réservées. Où est votre code ?  💥 perdu, disparu, irrécupérable...

- [ ] Supprimer votre service
- [ ] Constater que le front cesse de fonctionner et ... que ce que vous aviez fait est perdu pour toujours

Pas de solution miracle, si ça vous arrive, il faudra tout recommencer. Comment éviter ça ? En sauvegardant votre code et vos données. 

Une option très rhébarbative et encourageant les erreurs serait de vous faire télécharger vos fichiers. Mais c'est très pénible surtout quand vous commencez à avoir beaucoup de fichiers et pleins de versions différentes.
Nous allons donc utiliser un outil dédié à la gestion de versions de code: git. Cet outils est d'autant plus utile qu'il facilite la collaboration sur un projet.
</details>

## Git
<details>

Git est un outil de gestion de versions. Vous l'utiliserez en complément d'une forge telle que [github](https://github.com/) ou [gitlab](https://about.gitlab.com/fr-fr/) qui permettra de stocker votre code. Git vous permettra d'avoir une gestion propre de vos fichiers et de naviguer dans l'historique de votre code, voir les modifications apportées au fil du temps etc. 
Vous aurez bientôt un cours dédié à git donc on ne rentrera pas dans les détails ici. 

NB : Le repo cloné dans la suite du tp est public et donc accessible à tous. Il se peut que vous ayez parfois besoin de travailler sur des repos privés. Il vous faudra donc renseigner un token qui permettra de vous authentifier. Pour vous éviter d'avoir à renseigner vos credentials à chaque fois que vous aurez besoin de vous authentifier, vous avez la possibilité de renseigner vos informations de connexion au sein du datalab dans l'onglet "Mon compte" > "Git". Les credentials définis seront alors injectés dans vos services sous forme de variable d'environnement.

- [ ] Se rendre dans l'onglet "Mon compte" puis l'onglet "Git"
Bonus : Ajouter ses données d'authentification et faire ses premiers pas avec git, voir la partie *bonus: aller plus loin avec git* ou la [doc relative à la configuration de git sur le sspcloud](https://docs.sspcloud.fr/content/version-control.html#cr%C3%A9er-un-jeton-dacc%C3%A8s-token)

- [ ] Cloner le repo du TP
- [ ] Afficher les différentes contributions 

Dans un terminal, effectuer les commandes suivantes : 
```
git clone <le TP> # Vous obtenez une copie du code dans un dossier correspondant au nom du projet cloné
cd <le TP> # Vous vous déplacez au sein du dossier contenant le code
git log --oneline
```
Vous venez de créer une copie en local du repo distant et d'afficher l'historique des contributions au projet

NB: Il est aussi possible de réaliser ces étapes en passant par l'interface (*Source Control* symbole sur la gauche avec des branches)

- [ ] Configurer un nouveau service à son lancement (onglet "Git") pour que le repo soit cloné directement 

Comment synchroniser ce que vous avez en local ? et à distance ? La réponse début octobre. Et si vous êtes curieux, n'hésitez pas à [lire "le tuto" & les "formations" sur le sujet](https://www.sspcloud.fr/catalog?path=Bonnes%E2%90%A3pratiques%E2%90%A3de%E2%90%A3d%C3%A9veloppement%E2%90%A3avec%E2%90%A3Git%E2%90%A3et%E2%90%A3R) et à faire la partie bonus suivante.


</details>

## Bonus : Aller plus loin avec Git 
<details>

### Générer un token GitHub

Si vous avez déjà généré et déclaré un jeton GitHub, inutile de refaire ces 2 étapes.

- [ ] Connectez-vous à votre compte GitHub
- [ ] Allez dans settings :arrow_right: Developer settings :arrow_right: Personal access tokens :arrow_right: Tokens (classic)
- [ ] Générez un [nouveau jeton classique](https://github.com/settings/tokens/new)
  - Renseigner : 
    - nom du token : Datalab GENES
    - date d'expiration :arrow_right: Custom :arrow_right: 1 an
  - :white_check_mark: Cochez repo
  - Cliquez sur [Generate token]{.green-button}
  - Copiez ce jeton commençant par `ghp_` et gardez le précieusement de côté quelques minutes

:warning: 
- Ce jeton ne sera visible qu'une seule fois
- si vous le perdez ou s'il est expiré, il faut en générer un nouveau


### Déclarer votre jeton

GitHub vous a fournit un jeton. Il faut maintenant le déclarer sur le Datalab :

- [ ] Allez dans `Mon Compte` :arrow_right: Onglet `Git`
- [ ] Renseignez les informations suivantes 
  - nom d'utilisateur Git 
  - mail (celui utilisé pour votre compte GitHub)
- [ ] Collez votre token

Vous pouvez maintenant échanger du code entre les services du Datalab et vos dépôts GitHub. :tada:


### Dépôt pour le code

Avant de créer un service, nous allons créer un dépôt GitHub qui permettra de sauvegarder votre code.

- [ ] Dans GitHub, créer un [nouveau Repository](https://github.com/new)
  - Repository name : TP-datalab
  - Private
  - :white_check_mark: Cochez *Add a README file*
  - .gitignore template : Python
  - [Create Repository]{.green-button}
- [ ] Sur la page de votre repo, cliquez sur le bouton [Code]{.green-button}
- [ ] Copiez l'adresse *https* du repo


### Branchez votre service sur un répo

Lors du lancement d'un *Service*, vous pouvez vous brancher sur un répo git. Ainsi le contenu de votre dépôt sera importé dans votre service.

Vous pourrez alors utiliser le code de votre dépôt et éventuellement le mettre à jour en effectuant un *push*.

Lancez un service *Jupyter Notebook*

- [ ] Ouvrez la Configuration
  - De nombreux onglets permettent de configurer votre service
  - Service : possibilité d'utiliser une autre image Docker
  - Resources : choisir CPU et RAM
  - Init : script à lancer au démarrage
- [ ] Allez dans l'onglet `Git` et collez l'adresse *https* du repo dans la case *Repository url*
- [ ] `Lancez` le service, puis attendez quelques secondes


### Sauver son code

- [ ] Sur Jupyter, ouvrez un terminal
  - File :arrow_right: New :arrow_right: Terminal
- [ ] Positionnez-vous dans le repo : `cd /home/onyxia/work/TP-datalab/`
- [ ] `git status` pour voir l'état actuel
  - le fichier *ex0.ipynb* doit apparaître dans les *Untracked files*
- [ ] Ajoutez ce fichier à l'index
- [ ] Créez un commit
- [ ] Poussez ce commit vers votre dépôt distant (GitHub)
  - Vous pouvez vérifier sur GitHub que votre fichier *ex0.ipynb* est bien présent

- `git add .` ## Attention, à utliser avec précaution
- `git commit -m "création fichier tp"`
- `git push`


Vous savez désormais lancer des services et enregistrer votre code. Mais en tant que data scientist le coeur de métier ce sont... les données !
Comment les importer et les sauvegarder après des traitements informatiques ?

</details>

## Stockage S3
<details>

Les datalabs vous proposent de stocker vos données sur un espace dédié à cet effet en utilisant S3 (Simple Storage System). S3 est un **protocole de stockage objet** dérivé du service initialement offert par le cloud provider AWS.  

Vous aurez toujours besoin des deux éléments suivants : 
- URL de base du serveur S3 hébergé sur le sspcloud : https://minio.lab.sspcloud.fr  
- Nom du bucket auquel vous souhaitez accéder; si vous souhaitez accéder à votre bucket personnel, il s'agit de votre nom d'utilisateur sur le sspcloud 

Un bucket correspond en gros à un dossier à la racine du serveur S3. Les buckets permettent de séparer les usages, les permissions, les quotas ... En fonction du serveur S3 que vous utilisez et des permissions que vous avez, vous pouvez avoir accès à tout ou partie d'un ou plusieurs buckets.

### Authentification

A part pour l'accès aux données explicitement rendues publiques (la gestion de la visibilité et des permissions sur les fichiers se fait en général via un système de policies qui n'est pas abordé ici), il faudra des informations d'authentification (credentials) pour communiquer avec l'API s3.  
Ces credentials sont constitués d'un duo `access key` & `secret key` (login / mot de passe) pour les comptes de service et d'un trio `access key`, `secret key`, `session token` pour les identités temporaires (credentials personnels, expirant au bout d'un certain temps).  

Pourront être utilisées les variables d'environnements suivantes, généralement reconnues par les bibliothèques standards S3 :

AWS_ACCESS_KEY_ID=my_access_key
AWS_SECRET_ACCESS_KEY=my_secret_key
AWS_SESSION_TOKEN = my_session_token
ENDPOINT_URL = s3_endpoint

Pour récupérer vos informations d'authentification, vous pouvez vous rendre sur 
- SSPCLOUD : onglet my account > Connect to storage et sélectionner `shell environment variable`

### Un client pour communiquer avec S3

Afin de simplifier les intéractions avec l'API S3, nous allons utiliser un client s3. 

Des exemples de clients s3 en ligne de commande :  

- [mc](https://min.io/docs/minio/linux/reference/minio-mc.html) (minIO Client) : compatible pour tout service compatible s3
- [aws cli](https://aws.amazon.com/cli/) : outil officiel pour intéragir avec Amazon S3

Il existe évidemment des interfaces graphiques ainsi que des bibliothèques (SDK) pour tous les langages.  
Vous êtes libres d'utiliser le client S3 de votre choix, en fonction de vos préférences.  
Dans la suite on illustrera à partir du client `mc` préconfiguré sur le datalab.  


### Cas d'usages et limites  

S3 (et plus généralement le stockage objet) est parfait pour un certain nombre d'usages mais pas tous.  
Les principales limitations sont les suivantes :  

- **L'écriture partielle n'est pas possible** : un fichier ne peut pas être modifié. La moindre modification (y compris renommage) correspond à la réécriture complète du fichier  
- **La latence est plus forte que pour un stockage block / fichiers classique** : il n'est donc pas adapté pour des systèmes ayant besoin d'une latence faible comme les bases de données relationnelles  

Du coup on en tire quelques leçons :  

- Write once, read many (WORM): S3 est particulièrement adapté à ce pattern. Parfait pour les backups, les logs, les ressources statiques, la diffusion des repertoires
- S3 n'a pas vocation à remplacer entièrement les stockages block / fichiers existants mais à venir en complément pour les bons cas d'usage

#### Aller plus loin 

https://github.com/InseeFrLab/ecosysteme-data/tree/main/source/s3
https://docs.sspcloud.fr/content/storage.html
https://pythonds.linogaliana.fr/content/modern-ds/s3.html#les-donn%C3%A9es-sur-le-cloud


#### Revenons au TP
Lorsque l'on travaille dans le cloud, il est essentiel de **séparer les données des programmes** pour :

- mieux gérer les ressources
- renforcer la sécurité en limitant les accès et les permissions
- permettre une scalabilité indépendante des composants
- Un même code peut tourner sur plusieurs jeux de données. 

### Votre bucket
Un **bucket** est un conteneur dans lequel on stocke des objets (fichiers et métadonnées) dans des systèmes de stockage de type cloud. Il facilite l'organisation, la gestion des permissions et l'accès aux données.

Lors de votre création de compte, un bucket est créé avec votre nom d'utilisateur. Dans ce bucket, vous pouvez :

- créer / supprimer des dossiers
- importer / supprimer des fichiers

Vous avez plusieurs possibilités pour gérer votre stockage :

- Depuis le Datalab, onglet *Mes fichiers*
- Depuis un terminal avec un client comme le client Minio `mc`


### Stocker vos fichiers

- [ ] Téléchargez ce fichier [parquet](data/my-file.parquet)

Ensuite, allez sur la page d'accueil du Datalab :

- [ ] Allez dans `Mes fichiers`
- [ ] Créez un dossier `initiation` par exemple (organiser vos données comme vous le souhaitez !)
- [ ] Téléversez votre fichier *parquet* dans le dossier `initiation`

Vous remarquerez à droite, un encadré vert avec des lignes de commande du type `mc cp my-file.parquet s3/<username>/initiation/my-file.parquet`.

Ce sont des commandes pour interagir avec votre stockage depuis un terminal (voir ci-après).

Cependant, vous pouvez extraire de ces commandes une information intéressante : le chemin vers votre fichier : `s3/<username>/initiation/my-file.parquet`.

- [ ] Visualisez les données grâce à l'explorateur de données 

### Client MinIO

Le [client MinIO](https://min.io/docs/minio/linux/reference/minio-mc.html) `mc` installé, configuré et utilisable depuis le terminal permet également d'interagir avec vos fichiers.

Ouvrez un terminal (File :arrow_right: New :arrow_right: Terminal):

- [ ] `mc ls s3/<username>/` : pour lister le contenu de votre dossier
- [ ] `mc cp s3/<username>/initiation/my-file.parquet .` : pour copier le fichier depuis s3 dans votre dossier courant 
  - le fichier apparait dans votre explorer
- [ ] Supprimez ce fichier car importer les fichiers de données dans son espace de travail n'est pas une bonne pratique : `rm my-file.parquet`

La commande `mc --help` liste toutes les commandes possibles (ESPACE pour défiler, CTRL+C pour sortir)


### Utiliser des données

Sur la page d'accueil du Datalab :

- [ ] Allez dans `Mon Compte`, puis dans l'onglet `Connexion au Stockage`

Vous trouverez ici des informations pour vous connecter au stockage selon le language que vous utilisez : Python, R...
D'ailleurs pour chaque langage, il y a même plusieurs packages qui font le job. Par exemple *s3fs* ou *boto3* pour Python.

Retournez dans votre service Notebook Jupyter :

- [ ] Créez un nouveau Notebook
  - vous pouvez par exemple le nommer `S3.ipynb`
- [ ] Créer des cellules, puis collez, comprenez et exécutez les blocs de code ci-dessous.

Commencez par importer les packages nécessaires et récupérer les valeurs des variables d'environnement pour pouvoir vous connecter à votre stockage.

```python
import os

s3_endpoint = f'https://{os.environ["AWS_S3_ENDPOINT"]}'
s3_access_key = os.environ["AWS_ACCESS_KEY_ID"]
s3_secret_access_key = os.environ["AWS_SECRET_ACCESS_KEY"]
s3_session_token = os.environ["AWS_SESSION_TOKEN"]
s3_region = os.environ["AWS_DEFAULT_REGION"]

```

:warning:
Les clés et les jetons ont une durée de vie limitée. Si vous laissez votre service ouvert trop longtemps (à éviter !), vos clés et jetons pourraient être expirés.
Dans ce cas, vous devrez recharger des nouvelles valeurs (voir Mon Compte > Connexion au Stockage).

Définissez le chemin où se trouve votre fichier et lisez le avec pandas.

Rappel : Vous ne devriez jamais écrire vos mots de passe dans le code, utilisez des variables d'environnement à la place !  


De plus, les noms de ces variables d'environnement correspondent aux variables reconnues par la plupart des librairies. Ainsi, pour lire un fichier csv, il vous suffit d'écrire le code suivant :

```python
df = pd.read_csv("s3://inesh/diffusion/airports_fr.csv")

```
Si vos services n'étaient pas correctement configurés, vous devriez plutôt écrire le code suivant :

```python

import os, pandas as pd

storage_opts = {
    "key": os.environ["AWS_ACCESS_KEY_ID"],
    "secret": os.environ["AWS_SECRET_ACCESS_KEY"],
    "token": os.environ.get("AWS_SESSION_TOKEN"), 
    "client_kwargs": {
        "region_name": "eu-west-1",
        "endpoint_url": "https://minio.lab.sspcloud.fr"
    }
}
df = pd.read_csv("s3://inesh/diffusion/airports_fr.csv", storage_options=storage_opts)

```

Ou bien, en créant un filesystem:

```python
import os, s3fs, pandas as pd

# Create filesystem object
S3_ENDPOINT_URL = "https://" + os.environ["AWS_S3_ENDPOINT"]
fs = s3fs.S3FileSystem(client_kwargs={'endpoint_url': S3_ENDPOINT_URL})

# Lister les objets d'un bucket
fs.ls("donnees-insee")

# Importer des données

BUCKET = "donnees-insee"
FILE_KEY_S3 = "diffusion/BPE/2019/BPE_ENS.csv"
FILE_PATH_S3 = BUCKET + "/" + FILE_KEY_S3

with fs.open(FILE_PATH_S3, mode="rb") as file_in:
    df_bpe = pd.read_csv(file_in, sep=";")

# Exporter des données

BUCKET_OUT = "<mon_bucket>"
FILE_KEY_OUT_S3 = "mon_dossier/BPE_ENS.csv"
FILE_PATH_OUT_S3 = BUCKET_OUT + "/" + FILE_KEY_OUT_S3

with fs.open(FILE_PATH_OUT_S3, 'w') as file_out:
    df_bpe.to_csv(file_out)

```

Dans tous les cas, votre **guide de survie** pour lire des données (autre qu'une bonne recherche google) se trouve ici : https://www.sspcloud.fr/document?path=SSPCloud%E2%90%A3Documentation%E2%80%BAUsing%E2%90%A3the%E2%90%A3Datalab%E2%80%BAData%E2%90%A3storage


### Données d'autres utilisateurs

Ce fichier est stocké sur le bucket d'un autre utilisateur à l'adresse suivante :

- SSP Cloud : `s3://inesh/diffusion/airports_fr.parquet`

Malheureusement, la fonctionnalité n'est pas encore implémentée sur le Datalab du GENES. Les dossiers *diffusion* de chaque utilisateur ne sont pas accessibles en lecture. Il faudra les rendre accessibles soi-même.

À la racine de votre Bucket, vous pouvez créer un dossier nommé `diffusion`.

Vous pourrez alors stocker à l'intérieur les dossiers et fichiers que vous souhaitez partager aux autres utilisateurs. Ils auront un droit d'accès en lecture sur votre dossier *diffusion*.

De la même façon, vous pouvez rendre un fichier accessible aux autres utilisateurs depuis l'interface (symbole oeil) ou en ligne de commande en utilisant mc et obtenir un lien de téléchargement.


### Exportez vos résultats vers MinIO

Vous pouvez également exporter vos fichiers vers S3.

Nous allons utiliser ici la librairie [s3fs](https://s3fs.readthedocs.io/).

- [ ] utilisez le code suivant en veillant à bien rempacer le nom du bucket, l'emplement où vous souhaitez écrire votre fichier.

```python
import os, s3fs

# Create filesystem object
S3_ENDPOINT_URL = "https://" + os.environ["AWS_S3_ENDPOINT"]
fs = s3fs.S3FileSystem(client_kwargs={'endpoint_url': S3_ENDPOINT_URL})

BUCKET_OUT = "<mon_bucket>"
FILE_KEY_OUT_S3 = "initiation/output.csv"
FILE_PATH_OUT_S3 = BUCKET_OUT + "/" + FILE_KEY_OUT_S3


# Exemple si on souhaite exporter le dataframe df_bpe
with fs.open(FILE_PATH_OUT_S3, 'w') as file_out:
    df_bpe.to_csv(file_out)
```

- [ ] Sur le Datalab, allez dans `Mes fichiers` > `initiation`
  - le fichier *output.csv* a été généré
  - rafraichissez la page si besoin
- [ ] Double-cliquez sur ce fichier pour en avoir un aperçu



#### Un dernier exemple : TODO A FINALISER

``` python
  import pandas
  df = pandas.read_csv('FD_INDREG_2015.txt', sep=';', nrows=10)
  df.to_csv('FD_LOGEMT_2015_first_10.csv', sep=',')

read_csv charge en mémoire (BTW : mémoire vs disque) permettant traitements rapides
to_csv écrit le fichier sur disque

  
time python -c "import pandas; pandas.read_csv('FD_INDREG_2015.txt', sep=';').to_csv('FD_INDREG_2015.csv', sep=',')"


rm FD_INDREG_2015.txt
python
  import pandas
  df = pandas.read_csv('s3://donnees-insee/diffusion/RP/2015/FD_INDREG_2015.txt', sep=';', nrows=10)
-> ça va vite, pas d'espace disque requis
  df.to_csv('s3://bucket/FD_INDREG_2015.csv', sep=',')
```

Vous avez créé un processus réplicable, qui traite un fichier sur S3 et écrit le résultat sur S3

</details>


## Behind the scene
<details>

Onyxia injecte des variables d'environnement afin de vous proposer un environnement préconfiguré.

Pour accéder à ces variables: 
- depuis un terminal 
```
env   #beaucoup beaucoup beaucoup de choses
env | grep AWS    # toutes les variables d'environnement qui contiennent AWS
echo $AWS_ACCESS_KEY_ID   # affiche la valeur de la variable d'environnement
```
- avec python
```python
  import os
  os.environ
```
- avec R 
```r
Sys.getenv()
```
Les variables d'environnement sont accessibles à tous les programmes qui tournent sur le service.
</details>

## Configurer son service 

Comme nous l'avons vu plus tôt, il peut être utile de configurer son service
- CPU/RAM/Persistence
- Variable d'env : pour en ajouter si besoin
- S3 config : injection de variable d'env pour faire marcher S3
Onyxia retient ces paramètres pour vous
- Git

-> vous pouvez les retrouver et/ou les modifer dans "Mon compte"


## Bonus
<details>

### Surveiller son service

- [ ] Sur la page du Datalab, allez dans `Mes services`
- [ ] Cliquez sur le nom du service (Jupyter-python)
- [ ] Cliquez sur `Surveillance externe`

Vous arrivez sur la page de l'outil **Grafana** qui permet d'observer les métriques de votre service.


### Les secrets

::: {.callout-important title="Enigme du Père Fouras" icon="false"}
Plus j'ai de gardiens, moins je suis gardé.

Moins j'ai de gardiens, plus je suis gardé.

Qui suis-je ?
:::

Certains éléments ne doivent pas être diffusés dans votre code (jetons d'accès, mots de passe...).

Pour éviter d'avoir à nettoyer votre code à chaque fois que vous le poussez sur GitHub, le datalab propose de gérer vos secrets.

#### Créer un secret

- [ ] Allez dans *Mes secrets*
- [ ] Créez un `Nouveau secret` nommé *projet_patate*
- [ ] Double-cliquez pour ouvrir ce secret
- [ ] `Ajoutez une variable`
  - Nom : PATATE_TOKEN
  - Valeur : 123456
  - Cliquez sur :white_check_mark: pour valider
- [ ] Ajoutez une autre variable
  - Nom : PATATE_PORT
  - Valeur : 5236
  - Cliquez sur :white_check_mark: pour valider

#### Utiliser dans un service

- [ ] Préparez le lancement d'un service Rstudio
- [ ] Dans la configuration, allez dans l'onglet `Vault`
- [ ] secret : *projet_patate*
- [ ] Lancez le service

Dans votre servives, les deux variables d'environnement ont été créées. 

- [ ] Vérifiez leur présence via le terminal : `env | grep PATATE` ou `echo $PATATE_TOKEN`
- [ ] Ouvrez un notebook et récupérez la valeur de *PATATE_TOKEN*
  ```{.python}
  import os

  token = os.environ["PATATE_TOKEN"]
  print(token)
  ```
- [ ] Une fois que vous avez fini de jouer, supprimez votre service

### Personnaliser son service

- Utiliser un script d'initialisation
- Utilser sa propre image Docker

</details>

## Libérer les ressources 

Une fois vos travaux terminés, il est temps de libérer les ressources réservées.

- [ ] N'oubliez pas d'enregistrer votre code (git)
- [ ] N'oubliez pas d'enregistrer vos données (s3)
- [ ] Puis sur la page d'accueil, allez dans *Mes services*, mettez votre service à la poubelle 

Vous pouvez aisément reproduire votre travail plus tard :

- Votre code est téléchargé
- Vos données sont toujours sur MinIO
- Il suffit de relancer un nouveau service et de relancer les calculs


## Besoin d'assistance ? 

- Contactez l'équipe du SSP Cloud sur [Slack](https://join.slack.com/t/3innovation/shared_invite/zt-1bo6y53oy-Y~zKzR2SRg37pq5oYgiPuA){target="_blank"}
- Pour le Datalab du GENES, vous trouverez sur la page d'accueil un lien pour rejoindre le canal Teams


### Bibliographie 
- TP basé sur https://github.com/ludo2ne/ENSAI-1A-SQL/blob/main/doc/tp/tp3.qmd et https://github.com/InseeFrLab/ecosysteme-data

- [Le SSPCLOUD : une fabrique créative pour accompagner les expérimentations des statisticiens publics](https://hal.science/hal-04263723v1/document)

- [Utiliser RStudio sur l’environnement SSP Cloud](https://book.utilitr.org/01_R_Insee/Fiche_utiliser_Rstudio_SSPCloud.html), UtilitR
- [Formations et tutoriels du SSP Cloud](https://www.sspcloud.fr/formation)
  - Nombreux tutos : Python, R, ML, Spark, Cartographie 
- [Doc SSP Cloud](https://docs.sspcloud.fr/)
- [Principes du Datalab](https://docs.sspcloud.fr/content/principles.html)


### Pour aller plus loin 

Nous n'avons pas vraiment eu l'occasion de parler des dessous de la plateforme. Elle est construite sur un cluster Kubernetes. Et vous avez la possibilité d'interragir avec kubernetes en ligne de commande. Je vous laisse découvrir comment ça marche ici : https://github.com/olevitt/kubernetes



# Travaux Pratiques : Introduction à PySpark

## Objectif

Ce TP vise à vous familiariser avec PySpark, l'interface Python pour Apache Spark, en explorant ses principales fonctionnalités à travers des définitions, des exemples pratiques et des exercices approfondis.

## Introduction à PySpark

### Qu'est-ce que PySpark ?

PySpark est l'API Python pour Apache Spark, un moteur de traitement de données distribué conçu pour traiter et analyser de grandes quantités de données de manière efficace. PySpark permet aux utilisateurs d'écrire des scripts en Python pour interagir avec les fonctionnalités de Spark, facilitant ainsi le traitement parallèle et distribué des données.

### Avantages de PySpark

- **Scalabilité** : Capable de traiter des pétaoctets de données en distribuant le traitement sur plusieurs nœuds.
- **Vitesse** : Utilise le traitement en mémoire pour accélérer les calculs par rapport aux systèmes basés sur le disque.
- **Polyvalence** : Supporte divers langages de programmation, notamment Python, Scala, Java et R.
- **Communauté active** : Bénéficie d'une large communauté open-source, offrant une multitude de ressources et de bibliothèques.

## Concepts Clés de PySpark

### Resilient Distributed Dataset (RDD)

Les RDDs sont la structure de données fondamentale de Spark. Ils représentent une collection immuable et distribuée d'objets pouvant être traités en parallèle. Les RDDs offrent des opérations de transformation (comme `map`, `filter`) et des actions (comme `collect`, `count`) pour manipuler les données.

**Exemple** :

```python
from pyspark import SparkContext

sc = SparkContext("local", "Exemple RDD")
data = [1, 2, 3, 4, 5]
rdd = sc.parallelize(data)
rdd_squared = rdd.map(lambda x: x ** 2)
print(rdd_squared.collect())  # Résultat : [1, 4, 9, 16, 25]
```

## DataFrame

Un DataFrame est une abstraction de haut niveau au-dessus des RDDs, similaire à une table dans une base de données relationnelle ou à un DataFrame en pandas. Il permet des opérations optimisées sur des données structurées avec des noms de colonnes et des types de données.

**Exemple :**

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("Exemple DataFrame").getOrCreate()
data = [("Alice", 34), ("Bob", 45), ("Catherine", 29)]
df = spark.createDataFrame(data, ["Nom", "Âge"])
df.show()
```

**Résultat:**

```bash
+---------+---+
|      Nom|Âge|
+---------+---+
|    Alice| 34|
|      Bob| 45|
|Catherine| 29|
+---------+---+
```

## Dataset

Les Datasets sont similaires aux DataFrames mais offrent une vérification des types à la compilation et sont disponibles uniquement dans les langages à typage statique comme Scala et Java. En Python, les DataFrames sont utilisés à la place des Datasets.

# Installation et Configuration de PySpark

1. Installation de Java : PySpark nécessite Java. Assurez-vous que Java est installé en exécutant java -version dans votre terminal. Si ce n'est pas le cas, téléchargez-le depuis le site officiel d'Oracle.
2. Installation de PySpark : Installez PySpark via pip :
    ```bash
    pip install pyspark
    ```
3. Vérification de l'installation :
   ```python
   import pyspark
   print(pyspark.__version__)
   ```
   Cela devrait afficher la version de PySpark installée.

# Exercices Pratiques

Les exercices suivants sont conçus pour renforcer votre compréhension de PySpark. Ils sont classés par difficulté croissante et devraient vous occuper pendant une journée complète.

## Exercice 1 : Création et Manipulation de RDDs
Objectif : Créer un RDD à partir d'une liste de nombres entiers et effectuer les opérations suivantes :
- Filtrer les nombres pairs.
- Calculer le carré de chaque nombre filtré.
- Calculer la somme des nombres obtenus.

## Exercice 2 : Opérations de Base sur les DataFrames
Objectif : Créer un DataFrame à partir d'une liste de tuples contenant des informations sur des employés (nom, département, salaire). Effectuer les opérations suivantes :
- Afficher le schéma du DataFrame.
- Filtrer les employés dont le salaire est supérieur à 50 000.
- Calculer le salaire moyen par département.

## Exercice 3 : Chargement de Données à Partir d'un Fichier CSV
Objectif : Charger un fichier CSV contenant des informations sur des produits (ID, nom, catégorie, prix) dans un DataFrame et effectuer les opérations suivantes :

- Afficher les 5 premières lignes.
- Filtrer les produits appartenant à une catégorie spécifique.
- Calculer le prix moyen des produits par catégorie.

## Exercice 4 : Utilisation de Fonctions UDF (User Defined Functions)
Objectif : Créer une fonction personnalisée qui ajoute une colonne indiquant si le prix d'un produit est "Élevé" ou "Bas" en fonction d'un seuil donné. Appliquer cette fonction au DataFrame de l'exercice 3.

## Exercice 5 : Jointure de Deux DataFrames
Objectif : À partir de deux DataFrames, l'un contenant des informations sur des commandes (ID commande, ID client, montant) et l'autre sur des clients (ID client, nom, pays), effectuer une jointure pour obtenir le nom et le pays du client pour chaque commande.

## Exercice 6 : Agrégation et Groupement
Objectif : Utiliser le DataFrame des commandes pour calculer le montant total des commandes par pays et trier les résultats par montant décroissant.

## Exercice 7 : Gestion des Valeurs Manquantes
Objectif : À partir d'un DataFrame contenant des valeurs manquantes, appliquer des techniques pour gérer ces valeurs, comme le remplacement par la moyenne ou la suppression des lignes concernées.

## Exercice 8 : Partitionnement et Optimisation
Objectif : Répartir un DataFrame volumineux en plusieurs partitions et observer l'impact sur les performances des opérations.

## Exercice 9 : Utilisation de Spark SQL
Objectif : Enregistrer un DataFrame en tant que table temporaire et exécuter des requêtes SQL pour extraire des informations spécifiques.

## Exercice 10 : Implémentation d'une Fonction de Fenêtre
Objectif : Utiliser les fonctions de fenêtre pour calculer le classement des employés par salaire au sein de chaque département.

# Partie II Installation de PySpark

## Exercice 1 : Mise en route

- Installer PySpark sur vos machines. PySpark est disponible dans les dépots Python
- Lancer la commande pyspark pour lancer pyspark en ligne de commande.
- Ouvrez la documentation de API Spark
- Lancer la commande suivante, le contenu de votre fichier texte doit s'afficher
    ```python
    rddStr = sc.textFile(CHEMIN_VERS_FICHIER_TEXTE)
    print(rddStr.collect());
    ```
- Téléchargez le jeu de données suivant : [worldcitiespop.txt](https://github.com/CODAIT/redrock/blob/master/twitter-decahose/src/main/resources/Location/worldcitiespop.txt.gz)
- Reagrdez la première ligne du fichier en utilisant la commande head.

## Exercice 2 : Nettoyage simple worldcitiespop

Ecrivez un programme python Spark qui nettoie le fichier "worldcitiespop.txt" pour ne conserver que les lignes valides. Par valide on considère uniquement les lignes avec une population donnée.

```python
rom pyspark import *
from math import *

sc = SparkContext()
```

## Exercie 3 : Statistique

Modifiez votre programme pour afficher les statistiques suivantes sur les populations des villes. (min, max, sum , average)

## Exercice 4 : Historgrammes

Modifiez votre programme pour calculer un histogramme de fréquences des populations des villes. Pour l'histogramme on choisira les classes d'équivalences en utilisant une échelle logarithmique. (classe 0, villes de taille [0..10[, classe 1 villes de taille [10..100[ ...).

## Exercice 5 : TopK

Modifiez votre programme pour calculer et afficher les 10 villes ayant la population la plus importantes.

## Exercice 6 : Re-cleaning

En analysant les résultats de l'exercice 5, on s'aperçoit que "Delhi" et "New Delhi" sont les mêmes villes. Proposez une solution pour enlever les doublons (différentes villes au même endroit) en ne conservant les villes de plus forte population en cas de superposition. Recalculez vos histogrammes etc... Vous devez obtenir le résultat suivant.

```bash
(count: 37774, mean: 56685.35026737963, stdev: 335272.73059020063, max: 31480498.0, min: 7.0)
[(0, 4), (1, 65), (2, 1324), (3, 14545), (4, 18456), (5, 3107), (6, 264), (7, 9)]
jp,tokyo,Tokyo,40,31480498,35.685,139.751389
cn,shanghai,Shanghai,23,14608512,31.045556,121.399722
in,bombay,Bombay,16,12692717,18.975,72.825833
pk,karachi,Karachi,05,11627378,24.9056,67.0822
in,delhi,Delhi,07,10928270,28.666667,77.216667
ph,manila,Manila,D9,10443877,14.6042,120.9822
ru,moscow,Moscow,48,10381288,55.752222,37.615556
kr,seoul,Seoul,11,10323448,37.5985,126.9783
br,sao paulo,S�o Paulo,27,10021437,-23.473293,-46.665803
tr,istanbul,Istanbul,34,9797536,41.018611,28.964722
ng,lagos,Lagos,05,8789133,6.453056,3.395833
mx,mexico,Mexico,09,8720916,19.434167,-99.138611
id,jakarta,Jakarta,04,8540306,-6.174444,106.829444
us,new york,New York,NY,8107916,40.7141667,-74.0063889
cd,kinshasa,Kinshasa,06,7787832,-4.3,15.3
eg,cairo,Cairo,11,7734602,30.05,31.25
pe,lima,Lima,15,7646786,-12.05,-77.05
cn,peking,Peking,22,7480601,39.928889,116.388333
gb,london,London,H9,7421228,51.514125,-.093689
co,bogota,Bogot�,34,7102602,4.649178,-74.062827
```

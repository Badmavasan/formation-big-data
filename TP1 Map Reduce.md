# TP : Mise en Place d'une Architecture MapReduce en Environnement Distribué

## Objectif Général

L'objectif de ce TP est de vous familiariser avec les concepts de traitement distribué à l'aide de l'algorithme MapReduce. Vous allez concevoir et implémenter, en Python, une solution qui permet de :
- Distribuer un fichier de données volumineux en segments.
- Envoyer ces segments à plusieurs machines (ou processus) de traitement.
- Appliquer une fonction **Map** pour effectuer un traitement partiel sur chaque segment.
- Collecter et agréger (via une fonction **Reduce**) les résultats partiels pour obtenir une sortie finale (par exemple, un comptage de mots).

Ce TP se déroulera sur plusieurs machines connectées sur le même réseau local.

---

## Partie 1 : Comprendre l'Architecture MapReduce

### 1.1. Schéma Général

**Indications :**
- **Nœud Coordinateur** : Ce nœud (aussi appelé "contrôleur" ou "dispatcher") a pour rôle de découper le fichier en segments, d'envoyer les segments aux nœuds de traitement et de collecter les résultats.
- **Nœuds de Traitement** : Ces nœuds reçoivent un segment de données, appliquent la fonction **Map** sur ce segment et renvoient les résultats au nœud coordinateur.
- **Phase Reduce** : Une fois que le nœud coordinateur a récupéré tous les résultats partiels, il applique une fonction **Reduce** pour agréger les résultats en une seule sortie.

**Exemple schématique :**

```
         [Fichier de données]
                  │
         Découpage en segments
                  │
         ┌────────┴────────┐
         │  Coordinateur   │
         └────────┬────────┘
                  │
         Distribution des segments
          ┌────────┴─────────┐
          │                  │
  [Worker 1]            [Worker 2]  ... (pouvant s'étendre)
          │                  │
    Exécution de Map   Exécution de Map
          │                  │
          └────Résultats─────┘
                  │
          Agrégation (Reduce)
                  │
         [Résultat Final]
```

### 1.2. Fonctionnement en Détail

**Découpage du fichier :**
- Le fichier volumineux sera lu par le coordinateur.
- Vous pouvez choisir de découper le fichier par nombre de lignes ou par blocs de caractères. L’objectif est d'obtenir autant de segments que de nœuds de traitement prévus.

**Communication Réseau :**
- Utilisez des sockets TCP pour la communication entre le coordinateur et les nœuds de traitement.
- Le coordinateur se mettra en écoute sur un port spécifique.
- Les nœuds de traitement se connecteront à ce port pour recevoir leur segment de données et, après traitement, renverront leur résultat.

**Fonction Map :**
- La fonction Map traitera un segment de texte et produira un résultat partiel. Par exemple, pour un comptage de mots, la fonction Map lira le segment et produira un dictionnaire avec les mots en clés et leur nombre d'occurrences en valeurs.
- **Indications supplémentaires :**
  - Pensez à normaliser les mots (ex. en minuscules et en supprimant la ponctuation).
  - Utilisez la méthode `split()` pour découper le texte en mots, en prenant soin de nettoyer les chaînes.

**Fonction Reduce :**
- La fonction Reduce agrège les résultats partiels issus de chaque nœud de traitement.
- Par exemple, en additionnant les occurrences pour chaque mot provenant des différents résultats partiels.
- **Indications supplémentaires :**
  - Parcourez chaque dictionnaire partiel et mettez à jour un dictionnaire global pour regrouper les comptages.
  - Testez avec un petit nombre de segments pour vérifier que l'agrégation est correcte.

---

## Partie 2 : Mise en Place Pratique sur vos Machines

### 2.1. Préparation de l'Environnement

- **Installation de Python 3.x** : Vérifiez que Python est installé sur chaque machine.
- **Configuration réseau** : Assurez-vous que toutes les machines sont sur le même réseau local et que les ports choisis (ex. 5000) ne sont pas bloqués par un pare-feu.

### 2.2. Développement du Coordinateur

**Indications :**
- **Lecture et découpage du fichier** :  
  - Implémentez un module qui lit un fichier (ex. `grand_texte.txt`) et le découpe en segments.
- **Serveur TCP** :
  - Créez un serveur TCP qui se met en écoute sur une IP et un port définis.
  - Pour chaque connexion entrante, envoyez le segment correspondant en utilisant, par exemple, un format JSON pour la transmission des données.
- **Gestion des connexions** :
  - Utilisez des threads ou la programmation asynchrone pour gérer plusieurs connexions en parallèle.
  - Assurez-vous de collecter les résultats partiels dans une structure de données adaptée.
- **Phase Reduce** :
  - Une fois tous les résultats reçus, appliquez votre fonction Reduce pour produire le résultat final.
  - Affichez ou stockez ce résultat dans un fichier.

### 2.3. Développement des Nœuds de Traitement

**Indications :**
- **Client TCP** :
  - Implémentez un client qui se connecte au coordinateur en utilisant l'adresse IP et le port spécifiés.
- **Réception du segment** :
  - Le client doit recevoir le segment de données (par exemple, sous format JSON), le convertir en texte, et le stocker dans une variable.
- **Exécution de la fonction Map** :
  - Appliquez la fonction Map sur le segment reçu pour produire un dictionnaire partiel.
- **Envoi du résultat** :
  - Convertissez le dictionnaire en JSON et renvoyez-le au coordinateur via la connexion établie.
- **Gestion des erreurs** :
  - Prévoyez des mécanismes de reprise ou de déconnexion en cas de problème de communication.

### 2.4. Tests et Débogage

**Indications :**
- Commencez par tester la communication en local sur une seule machine en simulant plusieurs clients (via des processus ou des threads).
- Une fois la communication locale validée, déployez le coordinateur sur une machine et les nœuds de traitement sur d'autres machines.
- Utilisez des outils comme `ping` pour vérifier la connectivité et ajoutez des logs ou des impressions console pour suivre l'exécution.
- Notez dans votre rapport les difficultés rencontrées, les stratégies de débogage et les solutions mises en place.

---

## Travaux à réaliser après un simple MapReduce

1. **Ajout de la Tolérance aux Pannes :**  
   Implémentez un mécanisme permettant de détecter lorsqu'un nœud de traitement ne répond pas ou se déconnecte, et redirigez son segment vers un autre nœud disponible.

2. **Évolutivité Horizontale :**  (Optionnel)
   Permettez à l'architecture de gérer dynamiquement l'ajout et la suppression de nœuds de traitement pendant l'exécution du système.

3. **Analyse de Données Avancée :**  
   Modifiez les fonctions Map et Reduce pour réaliser d'autres types d'analyses sur le jeu de données de [Yelp](https://business.yelp.com/data/resources/open-dataset/)

---

## Partie 3 : Rédaction du Rapport

Votre rapport doit inclure (Pour chacune des questions) :

1. **Schéma détaillé de l'architecture MapReduce**  
   Expliquez les rôles du coordinateur et des nœuds de traitement avec les adresse IP.

2. **Description technique**  
   - Méthode de découpage des données.
   - Détails de la communication réseau (protocole utilisé, format des messages, gestion des connexions).
   - Implémentation des fonctions Map et Reduce.

3. **Tests et Débogage**  
   - Méthodologie de test (local puis déployé sur plusieurs machines).
   - Problèmes rencontrés et solutions apportées.
   - Logs des affichages
   - Captures d'écrans du worker et coordinator

4. **Pistes d'amélioration**  
   Proposez des améliorations futures (gestion d'un nombre plus important de nœuds, optimisation des performances, tolérance aux pannes, etc.).

---

Ce TP vous permettra d'aborder de manière progressive et pratique la mise en œuvre d'une architecture MapReduce en environnement distribué. Chaque étape est accompagnée d'indications détaillées pour guider votre réflexion et votre implémentation. Bonne réalisation !
Soumission doit être effectué avant Mercredi matin 8h

---

### Critères de notations :

1. 3 points pour la réalisation de chaque question 2 point pour l'explication dans le rapport pour chaque question. 

# 🧪 Travaux Pratiques : Conception d'une Architecture Big Data pour la Gestion de Données en Temps Réel

## 🎯 Objectif du TP

L'objectif de ce TP est de concevoir une **architecture Big Data pertinente** pour un **système de gestion de données en temps réel** dans un contexte complexe et exigeant. Les étudiants devront effectuer une **veille technologique**, comparer différentes technologies du Big Data, puis **établir une architecture adaptée** au contexte fourni.

L'architecture devra couvrir les trois piliers suivants :

- **Stockage des données**
- **Traitement des données en temps réel**
- **Visualisation / Affichage des données**

---

## 📘 Contexte

Une grande entreprise de **logistique humanitaire internationale** souhaite mettre en place une plateforme de gestion de crise en temps réel pour suivre et anticiper les catastrophes naturelles, les mouvements de population et les besoins logistiques sur le terrain.

Les défis du contexte :

- Les données proviennent de **sources multiples, hétérogènes et massives**
- Les données sont **structurées, semi-structurées et non-structurées**
- Il est essentiel de disposer d’une **vision temps réel pour réagir rapidement**
- Le système doit être **scalable, tolérant aux pannes, sécurisé** et **évolutif**

---

## 🔗 Sources de données

Voici les **10 sources de données** que votre architecture devra prendre en charge :

1. **Capteurs IoT sur le terrain** : température, humidité, qualité de l'air
2. **Drones et satellites** : images en temps réel et données géospatiales
3. **Flux de réseaux sociaux (Twitter, Facebook)** : extraction de sentiments et détection d’événements
4. **Systèmes GPS** des véhicules de transport
5. **Bases de données internes** de gestion de stocks et entrepôts
6. **Données ouvertes gouvernementales** (OpenData) : météo, cartographie, population
7. **Flux vidéo en direct** de caméras de surveillance
8. **Logs de serveurs** et systèmes informatiques internes
9. **Messageries instantanées d’agents de terrain** (via API WhatsApp, Telegram, etc.)
10. **Actualités RSS et flux d’agences de presse**

---

## 📌 Travail demandé

### 1. **Veille technologique**
- Identifier les outils disponibles pour :
  - Le **stockage** (ex: HDFS, Cassandra, MongoDB, etc.)
  - Le **traitement temps réel** (ex: Kafka, Spark Streaming, Flink, etc.)
  - La **visualisation** (ex: Grafana, Kibana, Superset, etc.)
- Analyser les **avantages, inconvénients, cas d’usage** de chaque technologie

### 2. **Comparaison de solutions**
- Comparer les architectures possibles : Lambda, Kappa, architecture orientée événements, etc.
- Discuter des critères de choix : latence, scalabilité, complexité, maintenance, coûts

### 3. **Proposition d'une architecture pertinente**
- Concevoir une architecture complète pour le contexte donné
- Définir les **outils choisis**, leur **positionnement** dans l’architecture, et leur **interaction**
- Inclure un **schéma de l’architecture**
- Justifier les choix techniques

---

## 📝 Livrables attendus

- Rapport structuré (PDF ou Markdown) avec :
  - Synthèse de la veille technologique
  - Tableau comparatif des outils
  - Description de l’architecture proposée
  - Schéma explicatif de l’architecture
- Optionnel : Prototype ou démonstration simple avec un jeu de données simulé

---

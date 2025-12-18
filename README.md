# Projet de Reinforcement Learning – LunarLander-v3 (discret)

## 1. Présentation générale

Ce projet a pour objectif de mettre en pratique les concepts fondamentaux du Reinforcement Learning à travers l’étude de l’environnement **LunarLander-v3**.  
L’objectif est de comparer plusieurs algorithmes de RL et d’analyser leurs performances, leur stabilité et leur comportement dans un environnement à **actions discrètes**.

L’environnement a été choisi pour sa dynamique non triviale et son système de récompense riche, permettant une analyse approfondie des stratégies apprises par les agents.

---

## 2. Environnement : LunarLander-v3

### Description générale

LunarLander-v3 simule l’atterrissage d’un module spatial sur une surface lunaire.  
L’agent doit contrôler les moteurs du module afin d’atterrir entre deux drapeaux, avec une vitesse et une orientation compatibles avec un atterrissage en douceur, tout en limitant la consommation de carburant.

Documentation officielle :  
https://gymnasium.farama.org/environments/box2d/lunar_lander/

---

### États (observations)

L’espace d’observation est un vecteur de **8 valeurs continues** :

1. Position horizontale du module  
2. Position verticale  
3. Vitesse horizontale  
4. Vitesse verticale  
5. Angle du module  
6. Vitesse angulaire  
7. Contact de la jambe gauche avec le sol (0 ou 1)  
8. Contact de la jambe droite avec le sol (0 ou 1)

Ces variables décrivent complètement l’état du système à un instant donné.

---

### Actions

L’espace d’actions est **discret** (`Discrete(4)`) :

- 0 : ne rien faire  
- 1 : activer le moteur gauche  
- 2 : activer le moteur principal  
- 3 : activer le moteur droit  

---

### Récompenses

La fonction de récompense encourage :

- une descente contrôlée,
- un atterrissage stable entre les drapeaux,
- une consommation de carburant modérée.

Un atterrissage réussi donne une récompense positive élevée, tandis qu’un crash entraîne une forte pénalité.

---

### Conditions de terminaison

Un épisode se termine lorsque :

- le module atterrit correctement,  
- le module s’écrase,  
- ou sort de la zone de jeu.

---

## 3. Algorithmes implémentés

Trois algorithmes de Reinforcement Learning adaptés aux actions discrètes ont été implémentés :

- **DQN (Deep Q-Network)**  
  Algorithme basé sur l’approximation de la fonction de valeur Q par un réseau de neurones.

- **PPO (Proximal Policy Optimization)**  
  Algorithme de type policy gradient, reconnu pour sa stabilité.

- **A2C (Advantage Actor-Critic)**  
  Algorithme actor-critic synchrone, plus simple et rapide à entraîner.

Ces algorithmes permettent de comparer différentes approches du Reinforcement Learning.

---

## 4. Méthodologie expérimentale

Chaque algorithme est entraîné sur le même environnement avec des paramètres similaires afin de garantir une comparaison équitable.  
Le nombre de timesteps est volontairement augmenté (50 000 à 100 000) pour permettre un apprentissage stable et significatif.

Les performances sont évaluées après l’entraînement sur plusieurs épisodes indépendants.  
Un callback personnalisé est utilisé pour enregistrer la récompense totale à la fin de chaque épisode.

---

## 5. Graphiques et métriques

### Courbes de récompense

- Pour rendre les courbes lisibles, nous avons utilisé **une moyenne glissante sur 10 épisodes**.  
- Cette méthode permet de **comparer directement PPO, DQN et A2C**, même si le nombre d’épisodes terminés diffère selon l’algorithme.  
- Les courbes montrent la tendance générale et la stabilité de chaque algorithme.

### Comparaison finale

- Le **score moyen par épisode** et l’**écart-type** sont calculés sur 10 épisodes.  
- Un barplot montre la performance et la stabilité relative des algorithmes, ce qui permet une comparaison rapide et claire.

---

## 6. Analyse critique

- Les différences de nombre d’épisodes sur les courbes s’expliquent par la **durée variable des épisodes** :  
  A2C termine souvent plus vite, PPO explore plus prudemment, DQN est intermédiaire.  
- L’augmentation des timesteps a permis d’obtenir des courbes plus stables et des scores positifs significatifs.  
- Les limites : hyperparamètres non optimisés, un seul seed, nombre de timesteps encore limité par le temps disponible.

---

## 7. Utilisation des outils d’IA

Des outils d’IA ont été utilisés comme **assistance** pour clarifier certains concepts, structurer le code expérimental et aider à l’analyse des résultats.  

L’ensemble du code, des choix techniques et des résultats a été compris, testé et validé par les étudiants.  
L’IA n’a pas été utilisée comme substitut à la réflexion scientifique.

---

## 8. Instructions d’exécution

### Dépendances

```bash
pip install gymnasium[box2d] stable-baselines3 matplotlib pandas

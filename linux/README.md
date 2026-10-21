# 🚩 OverTheWire: Bandit — Writeup & Apprentissage (Niveaux 0 à 6)

Ce dépôt documente ma progression et mon apprentissage sur le wargame **Bandit** de [OverTheWire](https://overthewire.org/wargames/bandit/). 

L'objectif de ce projet est d'apprendre et de consolider mes bases en **lignes de commande Linux**, en **sécurité des systèmes** et en **manipulation de fichiers via SSH**.

---

## 🛠️ Commandes Linux apprises et utilisées

Au cours de ces niveaux, j'ai manipulé et appris à utiliser les commandes fondamentales suivantes :

- **`ssh`** : Se connecter à un serveur distant de manière sécurisée.
- **`ls`** : Lister les fichiers et répertoires (options `-la` pour afficher les fichiers cachés).
- **`cd`** : Naviguer entre les dossiers.
- **`cat`** : Afficher le contenu d'un fichier dans le terminal.
- **`file`** : Déterminer le type de données/fichier (texte, binaire, etc.).
- **`find`** : Rechercher des fichiers selon des critères précis (taille, propriétaire, groupe, permissions).
- **`grep`** : Rechercher des chaînes de caractères spécifiques dans un fichier.
- **`strings`** : Extraire les chaînes de caractères lisibles d'un fichier binaire.
- **`base64`** : Décoder du contenu encodé en Base64.
- **`tr`** : Transposer ou remplacer des caractères (utilisé pour déchiffrer ROT13).

---

## 🎯 Résumé des niveaux accomplis

### 🟢 Niveau 0 ➔ Level 0 → Level 1
- **Objectif :** Se connecter au serveur de jeu via SSH.
- **Commande utilisée :**
  ```bash
  ssh bandit0@bandit.labs.overthewire.org -p 2220
  ```
- **Notions clés :** Utilisation de SSH avec un port spécifique (`-p 2220`) et lecture du mot de passe dans le fichier `readme` avec `cat`.

---

### 🟢 Niveau 1 ➔ Level 1 → Level 2
- **Objectif :** Lire le mot de passe stocké dans un fichier nommé `-`.
- **Commande utilisée :**
  ```bash
  cat ./-
  ```
- **Notions clés :** En Linux, un fichier nommé `-` peut être interprété comme l'entrée standard (*stdin*). Spécifier le chemin relatif `./-` permet de forcer la lecture du fichier.
![Lecture du fichier tiret avec le chemin relatif](screnshoot/bandit1.png)

---

### 🟢 Niveau 2 ➔ Level 2 → Level 3
- **Objectif :** Lire un fichier dont le nom contient des espaces (`spaces in this filename`).
- **Commandes utilisées :**
  ```bash
  cat "spaces in this filename"
  # ou
  cat spaces\ in\ this\ filename
  ```
- **Notions clés :** Échappement des espaces à l'aide d'anti-slashs (`\`) ou encadrement du nom du fichier avec des guillemets.
![Gestion des espaces dans le nom de fichier](screnshoot/bandit2.png)

---

### 🟢 Niveau 3 ➔ Level 3 → Level 4
- **Objectif :** Trouver le mot de passe caché dans un dossier `inhere`.
- **Commandes utilisées :**
  ```bash
  cd inhere
  ls -la
  cat .hidden
  ```
- **Notions clés :** Utilisation de `ls -a` pour afficher les fichiers cachés (qui commencent par un point `.`).
![Affichage du fichier caché avec ls -a](screnshoot/bandit3.png)

---

### 🟢 Niveau 4 ➔ Level 4 → Level 5
- **Objectif :** Trouver le seul fichier lisible par un humain parmi plusieurs fichiers binaires dans le dossier `inhere`.
- **Commandes utilisées :**
  ```bash
  cd inhere
  file ./*
  cat ./-file07
  ```
- **Notions clés :** Utilisation de la commande `file` pour inspecter le type de fichier (recherche de *ASCII text*) sans devoir tous les ouvrir.
![Utilisation de la commande file sur les binaires](screnshoot/bandit4.png)

---

### 🟢 Niveau 5 ➔ Level 5 → Level 6
- **Objectif :** Trouver un fichier répondant à 3 critères précis : lisible par un humain, d'une taille de 1033 octets et non exécutable.
- **Commandes utilisées :**
  ```bash
  find inhere/ -type f -size 1033c ! -executable
  cat <chemin_du_fichier_trouvé>
  ```
- **Notions clés :** Filtrage avancé avec `find` (`-type f` pour fichier, `-size 1033c` pour la taille exacte en octets, et `! -executable`).
![Recherche ciblée avec la commande find](screnshoot/bandit5.png)

---

### 🟢 Niveau 6 ➔ Level 6 → Level 7
- **Objectif :** Trouver un fichier présent sur le serveur appartenant à l'utilisateur `bandit7`, au groupe `bandit6` et faisant 33 octets.
- **Commandes utilisées :**
  ```bash
  find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
  ```
- **Notions clés :** Recherche depuis la racine `/` et redirection des erreurs de permission (`Permission denied`) vers `/dev/null` avec `2>/dev/null`.
![Recherche globale des permissions root avec find](screnshoot/bandit6-1.png)

---

## 🚀 Prochaines étapes

- [ ] Compléter les niveaux 7 à 15.
- [ ] Approfondir l'automatisation avec des scripts Bash.
- [ ] Découvrir la manipulation d'archives et la cryptographie de base.

---
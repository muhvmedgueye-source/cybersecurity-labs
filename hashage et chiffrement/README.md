# TP : Hachage et intégrité des données

## 🎯 Objectif

Ce TP a pour objectif de découvrir les fonctions de hachage et de comprendre comment elles peuvent aider à vérifier l’intégrité d’un fichier.

J’ai réalisé les manipulations sous **Windows PowerShell**, avec la commande `certutil`, en comparant les empreintes de fichiers avant et après une modification.

## 🧠 Notions apprises

- Une fonction de hachage transforme des données en une empreinte de longueur fixe.
- Une petite modification du contenu produit généralement une empreinte très différente : c’est l’**effet avalanche**.
- Le hachage est conçu pour être à sens unique : il ne sert pas à déchiffrer une donnée.
- Comparer l’empreinte calculée d’un fichier avec une empreinte de référence permet de détecter une modification.
- **MD5** et **SHA-1** sont considérés comme obsolètes pour les usages de sécurité sensibles. Pour cet exercice, j’ai également testé **SHA-256** et **SHA-512**.

> À retenir : une empreinte seule ne prouve pas que le fichier est fiable. Il faut comparer l’empreinte à une valeur de référence obtenue depuis une source de confiance.

## 🛠️ Environnement et outils

- Système : Windows
- Terminal : PowerShell
- Outil : `certutil`
- Fichier de test : `FILE3.txt.txt` (nom utilisé pendant la manipulation)

## 💻 Commandes utilisées

Pour calculer l’empreinte d’un fichier, j’ai utilisé les commandes suivantes :

```powershell
certutil -hashfile FILE3.txt.txt MD5
certutil -hashfile FILE3.txt.txt SHA1
certutil -hashfile FILE3.txt.txt SHA256
certutil -hashfile FILE3.txt.txt SHA512
```

La commande `-hashfile` demande à `certutil` de calculer l’empreinte du fichier indiqué avec l’algorithme choisi.

**Remarque :** le fichier doit exister dans le répertoire courant. Sinon, indique son chemin complet ou déplace-toi d’abord dans le bon dossier avec `cd`.

## 🧪 Déroulement du TP

1. Créer un fichier texte de test.
2. Calculer et noter ses empreintes avec MD5, SHA-1, SHA-256 et SHA-512.
3. Modifier légèrement le contenu du fichier, par exemple en ajoutant un caractère.
4. Recalculer les empreintes.
5. Comparer les résultats avant et après la modification.

### Résultat observé

Après la modification du fichier, les empreintes calculées ont changé. Cette observation illustre l’effet avalanche : une petite modification des données peut entraîner une empreinte très différente.

## 📸 Captures d’écran

Les captures ci-dessous documentent les étapes du TP. Place les images dans un dossier `screenshots/` à la racine de ce projet, en utilisant ces noms de fichiers :

| Fichier | Contenu |
|---|---|
| `screenshots/fichier_avant_modification.png` | Contenu du fichier avant modification |
| `screenshots/fichier_apres_modification.png` | Contenu du fichier après modification |
| `screenshots/hachage_avant_modification.png` | Empreintes calculées avant modification |
| `screenshots/hachage_apres_modification.png` | Empreintes calculées après modification |
| `screenshots/notes_hachage.png` | Notes de révision sur le hachage |

### Contenu avant modification

![Contenu du fichier avant modification](screenshots/fichier_avant_modification.png)

### Contenu après modification

![Contenu du fichier après modification](screenshots/fichier_apres_modification.png)

### Empreintes avant modification

![Empreintes avant modification](screenshots/hachage_avant_modification.png)

### Empreintes après modification

![Empreintes après modification](screenshots/hachage_apres_modification.png)

### Notes de révision

![Notes de révision sur le hachage](screenshots/notes_hachage.png)

## 🔎 Différence entre hachage et chiffrement

- **Hachage :** produit une empreinte et n’est pas conçu pour être inversé afin de retrouver les données originales.
- **Chiffrement :** protège la confidentialité des données et permet de retrouver le texte clair en utilisant la clé appropriée pour le déchiffrement.

Ces deux mécanismes ont donc des objectifs différents.

## ✅ Bilan

Ce TP m’a permis de pratiquer le calcul d’empreintes avec PowerShell, de comparer plusieurs algorithmes et de constater qu’une modification du fichier entraîne un changement de son empreinte.

Je poursuis mon apprentissage de la cybersécurité et je prévois d’ajouter progressivement à ce dépôt d’autres travaux pratiques sur la **cryptographie**, le chiffrement et les mécanismes de protection des données.

## 📚 Ressources

- Documentation Microsoft sur `certutil` : https://learn.microsoft.com/windows-server/administration/windows-commands/certutil

---

*TP réalisé dans le cadre de mon apprentissage personnel de la cybersécurité.*

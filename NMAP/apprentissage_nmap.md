# 🔍 Apprentissage de Nmap — Commande de Base & Options

Ce document récapitule les compétences et commandes de base que j'ai acquises lors de mon apprentissage de **Nmap** (*Network Mapper*).

---

## 💻 Environnement de Laboratoire (Home Lab)

Toutes ces commandes et expérimentations sont réalisées exclusivement dans un environnement virtuel local sécurisé et contrôlé. **Aucun réseau ou machine tierce n'est scanné sans autorisation préalable.**

Mon *lab* de test se compose de 3 machines virtuelles :
* **Kali Linux** : Machine d'attaque / Machine de scan principale.
* **Ubuntu Server/Desktop** : Cible Linux.
* **Windows 11** : Cible Windows.

---

## 🛠️ Options & Commutateurs Appris

### 1. Découverte d'hôtes & Gestion des Pings

* `-sn` (**Ping Scan / No Port Scan**) : Effectue uniquement une découverte d'hôtes sur le réseau local sans scanner les ports.
* `-Pn` (**No Ping**) : Désactive la découverte d'hôte par ping. Nmap considère que la cible est en ligne et lance directement le scan de ports (très utile si le pare-feu de Windows 11 ou Ubuntu bloque les requêtes ICMP).

### 2. Spécification des Ports

* `-p <port(s)>` : Permet de cibler un ou plusieurs ports spécifiques (ex: `-p 80`, `-p 22,80,443`, `-p 1-1000`).
* `-p-` : Scanne **la totalité** des 65 535 ports TCP (au lieu du top 1000 par défaut).

### 3. Détection de Services & Système d'Exploitation

* `-sV` (**Service Version Detection**) : Interroge les ports ouverts pour déterminer la version exacte des services/applications en cours d'exécution.
* `-O` (**OS Detection**) : Tente d'identifier le système d'exploitation de la machine cible (ex: faire la différence entre l'hôte Ubuntu et l'hôte Windows 11).
* `-A` (**Aggressive Scan**) : Active la détection du système d'exploitation (`-O`), la détection de version (`-sV`), le balayage par scripts (`-sC`) et le traceroute complet en une seule option.

### 4. Types de Scans

* `-sS` (**SYN Scan / Stealth Scan**) : Scan TCP à demi-ouvert (*Stealth scan*). C'est le scan le plus populaire, rapide et discret (requiert les privilèges `root` sous Kali).
* `-sT` (**TCP Connect Scan**) : Effectue une connexion TCP complète (Handshake à 3 voies). Utilisé par défaut si l'utilisateur n'a pas les privilèges administrateur.
* `-sU` (**UDP Scan**) : Scanne les ports UDP (plus lent que le scan TCP, mais indispensable pour découvrir des services comme DNS, DHCP, SNMP).

### 5. Sauvegarde des Résultats

* `-oN <fichier>` (**Normal Output**) : Redirige et sauvegarde le résultat du scan dans un fichier texte brut lisible pour archivage et analyse ultérieure.

---

## 💡 Exemple de Commande Exécutée depuis Kali Linux

```bash
sudo nmap -sS -sV -O -Pn -p- -oN scan.txt 192.168.56.102 192.168.56.103
```

> **Explication :** Depuis la machine Kali Linux, lancement d'un scan SYN (`-sS`) sur la cible (ex: Ubuntu), sur l'ensemble des ports (`-p-`), en ignorant le ping (`-Pn`), avec identification des services (`-sV`) et du système d'exploitation (`-O`), puis exportation du rapport dans un fichier texte (`-oN scan.txt`).
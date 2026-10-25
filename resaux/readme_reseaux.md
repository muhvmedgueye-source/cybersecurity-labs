# 🌐 Travaux Pratiques — Cisco Packet Tracer

Ce dossier rassemble mes réalisations pratiques sur la conception, l'adressage et le routage de réseaux sous **Cisco Packet Tracer**.

---

## 📌 TP 1 : Interconnexion et adressage d'un Réseau Local (LAN)

### 🎯 Objectif
Créer un réseau local commuté (LAN) à l'aide d'un switch et attribuer des adresses IP statiques aux équipements afin d'assurer la communication interne.

### 📐 Architecture & Configuration
* **Équipements :** 1 Commutateur (Switch Cisco 2960) et 4 PC.
* **Plage IP :** `192.168.1.0/24` (Masque : `255.255.255.0`).
* **Adressage des hôtes :**
  * `PC0` : `192.168.1.10`
  * `PC1` : `192.168.1.20`
  * `PC2` : `192.168.1.30`
  * `PC3` : `192.168.1.40`

### 📸 Captures d'écran

#### Topologie du Réseau Local
![Topologie LAN](srenshoot_reseaux/tp1-lan-topologie.png)

#### Configuration IP du PC0
![Configuration IP](srenshoot_reseaux/tp1-lan-config-ip.png)

#### Validation par Ping
![Ping Valide](srenshoot_reseaux/tp1-lan-ping-valide.png)

### ✅ Résultats & Validation
Les tests de connectivité effectués depuis la fenêtre de commande (`Command Prompt`) du `PC0` à l'aide de la commande `ping` vers `192.168.1.20` et `192.168.1.30` ont affiché **0% de perte de paquets**, ce qui valide le bon fonctionnement du réseau local.

---

## 📌 TP 2 : Routage Inter-Réseaux avec Routeur Cisco

### 🎯 Objectif
Interconnecter deux réseaux locaux virtuels distincts via un routeur Cisco ISR4331 et configurer les passerelles par défaut (`Default Gateway`) pour permettre la communication globale.

### 📐 Architecture & Configuration

#### 1. Plan d'adressage IP
| Équipement / Interface | Réseau / Role | Adresse IP | Masque de sous-réseau |
| :--- | :--- | :--- | :--- |
| **PC0** | LAN 1 | `192.168.1.1` | `255.255.255.0` |
| **Router1 (GigabitEthernet 0/0/0)** | Passerelle LAN 1 | `192.168.1.254` | `255.255.255.0` |
| **Router1 (GigabitEthernet 0/0/1)** | Passerelle LAN 2 | `192.168.2.254` | `255.255.255.0` |
| **PC1** | LAN 2 | `192.168.2.1` | `255.255.255.0` |

#### 2. Commandes de configuration du Routeur (CLI)
```text
Router> enable
Router# configure terminal

! Configuration de l'interface du LAN 1
Router(config)# interface gigabitEthernet 0/0/0
Router(config-if)# ip address 192.168.1.254 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

! Configuration de l'interface du LAN 2
Router(config)# interface gigabitEthernet 0/0/1
Router(config-if)# ip address 192.168.2.254 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
```

### 📸 Captures d'écran

#### Topologie Inter-Réseaux
![Topologie Routage](srenshoot_reseaux/tp2-routage-topologie.png)

#### Configuration CLI du Routeur
![CLI Routeur](srenshoot_reseaux/tp2-routage-cli-router.png)

#### Configuration de la Passerelle sur le PC
![Passerelle PC](srenshoot_reseaux/tp2-routage-passerelle-pc.png)

#### Ping Réussi entre Réseaux Différents
![Ping Inter-Réseaux](srenshoot_reseaux/tp2-routage-ping-inter-reseaux.png)

### ✅ Résultats & Validation
Après la configuration des passerelles par défaut sur `PC0` (`192.168.1.254`) et `PC1` (`192.168.2.254`), un test de `ping 192.168.1.1` depuis `PC1` a confirmé que les deux machines sur deux réseaux IP totalement différents parviennent à communiquer sans perte.

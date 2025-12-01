# 🔥 FICHE DE RÉVISION - LES PARE-FEU (FIREWALLS)

## Formation NSE 1 - Fortinet

---

## 1️⃣ DÉFINITION ET RÔLE

### Qu'est-ce qu'un pare-feu ?

Un **pare-feu (firewall)** est un dispositif de sécurité réseau qui surveille et contrôle le trafic entrant et sortant selon des règles de sécurité prédéfinies.

### Rôle principal

- **Barrière de sécurité** entre un réseau de confiance (interne) et un réseau non fiable (Internet)
- **Première ligne de défense** contre les cyberattaques
- **Point de contrôle** pour appliquer les politiques de sécurité

---

## 2️⃣ FONCTIONS PRINCIPALES

| Fonction | Description |
|----------|-------------|
| **Filtrage de paquets** | Analyse les paquets et autorise/bloque selon les règles |
| **Inspection du trafic** | Examine le contenu des communications |
| **Contrôle d'accès** | Détermine qui peut accéder à quelles ressources |
| **Journalisation** | Enregistre tous les événements pour audit |
| **Translation d'adresses (NAT)** | Masque les adresses IP internes |
| **Protection contre les menaces** | Détecte et bloque les attaques connues |

---

## 3️⃣ TYPES DE PARE-FEU

### A) Pare-feu à filtrage de paquets

- Niveau le plus basique
- Analyse les en-têtes des paquets (IP source/destination, ports)
- Rapide mais limité en sécurité

### B) Pare-feu à état (Stateful)

- Suit l'état des connexions réseau
- Se souvient des sessions établies
- Plus intelligent et sécurisé

### C) Pare-feu applicatif (Proxy)

- Inspecte le contenu au niveau application
- Peut filtrer selon le protocole (HTTP, FTP, etc.)
- Plus lent mais très sécurisé

### D) NGFW (Next-Generation Firewall) ⭐

**C'est la catégorie des FortiGate !**

- Combine toutes les fonctions précédentes
- Inspection approfondie des paquets (DPI - Deep Packet Inspection)
- Prévention d'intrusion (IPS)
- Filtrage web et applications
- Antivirus intégré
- Intelligence artificielle pour détecter les menaces

---

## 4️⃣ COMMENT FONCTIONNE UN PARE-FEU ?

### Principe de base : Les Règles de Sécurité

```
Règle 1 : AUTORISER le trafic HTTP (port 80) depuis Internet vers le serveur Web
Règle 2 : BLOQUER tout trafic non autorisé
Règle 3 : AUTORISER les employés à accéder à Internet
```

### Les critères de filtrage

- **Adresse IP source** : D'où vient le trafic ?
- **Adresse IP destination** : Où va le trafic ?
- **Port source et destination** : Quel service/application ?
- **Protocole** : TCP, UDP, ICMP ?
- **Direction** : Entrant ou sortant ?

### Ordre de traitement

1. Le trafic arrive au pare-feu
2. Le pare-feu consulte les règles **de haut en bas**
3. **Première règle correspondante** = action appliquée
4. Si aucune règle ne correspond = **blocage par défaut** (deny all)

---

## 5️⃣ POLITIQUES DE SÉCURITÉ

### Deux approches principales

#### 🔴 Liste Noire (Blacklist)

- Tout est **autorisé par défaut**
- On bloque seulement ce qui est dangereux
- ❌ Moins sécurisé (risque d'oublier des menaces)

#### 🟢 Liste Blanche (Whitelist) - **RECOMMANDÉE**

- Tout est **bloqué par défaut**
- On autorise seulement ce qui est nécessaire
- ✅ Plus sécurisé (principe du moindre privilège)

---

## 6️⃣ PLACEMENT DU PARE-FEU

### Architecture classique

```
Internet
   ↕
[Routeur]
   ↕
[PARE-FEU] 🔥
   ↕
[Switch]
   ↕
Réseau interne (LAN)
```

### Zones de sécurité

- **WAN** : Internet (non fiable)
- **LAN** : Réseau interne (de confiance)
- **DMZ** : Zone démilitarisée (serveurs publics)

---

## 7️⃣ AVANTAGES ET LIMITES

### ✅ Avantages

- Protection contre les accès non autorisés
- Contrôle du trafic réseau
- Journalisation et visibilité
- Prévention de nombreuses attaques
- Point central de sécurité

### ⚠️ Limites

- Ne protège pas contre les menaces internes
- Ne remplace pas l'antivirus
- Inefficace si mal configuré
- Ne protège pas contre l'ingénierie sociale
- Peut créer un faux sentiment de sécurité

---

## 8️⃣ BONNES PRATIQUES

1. **Politique de sécurité stricte** : Bloquer par défaut, autoriser uniquement le nécessaire
2. **Mise à jour régulière** : Firmware et signatures de menaces
3. **Surveillance continue** : Analyser les logs quotidiennement
4. **Segmentation réseau** : Diviser le réseau en zones
5. **Authentification forte** : Pour l'administration du pare-feu
6. **Sauvegarde de configuration** : Régulière et testée
7. **Documentation** : Maintenir à jour les règles et justifications

---

## 9️⃣ FORTINET ET LES PAREFEU

### FortiGate

- Gamme de pare-feu NGFW de Fortinet
- Du petit bureau aux grandes entreprises
- Intégré à la plateforme Fortinet Security Fabric

### Fonctionnalités clés Fortinet

- **FortiGuard** : Services de renseignement sur les menaces
- **SD-WAN** : Optimisation des connexions WAN
- **SSL Inspection** : Déchiffrement du trafic HTTPS
- **Application Control** : Contrôle granulaire des applications
- **Web Filtering** : Filtrage de contenu web

---

## 🎯 POINTS CLÉS À RETENIR

1. Un pare-feu est la **première ligne de défense** d'un réseau
2. Les NGFW (comme FortiGate) offrent une **protection multicouche**
3. Les règles sont traitées **de haut en bas** (ordre important !)
4. **Bloquer par défaut** est la meilleure approche (whitelist)
5. Un pare-feu seul **ne suffit pas** : approche défense en profondeur
6. La **configuration** est aussi importante que le matériel

---

## 📚 TERMES À CONNAÎTRE

- **Firewall** : Pare-feu
- **NGFW** : Next-Generation Firewall
- **IPS** : Intrusion Prevention System (Système de prévention d'intrusion)
- **DPI** : Deep Packet Inspection (Inspection approfondie des paquets)
- **NAT** : Network Address Translation
- **DMZ** : Demilitarized Zone (Zone démilitarisée)
- **ACL** : Access Control List (Liste de contrôle d'accès)
- **Stateful** : Avec état (suit les connexions)
- **Stateless** : Sans état (ne suit pas les connexions)


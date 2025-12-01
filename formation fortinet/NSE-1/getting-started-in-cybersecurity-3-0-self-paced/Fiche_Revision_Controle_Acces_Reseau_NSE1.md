# 🔐 FICHE DE RÉVISION - CONTRÔLE D'ACCÈS AU RÉSEAU (NAC)

## Formation NSE 1 - Fortinet - Leçon 02

---

## 1️⃣ DÉFINITION ET OBJECTIFS

### Qu'est-ce que le Contrôle d'Accès au Réseau (NAC) ?

Le **Network Access Control (NAC)** est une approche de sécurité qui contrôle l'accès au réseau en identifiant les utilisateurs et les appareils, en évaluant leur conformité aux politiques de sécurité, et en appliquant des restrictions d'accès appropriées.

### Objectifs principaux

- **Identifier** qui et quoi se connecte au réseau
- **Vérifier** la conformité de sécurité des appareils
- **Autoriser ou refuser** l'accès en fonction des politiques
- **Isoler** les appareils non conformes ou malveillants
- **Surveiller** l'activité des utilisateurs et appareils connectés

---

## 2️⃣ POURQUOI LE NAC EST-IL IMPORTANT ?

### Les menaces modernes

- **BYOD (Bring Your Own Device)** : Les employés utilisent leurs appareils personnels
- **IoT (Internet of Things)** : Imprimantes, caméras, thermostats connectés
- **Travail à distance** : Accès depuis des réseaux non sécurisés
- **Invités** : Visiteurs, partenaires, fournisseurs
- **Appareils non gérés** : Sans antivirus, non mis à jour, compromis

### Les risques sans NAC

- Accès non autorisé au réseau
- Propagation de malwares
- Vol de données sensibles
- Non-conformité réglementaire
- Manque de visibilité sur les appareils connectés

---

## 3️⃣ COMPOSANTS DU CONTRÔLE D'ACCÈS

### A) Authentification

**Vérifier l'identité de l'utilisateur**

Méthodes d'authentification :

- **Quelque chose que vous savez** : Mot de passe, PIN
- **Quelque chose que vous avez** : Carte à puce, token, certificat
- **Quelque chose que vous êtes** : Biométrie (empreinte, reconnaissance faciale)

Types d'authentification :

- **Authentification simple** : Nom d'utilisateur + mot de passe
- **Authentification multifacteur (MFA)** : Combinaison de 2 ou 3 facteurs
- **Authentification unique (SSO)** : Une seule connexion pour plusieurs services

### B) Autorisation

**Déterminer ce que l'utilisateur peut faire**

- Définit les droits d'accès aux ressources
- Basé sur le rôle, le groupe, ou l'identité
- Applique le principe du moindre privilège

### C) Comptabilité (Accounting)

**Enregistrer et auditer les activités**

- Qui s'est connecté ?
- Quand et d'où ?
- Quelles ressources ont été accédées ?
- Combien de temps ?

---

## 4️⃣ MODÈLE AAA (AUTHENTICATION, AUTHORIZATION, ACCOUNTING)

### Le Framework AAA

```
┌─────────────────┐
│ AUTHENTICATION  │ → Qui êtes-vous ?
├─────────────────┤
│ AUTHORIZATION   │ → Que pouvez-vous faire ?
├─────────────────┤
│ ACCOUNTING      │ → Qu'avez-vous fait ?
└─────────────────┘
```

### Processus AAA étape par étape

1. **Tentative de connexion** : L'utilisateur/appareil demande l'accès
2. **Authentication** : Vérification de l'identité (identifiants)
3. **Authorization** : Attribution des droits d'accès
4. **Accounting** : Journalisation de la session
5. **Surveillance continue** : Contrôle pendant toute la session
6. **Déconnexion** : Fin de session enregistrée

---

## 5️⃣ PROTOCOLES D'AUTHENTIFICATION

### A) RADIUS (Remote Authentication Dial-In User Service)

**Le plus utilisé pour le NAC**

Caractéristiques :

- Protocole client-serveur
- Utilise UDP (ports 1812 et 1813)
- Centralise l'authentification
- Supporte différentes méthodes d'authentification
- Largement compatible

### B) TACACS+ (Terminal Access Controller Access-Control System Plus)

Caractéristiques :

- Développé par Cisco
- Utilise TCP (port 49)
- Sépare AAA en trois fonctions distinctes
- Plus granulaire que RADIUS
- Principalement pour équipements réseau

### C) 802.1X

**Standard pour le contrôle d'accès au niveau port**

Composants :

- **Supplicant** : L'appareil qui veut se connecter
- **Authenticator** : Le switch ou point d'accès WiFi
- **Authentication Server** : Serveur RADIUS

Fonctionnement :

1. L'appareil se connecte au switch
2. Le switch bloque tout trafic sauf l'authentification
3. L'appareil envoie ses identifiants via le switch
4. Le serveur RADIUS valide ou refuse
5. Le switch autorise ou bloque l'accès

---

## 6️⃣ ÉVALUATION DE LA CONFORMITÉ

### Vérifications de sécurité (Posture Assessment)

Avant d'autoriser l'accès, le NAC vérifie :

**État de sécurité de l'appareil :**

- ✅ Antivirus installé et à jour ?
- ✅ Pare-feu activé ?
- ✅ Système d'exploitation mis à jour ?
- ✅ Patches de sécurité appliqués ?
- ✅ Logiciels autorisés uniquement ?
- ✅ Chiffrement du disque activé ?

### Actions selon la conformité

| État | Action |
|------|--------|
| **Conforme** | Accès complet au réseau |
| **Partiellement conforme** | Accès limité (quarantaine) |
| **Non conforme** | Accès refusé ou réseau de remédiation |
| **Inconnu** | Isolation et analyse |

---

## 7️⃣ SEGMENTATION DU RÉSEAU

### VLAN (Virtual Local Area Network)

Le NAC utilise les VLAN pour séparer le trafic :

**Exemples de segmentation :**

- **VLAN Employés** : Accès complet aux ressources internes
- **VLAN Invités** : Accès Internet uniquement
- **VLAN Quarantaine** : Appareils non conformes (accès limité pour mise à jour)
- **VLAN IoT** : Appareils connectés (imprimantes, caméras)
- **VLAN Serveurs** : Zone critique isolée

### Avantages de la segmentation

- Limite la propagation des attaques
- Améliore les performances
- Simplifie la gestion
- Renforce la sécurité
- Facilite la conformité

---

## 8️⃣ TYPES DE DÉPLOIEMENT NAC

### A) NAC en ligne (In-line)

Le NAC est **physiquement dans le chemin** du trafic

Avantages :

- Contrôle total du trafic
- Peut bloquer instantanément
- Application stricte des politiques

Inconvénients :

- Point de défaillance unique
- Peut affecter les performances
- Plus complexe à déployer

### B) NAC hors-bande (Out-of-band)

Le NAC **surveille et configure** sans être dans le chemin

Avantages :

- Pas d'impact sur les performances
- Pas de point de défaillance unique
- Plus facile à déployer

Inconvénients :

- Dépend des équipements réseau (switches)
- Délai de réaction possible

---

## 9️⃣ FORTINET ET LE NAC

### FortiNAC

**Solution NAC complète de Fortinet**

Fonctionnalités principales :

- **Visibilité totale** : Découverte automatique de tous les appareils
- **Contrôle d'accès** : Authentification et autorisation
- **Évaluation de conformité** : Vérification de la posture de sécurité
- **Réponse automatique** : Quarantaine des appareils non conformes
- **Intégration** : Fonctionne avec FortiGate et Security Fabric

### FortiAuthenticator

**Serveur d'authentification Fortinet**

Fonctionnalités :

- Serveur RADIUS/LDAP
- Gestion des certificats
- Authentification multifacteur (MFA)
- Portail captif pour invités
- Single Sign-On (SSO)

### Intégration Security Fabric

FortiNAC s'intègre avec :

- **FortiGate** : Pare-feu pour appliquer les politiques
- **FortiSwitch** : Switches pour contrôle d'accès au niveau port
- **FortiAP** : Points d'accès WiFi pour contrôle sans fil
- **FortiAnalyzer** : Journalisation et reporting centralisés
- **FortiClient** : Agent endpoint pour évaluation de conformité

---

## 🔟 CAS D'USAGE PRATIQUES

### Scénario 1 : Employé avec laptop d'entreprise

1. Employé arrive au bureau et se connecte au réseau filaire
2. Switch demande authentification 802.1X
3. FortiNAC vérifie l'identité (Active Directory)
4. FortiClient agent vérifie la conformité (antivirus, patches)
5. ✅ Conforme → VLAN Employés, accès complet

### Scénario 2 : Smartphone personnel (BYOD)

1. Employé connecte son téléphone au WiFi
2. Portail captif demande identifiants
3. FortiNAC authentifie via RADIUS
4. Vérification basique de sécurité
5. ⚠️ Appareil personnel → VLAN BYOD, accès limité

### Scénario 3 : Visiteur invité

1. Visiteur demande accès WiFi
2. Réceptionniste crée compte temporaire
3. Visiteur se connecte avec identifiants temporaires
4. 🔒 Accès Internet uniquement → VLAN Invités
5. Compte expire après X heures

### Scénario 4 : Appareil non conforme

1. Laptop se connecte avec antivirus désactivé
2. FortiNAC détecte non-conformité
3. ❌ Accès refusé → VLAN Quarantaine
4. Message : "Veuillez activer votre antivirus"
5. Accès limité au serveur de mise à jour uniquement

---

## 1️⃣1️⃣ BONNES PRATIQUES NAC

### Déploiement

1. **Commencer en mode surveillance** : Observer avant de bloquer
2. **Déploiement progressif** : Par département ou type d'appareil
3. **Inventaire complet** : Recenser tous les appareils avant activation
4. **Exceptions documentées** : Lister les appareils qui ne peuvent pas être conformes
5. **Communication** : Informer les utilisateurs avant le déploiement

### Gestion quotidienne

1. **Surveiller les alertes** : Vérifier les tentatives bloquées
2. **Mettre à jour les politiques** : Adapter aux nouveaux besoins
3. **Réviser les accès** : Audit régulier des autorisations
4. **Former les utilisateurs** : Sensibilisation à la sécurité
5. **Tester régulièrement** : Vérifier que le NAC fonctionne correctement

### Sécurité

1. **MFA obligatoire** : Pour accès à distance et administrateurs
2. **Principe du moindre privilège** : Accès minimal nécessaire
3. **Segmentation stricte** : Séparer les zones sensibles
4. **Chiffrement** : Pour toutes les communications d'authentification
5. **Redondance** : Serveurs RADIUS multiples

---

## 1️⃣2️⃣ AVANTAGES ET DÉFIS

### ✅ Avantages du NAC

- **Visibilité complète** : Connaissance de tous les appareils connectés
- **Sécurité renforcée** : Seuls les appareils autorisés et conformes accèdent
- **Conformité réglementaire** : Preuve de contrôles de sécurité
- **Réponse automatique** : Isolation rapide des menaces
- **Support du BYOD** : Gestion sécurisée des appareils personnels
- **Réduction des risques** : Moins d'exposition aux menaces

### ⚠️ Défis du NAC

- **Complexité de déploiement** : Nécessite planification et expertise
- **Compatibilité** : Certains appareils (IoT) ne supportent pas l'authentification
- **Gestion continue** : Maintenance des politiques et exceptions
- **Impact utilisateur** : Peut causer des frustrations si mal configuré
- **Coût initial** : Investissement en matériel et licences
- **Formation** : Équipe IT doit être formée

---

## 🎯 POINTS CLÉS À RETENIR

1. Le NAC contrôle **qui et quoi** accède au réseau
2. Le modèle **AAA** est fondamental : Authentication, Authorization, Accounting
3. **802.1X** est le standard pour contrôle d'accès au niveau port
4. La **conformité des appareils** doit être vérifiée avant l'accès
5. La **segmentation VLAN** isole les différents types de trafic
6. Le NAC fonctionne **en ligne** ou **hors-bande**
7. FortiNAC s'intègre dans la **Security Fabric** de Fortinet
8. Le déploiement doit être **progressif** et bien planifié

---

## 📚 TERMES À CONNAÎTRE

- **NAC** : Network Access Control (Contrôle d'Accès au Réseau)
- **AAA** : Authentication, Authorization, Accounting
- **RADIUS** : Remote Authentication Dial-In User Service
- **TACACS+** : Terminal Access Controller Access-Control System Plus
- **802.1X** : Standard IEEE pour contrôle d'accès au niveau port
- **Supplicant** : Client demandant l'accès au réseau
- **Authenticator** : Équipement réseau (switch/AP) qui contrôle l'accès
- **Posture Assessment** : Évaluation de la conformité de sécurité
- **VLAN** : Virtual Local Area Network (Réseau local virtuel)
- **MFA** : Multi-Factor Authentication (Authentification multifacteur)
- **SSO** : Single Sign-On (Authentification unique)
- **BYOD** : Bring Your Own Device (Apportez votre appareil personnel)
- **Quarantine** : Isolement des appareils non conformes
- **Remediation** : Mise en conformité des appareils

---

## 🔄 COMPARAISON NAC vs PARE-FEU

| Aspect | Pare-feu | NAC |
|--------|----------|-----|
| **Focus** | Trafic réseau | Utilisateurs et appareils |
| **Niveau** | Couches 3-7 OSI | Couche 2 (niveau port) |
| **Décision** | Autorise/bloque le trafic | Autorise/bloque l'accès réseau |
| **Critères** | IP, ports, protocoles | Identité, conformité |
| **Moment** | Pendant la communication | Avant l'accès au réseau |
| **Complémentarité** | ✅ Travaillent ensemble | ✅ Travaillent ensemble |

**Important** : Le NAC et le pare-feu sont **complémentaires**, pas des alternatives !

---

## ✏️ NOTES PERSONNELLES

_(Espace pour ajouter vos propres notes, exemples du cours, ou questions)_

---

**💡 Conseil de révision :**

- Comprenez bien la différence entre authentification et autorisation
- Mémorisez le processus AAA dans l'ordre
- Visualisez les différents VLAN et leur utilité
- Pensez à des cas d'usage concrets dans votre environnement

**🎓 Formation NSE 1 - Fortinet Network Security Expert**

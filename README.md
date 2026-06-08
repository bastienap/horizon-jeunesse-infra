# Horizon Jeunesse - Infrastructure IT

## Présentation du Projet
Ce dépôt documente la restructuration informatique de l'association "Horizon Jeunesse". L'objectif était de transformer un parc informatique "artisanal" (postes isolés, risques de sécurité) en une infrastructure centralisée, sécurisée et évolutive.

Organisation : Association "Horizon Jeunesse" (aide à la réinsertion professionnelle de jeunes et suivi de mineurs).
Effectif : 15 salariés permanents + bénévoles réguliers.

### État initial du parc informatique (Audit) :

- Postes de travail (Windows 11 Pro) isolés en groupe de travail (Workgroup).
- Tous les salariés sont administrateurs locaux de leur machine (Shadow IT, risques de malwares, manque de contrôle).
- Aucune politique de mot de passe (comptes sans mot de passe ou obsolètes).
- Échange de données sensibles par clés USB ou partages réseau non sécurisés.

Opportunité : Récupération d'un serveur physique (don).

### Objectifs
- **Centralisation :** Déploiement d'un contrôleur de domaine (Active Directory).
- **Sécurisation :** Rétrogradation des privilèges locaux et durcissement des accès.
- **Automatisation :** Gestion des utilisateurs et des permissions via PowerShell.

### Architecture Technique
- **Serveur :** Windows Server 2025 (`SRV-DC01`)
- **Domaine :** `horizon.local`
- **Clients :** Windows 11 Pro

## Étapes de Déploiement

### 1. Déploiement du Cœur de l'Infrastructure
- **Serveur cible** : SRV-DC01 (Windows Server 2025 Standard - Expérience de bureau).
- **Configuration réseau** : IP statique fixe (192.168.10.10/24), Passerelle (192.168.10.1), DNS primaire local (127.0.0.1 puis 192.168.10.10).
- **Rôles installés** : AD DS (Active Directory Domain Services) et serveur DNS.
- **Forêt & Domaine créé** : horizon.local (Nom NetBIOS : HORIZON).
- **Sécurité d'installation** : Configuration du mot de passe de secours DSRM (Directory Services Restore Mode).
- **Arborescence AD (Unités Organisationnelles)** :
  - OU_Direction
  - OU_Permanents (salariés stables)
  - OU_Benevoles (comptes temporaires ou partagés)

### 2. Sécurisation des Postes Clients
- Poste cible : PC-PERM-01 (Poste de travail Windows 11 Pro).
- Actions locales indispensables (Avant jonction) :
  - Création d'un compte de secours local du helpdesk : Support_Tech (membre du groupe local Administrateurs, mot de passe robuste à renouvellement non obligatoire).
  - Audit du groupe local Administrateurs : identification du compte de l'utilisateur (ex: Julie / j.dupont) pour planifier sa rétrogradation en Utilisateur standard après la jonction.

### 3 : Migration et Intégration au Domaine
- Configuration réseau du client : IP fixe (192.168.10.20/24), Passerelle (192.168.10.1), et DNS primaire obligatoirement configuré vers le DC (192.168.10.10).
- Jonction au domaine : Intégration de la machine PC-PERM-01 dans le domaine horizon.local à l'aide de l'authentification HORIZON\Administrateur.
- Validation post-migration :
  - Vérification de l'objet ordinateur dans l'Active Directory.
  - Connexion au profil de domaine (j.dupont) et vérification de son statut d'utilisateur standard sur sa machine (impossible d'installer de logiciels ou de modifier la configuration réseau sans élévation de privilèges via le compte local Support_Tech

### 4. Gestion des identités & délégation de droits
- Création automatisée de 20 comptes utilisateurs répartis par département :
  - **OU_Direction** : 5 utilisateurs
  - **OU_Permanents** : 10 utilisateurs
  - **OU_Benevoles** : 5 utilisateurs
- Mise en place de la **Délégation de contrôle** pour permettre aux responsables de département de gérer les mots de passe de leurs collaborateurs sans privilèges d'administrateur domaine.

## Outils utilisés
- **Windows Server 2025** (AD DS, DNS)
- **PowerShell** (Automatisation des tâches d'administration)
- **VirtualBox** (Virtualisation de l'environnement)

---
*Projet réalisé dans le cadre de la standardisation des systèmes d'information.*

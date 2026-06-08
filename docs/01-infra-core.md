# Fiche Technique : Déploiement du Cœur de l'Infrastructure (AD DS)
## 1. Objectifs
- Installer le rôle Active Directory Domain Services (AD DS).
- Promouvoir le serveur en tant que premier contrôleur de domaine d'une nouvelle forêt.
- Structurer l'annuaire avec des Unités d'Organisation (OU) spécifiques aux besoins de l'association.

## 2. Installation du rôle AD DS
Une fois la configuration réseau de base effectuée (IP statique 192.168.10.10), l'installation des services d'annuaire commence dans le Gestionnaire de serveur.
1. Allez dans Gérer > Ajouter des rôles et fonctionnalités.
2. Dans l'assistant, progressez jusqu'à la section Rôles de serveurs.
3. Cochez la case Services de domaine Active Directory.
4. Une fenêtre surgissante proposera d'ajouter les outils d'administration (RSAT) ; validez en cliquant sur Ajouter des fonctionnalités.

<img width="516" height="363" alt="1  Active directory domain server activé" src="https://github.com/user-attachments/assets/caacf7f4-eebe-42ca-967b-7ac402ac25e6" />


## 3. Promotion du serveur en Contrôleur de Domaine

L'installation du rôle ne suffit pas à créer le domaine ; il faut passer par l'assistant de promotion.
1. Cliquez sur l'icône de notification (drapeau ⚑) dans le Gestionnaire de serveur et sélectionnez Promouvoir ce serveur en contrôleur de domaine.
2. Sur la page Configuration de déploiement, sélectionnez l'option Ajouter une nouvelle forêt.
3. Saisissez le nom de domaine racine : horizon.local.

<img width="516" height="364" alt="3  Add new forest" src="https://github.com/user-attachments/assets/aecb8f32-0dea-4ee0-9190-6f26daade719" />

4. Configurez le mot de passe DSRM (Directory Services Restore Mode), indispensable pour la maintenance de la base de données AD en cas de corruption.
5. Poursuivez jusqu'à l'étape de vérification.

## 4. Vérification des prérequis
Avant de lancer l'installation finale, Windows Server effectue une batterie de tests pour s'assurer que le serveur est prêt (nom correct, IP fixe, espace disque suffisant).

1. Attendez que l'assistant termine l'analyse.
2. Assurez-vous que le message "Toutes les vérifications de la configuration requise ont donné satisfaction" apparaît en haut de la fenêtre.

<img width="516" height="363" alt="4  toutes les vérifications des prérequis ont réussi" src="https://github.com/user-attachments/assets/e96fc208-767a-4f00-9520-247b99c3b582" />

3. Cliquez sur Installer. Le serveur redémarrera automatiquement à la fin du processus.

## 5. Validation de l'installation et Connexion
Après le redémarrage, le serveur fait officiellement partie du domaine HORIZON.

1. Sur la mire de connexion, utilisez le format suivant pour vous identifier : HORIZON\Administrateur.
2. Entrez le mot de passe défini lors de l'installation initiale du système.

<img width="508" height="382" alt="5  Connexion nouvel utilisateur" src="https://github.com/user-attachments/assets/b7c76570-36c0-4d25-8c87-19396117d3fa" />


## 6. Structuration de l'Annuaire (OU)
Conformément au contexte métier, l'annuaire doit être organisé pour faciliter l'application des futures stratégies de groupe (GPO).

1. Exécutez la commande suivante ou recherchez l'outil dans le menu Démarrer :
2. Dans la console Utilisateurs et ordinateurs Active Directory, faites un clic droit sur le domaine horizon.local.
3. Créez les trois Unités d'Organisation (OU) suivantes :
  - OU_Direction
  - OU_Permanents
  - OU_Benevoles

<img width="511" height="362" alt="6  Mise en place OU_" src="https://github.com/user-attachments/assets/4d4244c8-2187-4fa2-a42f-54d42978197e" />

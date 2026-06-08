# Fiche Technique : Audit, Nettoyage et Sécurisation des Postes Clients
## 1. Objectifs
- Identifier les privilèges excessifs sur les postes clients (Audit).
- Créer un compte d'administration local de secours (Support_Tech) pour le helpdesk.
- Préparer la rétrogradation des utilisateurs en "Utilisateurs standards" pour réduire la surface d'attaque.

## 2. Audit de l'état initial (Preuve "Avant" migration)
Avant toute modification, il est impératif de documenter l'état de la machine. Actuellement, dans l'association, les salariés sont administrateurs de leur propre poste, ce qui représente un risque de sécurité majeur.

- Ouvrez PowerShell en tant qu'administrateur.
- Exécutez la commande suivante pour lister les membres ayant les pleins pouvoirs sur la machine :

<img width="487" height="320" alt="1  Get-LocalUser _ Support tech" src="https://github.com/user-attachments/assets/fa071eea-ad17-425a-b8bd-5f519868718d" />

Note : Cette capture prouve que l'utilisateur final (Marc) dispose encore des droits administrateurs avant la migration. Le compte Support_Tech a déjà été anticipé.

## 3. Création du compte de secours Helpdesk et attribution des privilèges administratifs
Pour éviter d'être bloqué si la jonction au domaine échoue ou si le compte utilisateur est verrouillé, nous créons un compte de maintenance local robuste.
1. Définissez le mot de passe sécurisé
2. Créez le compte utilisateur local
3. Vérifiez la présence du compte
4. Ajoutez le compte au groupe

<img width="485" height="140" alt="2  Liste utilisateur (administrateurs)" src="https://github.com/user-attachments/assets/4be59f7e-36f6-4b32-aa69-9d94f2054cfd" />

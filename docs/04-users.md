# Fiche Technique : Gestion des Identités et Délégation de Droits
## 1. Objectifs
- Peupler l'annuaire Active Directory de manière automatisée via PowerShell.
- Appliquer une politique de sécurité forçant le changement de mot de passe à la première connexion.
- Déléguer la gestion des mots de passe aux responsables d'Unités d'Organisation (OU) pour décharger le support central.

## 2. Automatisation de la création des comptes
Pour éviter les erreurs humaines et gagner du temps, nous utilisons un script PowerShell pour injecter les comptes dans les trois OU cibles : OU_Direction, OU_Permanents et OU_Benevoles.
Configuration du script :
- Identifiants : Création de 5 comptes Direction (Dir_i), 10 comptes Permanents (Perm_i) et 5 comptes Bénévoles (Ben_i).
- Sécurité : L'attribut -ChangePasswordAtLogon $true est systématiquement appliqué pour que chaque utilisateur soit le seul à connaître son mot de passe final.

<img width="317" height="216" alt="6  Script ajout membres réseau" src="https://github.com/user-attachments/assets/8c75385d-b138-4cba-8f99-29d5834379b6" />

Le script définit les chemins LDAP des OU et utilise des boucles for pour automatiser la création via la commande New-ADUser.

## 3. Validation de la structure de l'annuaire
Une fois le script exécuté, la console Utilisateurs et ordinateurs Active Directory (dsa.msc) permet de valider la bonne répartition des 20 objets utilisateurs.
- Direction (5 utilisateurs) : Comptes de Dir_1 à Dir_5.
- Permanents (10 utilisateurs) : Comptes de Perm_1 à Perm_10.
- Bénévoles (5 utilisateurs) : Comptes de Ben_1 à Ben_5.

<img width="374" height="170" alt="7 3 membre permanent" src="https://github.com/user-attachments/assets/7d87ba8f-6d9f-4a73-ac24-5a31ac138692" />
<img width="374" height="155" alt="7 2 membre direction" src="https://github.com/user-attachments/assets/718987a7-d96f-4454-8664-3e1e58b488b7" />
<img width="374" height="146" alt="7 membre benevole" src="https://github.com/user-attachments/assets/4e13652f-a89e-4fec-8302-bd4f47c721af" />

## 4.Mise en place de la Délégation de Contrôle
Dans une optique de sécurité et d'agilité, il est nécessaire de permettre à certains utilisateurs (ex: Dir_1) de gérer les incidents mineurs de leur département, comme l'oubli de mot de passe, sans leur donner de droits d'Administrateur du Domaine.
Procédure :
1. Faites un clic droit sur l'OU cible (ex: OU_Direction) et sélectionnez Déléguer le contrôle.
2. Ajoutez l'utilisateur ou le groupe responsable (ex: Dir_1).
3. Sélectionnez la tâche commune : "Réinitialiser les mots de passe utilisateur et forcer le changement de mot de passe à la prochaine ouverture de session".

<img width="253" height="206" alt="8  dir 1 - Creation mdp et modif mdp" src="https://github.com/user-attachments/assets/a0fce855-117f-4101-9e29-b515925e678f" />

**Confidentialité** : Aucun administrateur ne connaît le mot de passe final des utilisateurs.
**Efficience du Support** : Les responsables d'OU peuvent débloquer leurs collaborateurs instantanément via la délégation, réduisant le nombre de tickets pour le support technique central.
**Moindre privilège** : Dir_1 peut modifier les mots de passe de son équipe mais n'a aucun droit de modification sur les serveurs ou les autres départements.

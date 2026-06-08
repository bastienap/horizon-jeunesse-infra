# Fiche Technique : Migration et Intégration au Domaine
## 1. Objectifs
- Configurer la résolution DNS du client vers le contrôleur de domaine (DC).
- Joindre la machine Windows 11 au domaine Active Directory.
- Valider le changement d'appartenance du poste (passage de Workgroup à Domaine).

## 2. Configuration Réseau (Le prérequis vital)
Pour qu'une machine puisse joindre un domaine, elle doit impérativement être capable de localiser le contrôleur de domaine via le DNS. Si le DNS pointe vers une adresse externe (comme Google ou une box internet), la jonction échouera systématiquement.

1. Sur le poste PC-PERM-01, ouvrez les Connexions réseau.
2. Accédez aux propriétés de la carte Ethernet, puis aux propriétés du Protocole Internet version 4 (TCP/IPv4).
3. Configurez l'adresse IP statique du client (ex: 192.168.10.20) et fixez le Serveur DNS préféré sur l'adresse IP du serveur SRV-DC01 : 192.168.10.10.

<img width="511" height="354" alt="3  IPv4 Serveur" src="https://github.com/user-attachments/assets/9c89a424-5948-4fba-876b-8f6c1b4a54ed" />


## 3. Procédure de Jonction au Domaine
Une fois la connectivité DNS validée (testable via un ping horizon.local), vous pouvez procéder à l'intégration système.

1. Allez dans Paramètres > Système > Informations système.
2. Cliquez sur Paramètres avancés du système, puis sur l'onglet Nom de l'ordinateur.
3. Cliquez sur le bouton Modifier.
4. Dans la section "Membre d'un", sélectionnez Domaine et saisissez : horizon.local.
5. Une fenêtre d'authentification s'ouvre : utilisez les identifiants de l'administrateur du domaine (ex: HORIZON\Administrateur) pour autoriser l'opération.

<img width="308" height="167" alt="4  Bienvenu sereur" src="https://github.com/user-attachments/assets/df6db063-ccc4-4283-8393-0fdaf01bbcce" />


## 4. Validation Post-Migration
Après avoir cliqué sur OK, Windows vous demandera de redémarrer la machine pour appliquer les modifications.

1. Redémarrez le poste client.
2. À l'écran de verrouillage, connectez-vous avec un compte du domaine (ex: Administrateur@horizon.local).
3. Pour vérifier la réussite, faites un clic droit sur Ce PC > Propriétés.
4. Vérifiez que la section "Nom de l'appareil" affiche désormais le nom complet du domaine.

<img width="275" height="326" alt="5  Domaine Horizon Local" src="https://github.com/user-attachments/assets/94129afe-8a72-4aa3-9ccc-b830e967abcb" />

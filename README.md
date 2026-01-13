# Lab Active Directory – Windows Server 2022

## Présentation du projet
Ce projet vise à mettre en place un environnement Active Directory sous Windows Server 2022 dans un environnement virtualisé.  Il comprend l’installation des rôles AD DS et DNS, la création du domaine lab.local, ainsi que la mise en place d’une unité d’organisation et d'un compte utilisateur.  Un poste client Windows a été configuré et joint au domaine afin de valider le bon fonctionnement de l’authentification Active Directory.

## Compétences développées
- Administration de base de Windows Server
- Active Directory (niveau débutant)
- Gestion des comptes utilisateurs
- Compréhension des environnements d’entreprise
- Méthodologie et documentation technique

## Environnement & outils
- Windows Server 2022
- Active Directory Domain Services (AD DS)
- Machine virtuelle (VMware)
- Client Windows (pour tests de domaine)

## Configuration réalisée
### Installation de Windows Server 2022
- Création d’une machine virtuelle pour Windows server 2022
	- OS: Windows
	- Version: Windows Server 2022
	- Ressources attribuées :
		- 60 Go de disque
		- 4069 Mo de mémoire
		- 4 CPU
	- ISO: Windows Server 2022
	- Carte réseau en mode ‘Custom - Host-Only’
###### *Ref 1 - Paramètres de la machine virtuelle pour Windows Server 2022*
<img width="328" height="326" alt="SRV_AD_LAB-VM" src="https://github.com/user-attachments/assets/dfa8aa2b-1f73-44b8-92bd-400a34259773" />

- Installation de Windows Server 2022
	- La VM a été démarée.
	- La langue a installer, la langue du clavier et le format horaire ont été configurés.
	- Windows Server 2022 Standard Evaluation (Experience du bureau) a été sélectionné comme système d'exploitation a installer.
	- Les termes du contrat de licence logiciel de Microsoft ont été acceptés.
	- L’option 'personalisé' a été choisie pour l'installation.
	- Le  lecteur a été sélectionné et puis l’installation a été finalisée en cliquant 'Installer'.
	
- Configuration de base du serveur
	- Une fois le système redémaré, un mot de passe pour le compte Administrateur a été créé.
	- Avec le nouveau mot de passe, le compte Adminastrateur a été déverouillé.
	- Dans le **Gestionnaire de serveur**, l'onglet 'Serveur Local'
		- L'ordinateur a été renommé SVR-LAB et puis redémaré.
		- Les paramètres IP ont été configurés:
			- Addresse IP: 192.168.1.253
			- Masque de sous-réseau: 255.255.255.0
			- Passerelle par défault: 192.168.1.254
			- Serveur DNS préféré: 192.168.1.254
		- La configuration de sécurité renforcée d'Internet Explorer a été désactivée pour les administrateurs et les utilisateurs.
###### *Ref 2 - Creation d'un mot de passe pour le compte Administrateur*
<img width="450" height="350" alt="SVR_AD_LAB-MDP" src="https://github.com/user-attachments/assets/56af630a-959e-491c-ac03-cd2914715061" />

###### *Ref 3 - Les Paramètres IP du serveur*
<img width="270" height="320" alt="SRV_AD_LAB-resau" src="https://github.com/user-attachments/assets/248b269d-db1b-4c04-855d-d8a49ddb6d3a" />

- Test de connectivité
	- Le routeur a été pingé depuis le serveur AD.
###### *Ref 4 - Test de ping entre le serveur et le routeur*
<img width="600" height="400" alt="SRV_AD_LAB-testconnectivite" src="https://github.com/user-attachments/assets/f19b09c3-6e1a-4a50-afec-d6bb36c250ce" />

### Configuration des rôles Active Directory Domain Services (AD DS) et DNS
- Une fois l’assistant d’installation lancé, les étapes suivantes ont été réalisées:
	- Avant de commencer l'installation, une vérification des conditions préalables a été effectuée.
	- L’option 'Installation basée sur un rôle ou une fonctionnalité' a été sélectionnée.
	- Le serveur SVR-LAB a été choisi comme serveur de destination pour l’installation des rôles et fonctionnalités.
	- Les fonctionnalités requises pour les rôles DNS et AD DS ont été ajoutées automatiquement.
	- Les sélections d’installation ont été confirmées, puis l’installation a été lancée.
	- Une fois l’installation terminée, le serveur a été redémarré.
	- Après le redémarrage, une installation post-déploiement a été réalisée afin de promouvoir le serveur en contrôleur de domaine.
###### *Ref 5 - Sélection des rôles Active Directory Domain Services (AD DS) et DNS*
<img width="396" height="284" alt="SRV_AD_LAB-service AD-DNS" src="https://github.com/user-attachments/assets/fc5b3f27-d603-48ed-8b86-d6136521a083" />


###### *Ref 6 - Installation post-déploiement du contrôleur de domaine*
<img width="515" height="209" alt="SRV_AD_LAB-Post-deploiement" src="https://github.com/user-attachments/assets/09ecd6e7-0f60-4250-9202-9ebf69e4af4a" />


### Installation post-déploiement
- Une nouvelle forêt a été créée avec le nom de domaine racine: lab.local.
- Un mot de passe pour le mode de restauration des services d’annuaire (DSRM) a été défini..
- Le nom de domaine NetBIOS a été généré automatiquement.
- L’emplacement par défaut de la base de données AD DS a été conservé,
- Après vérification des sélections effectuées, la configuration requise a été validée afin de lancer la promotion du serveur en contrôleur de domaine.
###### *Ref 7 - Création d'une nouvelle forêt*
<img width="385" height="285" alt="SRV_AD_LAB-lab local" src="https://github.com/user-attachments/assets/ded1b7f0-4caf-46f7-8f0d-bcbe4ae5d3b9" />

###### *Ref 8 - Création d'un mot de passe pour le mode de restauration des services d’annuaire (DSRM)*
<img width="385" height="286" alt="SRV_AD_LAB-MDP-DSRM" src="https://github.com/user-attachments/assets/9958d5f2-89ea-432a-acea-566b84ce4052" />

###### *Ref 9 -  Paramtere des services de domaine AD*
<img width="386" height="287" alt="SRV_AD_LAB-options" src="https://github.com/user-attachments/assets/05334560-da25-4599-aaf1-927791660c7f" />

### Organisation de l’AD
- Creation d'une console MMC
	- Les composants logiciels enfichables « Utilisateurs et ordinateurs Active Directory » et « Gestion des stratégies de groupe » ont été ajoutés.
	- La console a été renommée « Console_AD » afin de faciliter l’administration du domaine.
*Cette console MMC permet de centraliser les outils d’administration Active Directory et des stratégies de groupe au sein d’une interface unique, améliorant ainsi l’efficacité et la lisibilité des tâches d’administration.*
###### *Ref 10 - L'ajout des composants logiciels enfichables*
<img width="380" height="262" alt="SRV_AD_LAB-MMC" src="https://github.com/user-attachments/assets/74d8d74c-4273-48ff-a911-32049e80ff99" />

###### *Ref 11 - La racine de la Console_AD*
<img width="380" height="92" alt="SRV_AD_LAB-MMC2" src="https://github.com/user-attachments/assets/df818acc-6383-4164-b840-a3d07f763d84" />

- Création d’une Unité d’organisation
	- Depuis la console MMC, une nouvelle unité d’organisation a été créée et nommée « LAB_Test », afin d’organiser les objets liés à l’environnement de test.
	- En suite un nouvel utilisateur, Tech, a été crée et son mot de passe definie.
	- Finalement, le compte Tech a été activé.
###### *Ref 12 - Création d'une nouvelle unité d'organisation*
<img width="416" height="218" alt="SVR_AD_LAB-UO-LAB_Test" src="https://github.com/user-attachments/assets/54cb39d3-48d4-4ed4-bb0a-b189db11746c" />

###### *Ref 13 - Création d’un compte utilisateur*
<img width="415" height="215" alt="SVR_AD_LAB-userTech" src="https://github.com/user-attachments/assets/1bc7b9f8-63ea-49a9-ac7a-36aacbd2be6f" />

###### *Ref 14 - Création d’un mot de passe pour le compte utilisateur*
<img width="415" height="214" alt="SVR_AD_LAB-UO-userMDP" src="https://github.com/user-attachments/assets/4346b297-d4ed-4c1c-b1b2-bff3388c39c2" />

###### *Ref 15 - Finalisation de la création du compte Tech*
<img width="416" height="217" alt="SVR_AD_LAB-OUterminer" src="https://github.com/user-attachments/assets/6081b306-68b4-407e-a060-adc48b11699c" />

### L'ajout d'un poste client au domaine
- Une vérification des conditions préalables a été effectuée :
	- Le poste client et le serveur étaient connectés au même réseau.
	- Un compte administrateur était disponible pour l’intégration.
- Une fois connecté au compte administrateur du poste client, l’adresse du serveur DNS (192.168.1.253) a été configurée. 
- Le domaine, lab.local, a ensuite été renseigné.
- Les identifiants de l’administrateur du domaine (nom d’utilisateur et mot de passe) ont été saisis pour valider l’ajout au domaine.
- Un message de confirmation est apparu, puis la machine a été redémarrée.
- Enfin, le compte Tech a été utilisé pour se connecter avec succès au domaine.
###### *Ref 16 - Configuration de l'addresse du serveur DNS*
<img width="300" height="400" alt="SVR_AD_LAB-pcdns" src="https://github.com/user-attachments/assets/0f364c9c-d0c8-45aa-b91e-c0524cf87bac" />

###### *Ref 17 - Renseignement du domain « lab.local »*
<img width="300" height="400" alt="SVR_AD_LAB-Domain" src="https://github.com/user-attachments/assets/62d5d886-37bb-48b2-b33e-0187180a9477" />

###### *Ref 18 - Authentification de l’administrateur du domaine*
<img width="250" height="200" alt="SVR_AD_LAB-domain2" src="https://github.com/user-attachments/assets/6b978c5b-9ac3-44d7-bfe3-8ff707923ee7" />

###### *Ref 19 - Confirmation de l’ajout du poste client au domaine*
<img width="180" height="130" alt="SVR_AD_LAB-Yourein" src="https://github.com/user-attachments/assets/e8c97db9-d5f8-4354-8920-20a56d9e0523" />

###### *Ref 20 - Connexion au compte Tech*
<img width="200" height="221" alt="SVR_AD_LAB-Signin" src="https://github.com/user-attachments/assets/8f23a91e-5e94-4e67-a2ad-75766d581ba3" />

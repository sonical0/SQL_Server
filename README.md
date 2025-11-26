SANCHEZ Alexandre
26/11/2025
Virtual box - Windows Server 2016
Microsoft SQL Server Management

# Introduction

# Labo 1 – Installation et paramétrage de l’instance MKTGDEV
## Objectif
Installer et configurer une instance SQL Server nommée MKGTDEV, en respectant les consignes suivantes : installation du moteur de base uniquement, répertoires par défaut situés sur les disques D: et L:, activation du mode d’authentification mixte, configuration des services SQL Server et SQL Server Agent en démarrage automatique, ajout d’un administrateur SQL.

## Spécifications
- Instance : MKTGDEV
- Fonctionnalités installées : Moteur de base de données SQL Server uniquement
- Répertoires par défaut :
  - Données (DATA) : D:\MKGTDEV
  - Journaux (LOG) : L:\MKGTDEV
- Mode d’authentification : Mixte (Windows + SQL Server)
- Compte administrateur SQL ajouté : utilisateur local
- Services configurés :
  - SQL Server (MKTGDEV) : démarrage automatique
  - SQL Server Agent (MKTGDEV) : démarrage automatique

## Marche à suivre

## Résultats (captures d’écran)
- **C01_L1_Connexion_SSMS.png**  
    _(Zone pour coller la capture)_
    
- **C02_L1_Mode_Authentification.png**  
    _(Zone pour coller la capture)_
    
- **C03_L1_Services_SQL.png**  
    _(Zone pour coller la capture)_
    
- **C04_L1_Options_Stockage.png**  
    _(Zone pour coller la capture)_
    
- **C05_L1_Admin_SQL_Ajouté.png**  
    _(Zone pour coller la capture)_
    
- **C06_L1_Répertoires_Défaut.png**  
    _(Zone pour coller la capture)_
## Remarques / difficultés

# Labo 2 – Création et paramétrage de la base RateTracking
## Objectif
Créer et configurer la base de données RateTracking sur l’instance MKTGDEV, en séparant les fichiers de données et de journaux, en ajoutant les fichiers secondaires selon les besoins, en définissant les groupes de fichiers PRIMARY, USERDATA et ARCHIVE, et en définissant USERDATA comme groupe de fichiers par défaut.

## Spécifications
- Instance cible : MKTGDEV
- Nom de la base : RateTracking

- Fichier principal (PRIMARY) :
  - Nom logique : RateTracking_dat
  - Nom physique : RateTracking.mdf
  - Emplacement : D:\MKGTDEV
  - Taille initiale : 10 MB
  - Croissance : 10 MB
  - Taille maximale : 100 MB

- Fichier journal (LOG) :
  - Nom logique : RateTracking_log
  - Nom physique : RateTracking_log.ldf
  - Emplacement : L:\MKGTDEV
  - Taille initiale : 20 MB
  - Croissance : 20 MB
  - Taille maximale : illimitée

- Fichiers de données USERDATA :
  - RateTracking_dat_1, RateTracking_dat_2, RateTracking_dat_3
  - Emplacement : D:\MKGTDEV
  - Groupe de fichiers : USERDATA
  - Taille initiale : 100 MB
  - Croissance : 50 MB
  - Taille maximale : 500 MB

- Fichier de données ARCHIVE :
  - Nom logique : RateTracking_dat_4
  - Emplacement : D:\MKGTDEV
  - Groupe de fichiers : ARCHIVE
  - Taille initiale : 200 MB
  - Croissance : 100 MB
  - Taille maximale : 1 GB

- Groupe de fichiers par défaut de la base : USERDATA

## Marche à suivre

## Résultats (captures d’écran)
- **C07_L2_Fichiers_RateTracking.png**  
    _(Collez ici la capture montrant tous les fichiers RateTracking)_
    
- **C08_L2_Groupe_Fichiers_Defaut_USERDATA.png**  
    _(Collez ici la capture montrant USERDATA comme groupe par défaut)_
    
- **C09_L2_Récapitulatif_Propriétés.png**  
    _(Optionnel selon ton interface ; zone pour coller la capture si tu en as une)_
## Scripts utilisés

## Remarques / difficultés


# Labo 2’ – Reparamétrage de tempdb
## Objectif
Reconfigurer la base système tempdb conformément aux exigences : modifier les emplacements des fichiers de données et de journal vers les disques D: et L:, ajuster leurs tailles initiales, ajouter les fichiers supplémentaires tempdev2 et tempdev3, puis redémarrer l’instance pour valider les nouveaux paramètres.

## Spécifications
- Base concernée : tempdb

- Fichier principal (tempdev) :
  - Nom logique : tempdev
  - Emplacement : D:\MKGTDEV
  - Taille initiale : 30 MB
  - Croissance : 10 MB
  - Taille maximale : illimitée

- Fichier journal (templog) :
  - Nom logique : templog
  - Emplacement : L:\MKGTDEV
  - Taille initiale : 10 MB
  - Croissance : 10 MB
  - Taille maximale : illimitée

- Fichier secondaire tempdev2 :
  - Emplacement : D:\MKGTDEV
  - Taille initiale : 20 MB
  - Croissance : 10 MB
  - Taille maximale : illimitée

- Fichier secondaire tempdev3 :
  - Emplacement : D:\MKGTDEV
  - Taille initiale : 20 MB
  - Croissance : 10 MB
  - Taille maximale : illimitée

- Opération finale nécessaire : redémarrage de l’instance SQL Server pour prise en compte des modifications.

## Marche à suivre

## Résultats (captures d’écran)
- **C10_L2p_Script_tempdb.png**  
    _(Collez ici la capture du script ALTER DATABASE)_
    
- **C11_L2p_Propriétés_tempdb_Fichiers.png**  
    _(Collez ici la capture des fichiers tempdb dans SSMS)_
    
- **C12_L2p_Emplacements_tempdb.png**  
    _(Collez ici la capture montrant D:\MKGTDEV et L:\MKGTDEV)_
## Scripts utilisés
Aucun script utilisé — configuration réalisée intégralement via l’interface graphique de SSMS.
## Remarques / difficultés


# Labo 3 – Sauvegarde et restauration d’AdventureWorks
## Objectif
Réaliser différentes opérations de sauvegarde de la base AdventureWorks : effectuer une sauvegarde complète non compressée puis une sauvegarde complète compressée, comparer les tailles obtenues, puis mettre en place un plan de maintenance automatisé incluant des sauvegardes incrémentielles et une sauvegarde complète hebdomadaire dans le répertoire U:\BKPMKGTDEV.

## Spécifications
- Base concernée : AdventureWorks
- Répertoire de sauvegarde : U:\BKPMKGTDEV

- Sauvegarde complète non compressée :
  - Type : Full backup
  - Compression : Désactivée
  - Destination : U:\BKPMKGTDEV

- Sauvegarde complète compressée :
  - Type : Full backup
  - Compression : Activée
  - Destination : U:\BKPMKGTDEV

- Plan de maintenance (méthode 1) :
  - Sauvegardes incrémentielles :
    - Lundi à 05h00
    - Mercredi à 05h00
    - Vendredi à 19h00
  - Sauvegarde complète :
    - Dimanche à 03h00

- SQL Server Agent Jobs (méthode 2) :
  - Reprise identique du planning ci-dessus
  - Un job dédié aux sauvegardes incrémentielles
  - Un job dédié à la sauvegarde complète

## Marche à suivre

## Résultats (captures d’écran)
### 1. Présence de la base

- **C13_L3_Base_AdventureWorks.png**  
    _(Collez ici la capture)_
    

### 2. Sauvegarde complète non compressée

- **C14_L3_Sauvegarde_NonCompressée_Config.png**  
    _(Zone pour coller la capture)_
    
- **C15_L3_Fichier_NonCompressé.png**  
    _(Zone pour coller la capture du fichier .bak non compressé dans U:)_
    

### 3. Sauvegarde complète compressée

- **C16_L3_Sauvegarde_Compressée_Config.png**  
    _(Zone pour coller la capture)_
    
- **C17_L3_Fichier_Compressé.png**  
    _(Zone pour coller la capture du fichier compressé dans U:)_
### 4. Tableau comparatif

| Type           | Taille obtenue       | Répertoire    | Commentaire          |
| -------------- | -------------------- | ------------- | -------------------- |
| Non compressée | **(insérer taille)** | U:\BKPMKGTDEV | Taille plus élevée   |
| Compressée     | **(insérer taille)** | U:\BKPMKGTDEV | Compression efficace |
### 5. Plan de maintenance

- **C18_L3_Plan_Maintenance.png**  
    _(Zone pour coller la capture du plan complet)_
    

### 6. Planifications détaillées

- **C19_L3_Planif_Complet_3h.png**  
    _(Dimanche 03h00)_
    
- **C20_L3_Planif_Incr_LuMe_5h.png**  
    _(Lundi & Mercredi 05h00)_
    
- **C21_L3_Planif_Incr_Vend_19h.png**  
    _(Vendredi 19h00)_
    

### 7. Jobs SQL Server Agent

- **C22_L3_Jobs_List.png**  
    _(Liste complète des jobs)_
    
- **C23_L3_Job_Complete_Etapes.png**  
    _(Détail des étapes du job de sauvegarde complète)_
    
- **C24_L3_Job_Complete_Planif.png**  
    _(Détail de la planification du job)_
# Labo 4 – Connexions et droits d’accès
## Objectif
Créer et configurer quatre connexions pour la base AdventureWorks : deux logins en mode mixte (consult et redact) et deux logins Windows (User1 et User2). Associer chacun de ces logins à un utilisateur dans la base AdventureWorks, et attribuer les autorisations correspondant aux besoins : lecture seule pour consult et User1, accès total pour redact et User2.

## Spécifications
- Base concernée : AdventureWorks

- Logins en mode mixte :
  - consult
    - Mot de passe : C0nsulT
    - Type d’accès : Lecture seule (db_datareader)
  - redact
    - Mot de passe : REd@cT
    - Type d’accès : Accès total (db_owner)

- Logins Windows :
  - User1
    - Type d’accès : Lecture seule (db_datareader)
  - User2
    - Type d’accès : Accès total (db_owner)

- Mappage utilisateur :
  - Chaque login est associé à un utilisateur correspondant dans la base AdventureWorks.

## Marche à suivre

## Résultats (captures d’écran)
- **C25_L4_Logins.png**  
    _(Liste des connexions dans SSMS)_
    
- **C26_L4_Consult.png**  
    _(Mappage user + rôle db_datareader)_
    
- **C27_L4_Redact.png**  
    _(Mappage user + rôle db_owner)_
    
- **C28_L4_User1.png**  
    _(Mappage user1 + rôle db_datareader)_
    
- **C29_L4_User2.png**  
    _(Mappage user2 + rôle db_owner)_
    
- **C30_L4_Users_DB.png**  
    _(Liste des utilisateurs dans la base AdventureWorks)_


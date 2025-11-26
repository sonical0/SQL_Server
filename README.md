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

## Résultats (captures d'écran)
![Connexion SSMS](TP_SQL_Screenshots/C01_L1_Instance_MKTGDEV.png)
<p align="center"><i>Connexion SSMS</i></p>

![Mode Authentification](TP_SQL_Screenshots/C02_L1_RepDefaut.png)
<p align="center"><i>Mode Authentification</i></p>

![Services SQL](TP_SQL_Screenshots/C03_L1_ModeMixte.png)
<p align="center"><i>Services SQL</i></p>

![Options Stockage](TP_SQL_Screenshots/C04_L1_Services.png)
<p align="center"><i>Options Stockage</i></p>

![Admin SQL Ajouté](TP_SQL_Screenshots/C05_L1_Connexions.png)
<p align="center"><i>Admin SQL Ajouté</i></p>

![Répertoires Défaut](TP_SQL_Screenshots/C06_L2_RateTracking_Liste.png)
<p align="center"><i>Répertoires Défaut</i></p>
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

## Résultats (captures d'écran)
![Fichiers RateTracking](TP_SQL_Screenshots/C07_L2_Fichiers.png)
<p align="center"><i>Fichiers RateTracking</i></p>

![Groupe Fichiers Defaut USERDATA](TP_SQL_Screenshots/C08_L2_GroupeDefaut.png)
<p align="center"><i>Groupe Fichiers Defaut USERDATA</i></p>
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

## Résultats (captures d'écran)
![Script tempdb](TP_SQL_Screenshots/C10_L2p_Script_tempdb.png)
<p align="center"><i>Script tempdb</i></p>

![Propriétés tempdb Fichiers](TP_SQL_Screenshots/C11_L2p_Fichiers_tempdb.png)
<p align="center"><i>Propriétés tempdb Fichiers</i></p>

![Emplacements tempdb](TP_SQL_Screenshots/C12_L2p_Emplacements_tempdb.png)
<p align="center"><i>Emplacements tempdb</i></p>
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

![Base AdventureWorks](TP_SQL_Screenshots/C13_L3_AdventureWorks.png)
<p align="center"><i>Base AdventureWorks</i></p>

### 2. Sauvegarde complète non compressée

![Sauvegarde NonCompressée Config](TP_SQL_Screenshots/C14_L3_Sauvegarde_NonComp.png)
<p align="center"><i>Sauvegarde NonCompressée Config</i></p>

![Fichier NonCompressé](TP_SQL_Screenshots/C15_L3_Fichier_NonComp.png)
<p align="center"><i>Fichier NonCompressé</i></p>
    

### 3. Sauvegarde complète compressée

![Sauvegarde Compressée Config](TP_SQL_Screenshots/C16_L3_Sauvegarde_Comp.png)
<p align="center"><i>Sauvegarde Compressée Config</i></p>

![Fichier Compressé](TP_SQL_Screenshots/C17_L3_Fichier_Comp.png)
<p align="center"><i>Fichier Compressé</i></p>

### 5. Plan de maintenance

![Plan Maintenance](TP_SQL_Screenshots/C18_L3_Plan_Maintenance.png)
<p align="center"><i>Plan Maintenance</i></p>

### 6. Planifications détaillées

![Planif Complet 3h](TP_SQL_Screenshots/C19_L3_Planif_Complet.png)
<p align="center"><i>Planif Complet 3h</i></p>

![Planif Incr LuMe 5h](TP_SQL_Screenshots/C20_L3_Planif_Incr_LuMe.png)
<p align="center"><i>Planif Incr LuMe 5h</i></p>

![Planif Incr Vend 19h](TP_SQL_Screenshots/C21_L3_Planif_Incr_Vend.png)
<p align="center"><i>Planif Incr Vend 19h</i></p>
    

### 7. Jobs SQL Server Agent

![Jobs List](TP_SQL_Screenshots/C22_L3_Jobs_List.png)
<p align="center"><i>Jobs List</i></p>

![Job Complete Etapes](TP_SQL_Screenshots/C23_L3_Job_Complete_Etapes.png)
<p align="center"><i>Job Complete Etapes</i></p>

![Job Complete Planif](TP_SQL_Screenshots/C24_L3_Job_Complete_Planif.png)
<p align="center"><i>Job Complete Planif</i></p>
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

## Résultats (captures d'écran)
![Logins](TP_SQL_Screenshots/C25_L4_Logins.png)
<p align="center"><i>Logins</i></p>

![Consult](TP_SQL_Screenshots/C26_L4_Consult.png)
<p align="center"><i>Consult</i></p>

![Redact](TP_SQL_Screenshots/C27_L4_Redact.png)
<p align="center"><i>Redact</i></p>

![User1](TP_SQL_Screenshots/C28_L4_User1.png)
<p align="center"><i>User1</i></p>

![User2](TP_SQL_Screenshots/C29_L4_User2.png)
<p align="center"><i>User2</i></p>

![Users DB](TP_SQL_Screenshots/C30_L4_Users_DB.png)
<p align="center"><i>Users DB</i></p>


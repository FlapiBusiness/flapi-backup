
# **Flapi - Backup Database**

## 🚀 **Description**

**Flapi - Backup Database** est un workflow automatisé qui permet d'effectuer des sauvegardes régulières des bases de données MariaDB/MySQL d'un serveur O2Switch. Chaque base de données est sauvegardée individuellement dans un fichier compressé (`.sql.gz`), puis transférée sur **deux serveurs FTP distincts** : **OVH** et **O2Switch** pour garantir la redondance des sauvegardes.

Ce projet utilise **GitHub Actions** pour automatiser l'exécution du processus de sauvegarde toutes les 12 heures.

---

<br /><br />

## 🛠️ **Fonctionnalités**

1. **Sauvegarde individuelle des bases de données** :  
   Chaque base de données est exportée séparément au format `.sql.gz` via `mysqldump`.

2. **Automatisation avec GitHub Actions** :  
   Le workflow est déclenché toutes les 12 heures via une tâche planifiée `cron`.

3. **Transfert sécurisé vers deux serveurs FTP** :  
   Les fichiers de sauvegarde sont automatiquement transférés sur :
    - **Serveur FTP O2Switch** : Sauvegarde locale pour les utilisateurs du service O2Switch.
    - **Serveur FTP OVH** : Sauvegarde externe pour redondance et sécurité.

4. **Gestion des noms de fichiers** :  
   Chaque sauvegarde possède un nom unique avec un horodatage pour faciliter l'identification.

---

<br /><br />

## 📂 **Structure du projet**

```plaintext
.
├── .github/
│   └── workflows/
│       └── backup_database.yml   # Le workflow GitHub Actions pour exécuter la sauvegarde
└── README.md                     # Documentation du projet
```

---

<br /><br />

## 🔧 **Configuration**

### 1. **Ajout des secrets GitHub**
Ajoute les clés suivantes dans la section **Settings > Secrets and variables > Actions** de ton dépôt GitHub :

- `O2SWITCH_BACKUP_DATABASE_HOST`
- `O2SWITCH_BACKUP_DATABASE_USERNAME`
- `O2SWITCH_BACKUP_DATABASE_PASSWORD`
- `O2SWITCH_FTP_HOST`,
- `O2SWITCH_FTP_USERNAME`,
- `O2SWITCH_FTP_PASSWORD`
- `OVH_FTP_HOST`,
- `OVH_FTP_USERNAME`,
- `OVH_FTP_PASSWORD`

---

<br /><br />

## 🔄 **Exécution**

Le workflow est exécuté automatiquement toutes les **12 heures** à 00h00 et 12h00. Tu peux également l'exécuter manuellement via **Actions > Run workflow**.

---

<br /><br />

## 🛡️ **Redondance des sauvegardes**

Les sauvegardes sont envoyées sur deux serveurs FTP distincts :
1. **Serveur FTP O2Switch** : Sauvegarde locale pour un accès rapide.
2. **Serveur FTP OVH** : Sauvegarde externe pour assurer une redondance sécurisée.

---

<br /><br />

## 📥 **Téléchargement des sauvegardes**

Les fichiers de sauvegarde sont nommés avec un horodatage unique :  
`reco5282_<nom_db_client>_backup-<dd-mm-yyyy-hh-mm-ss>.sql.gz`

Ils sont disponibles dans les répertoires suivants :
- **Serveur FTP O2Switch** : `/backup-database/mariadb/`
- **Serveur FTP OVH** : `/backup-database/mariadb/`

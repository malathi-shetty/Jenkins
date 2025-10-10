# Jenkins Backup Guide

Backing up Jenkins is crucial to ensure that jobs, configurations, and plugins are not lost in case of failures. Below are various methods to back up Jenkins safely.

## 1. What to Back Up in Jenkins?
Jenkins stores all its critical data inside the **JENKINS_HOME** directory. You should back up the following:

- **Jenkins Home Directory** (`$JENKINS_HOME` or `/var/lib/jenkins/`)
- **Jobs Configuration** (`$JENKINS_HOME/jobs/`)
- **User Configuration** (`$JENKINS_HOME/users/`)
- **Plugins** (`$JENKINS_HOME/plugins/`)
- **Secrets & Credentials** (`$JENKINS_HOME/secrets/`)
- **Build History** (`$JENKINS_HOME/jobs/*/builds/`)
- **Global Configuration** (`$JENKINS_HOME/config.xml`)
- **Nodes Configuration** (`$JENKINS_HOME/nodes/`)

## 2. Backup Methods

### Method 1: Manual Backup (Copy Jenkins Home Directory)
#### Steps:
1. **Stop Jenkins** to avoid inconsistencies.
   ```bash
   sudo systemctl stop jenkins
   ```
2. **Copy Jenkins Home Directory** to a backup location.
   ```bash
   sudo cp -r /var/lib/jenkins /backup/jenkins_backup_$(date +%F)
   ```
3. **Start Jenkins again** after backup.
   ```bash
   sudo systemctl start jenkins
   ```
4. **Optional:** Compress the backup for storage efficiency.
   ```bash
   tar -czvf /backup/jenkins_backup_$(date +%F).tar.gz /backup/jenkins_backup_$(date +%F)
   ```

### Method 2: Using Jenkins ThinBackup Plugin
This plugin allows scheduled and manual backups within Jenkins.

#### Steps:
1. **Install the ThinBackup Plugin**
   - Go to **Manage Jenkins** → **Manage Plugins** → **Available**
   - Search for **ThinBackup** and install it.
   - Restart Jenkins.

2. **Configure ThinBackup**
   - Go to **Manage Jenkins** → **ThinBackup**
   - Set **Backup Directory** (e.g., `/backup/jenkins-thinbackup/`).
   - Set **Schedule** for automatic backups.
   - Click **Save**.

3. **Run a Backup**
   - Click **Backup Now** to manually trigger a backup.

### Method 3: Using Jenkins Job to Automate Backup
You can create a Jenkins job to schedule backups.

#### Steps:
1. **Create a new job** (Freestyle Project).
2. **Add a build step** → **Execute Shell**.
3. Paste this script:
   ```bash
   #!/bin/bash
   BACKUP_DIR="/backup/jenkins_auto_backup_$(date +%F)"
   sudo mkdir -p $BACKUP_DIR
   sudo cp -r /var/lib/jenkins/* $BACKUP_DIR
   sudo tar -czvf $BACKUP_DIR.tar.gz $BACKUP_DIR
   sudo rm -rf $BACKUP_DIR
   ```
4. **Schedule it** under **Build Triggers** using **Cron syntax**, e.g., `H 2 * * *` (runs at 2 AM daily).
5. sudo visudo
6. jenkins ALL=(ALL) NOPASSWD: /bin/mkdir, /bin/cp, /bin/tar, /bin/rm





## 3. Restoring a Backup

### Manual Restore
1. **Stop Jenkins**
   ```bash
   sudo systemctl stop jenkins
   ```
2. **Restore Jenkins Home Directory**
   ```bash
   sudo cp -r /backup/jenkins_backup_DATE /var/lib/jenkins
   ```
3. **Set Correct Permissions**
   ```bash
   sudo chown -R jenkins:jenkins /var/lib/jenkins
   ```
4. **Start Jenkins**
   ```bash
   sudo systemctl start jenkins
   ```

### ThinBackup Restore
1. Go to **Manage Jenkins** → **ThinBackup**.
2. Select **Restore Backup**.
3. Choose the backup file and restore.

## 4. Best Practices for Jenkins Backup
- **Automate backups** using jobs or cron jobs.
- **Store backups remotely** (AWS S3, Google Drive, etc.).
- **Test restores** regularly to ensure backups are working.
- **Exclude logs and unnecessary files** to reduce backup size.


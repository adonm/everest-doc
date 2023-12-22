# Restore the database from a previously saved backup

Database backups and data replication are complementary components of an effective disaster recovery strategy. 

Everest enables you to use backups to either create a new database or restore the backup data to the original database. Choosing between these two options often depends on the specific scenario, the urgency of recovery, the impact on ongoing operations, the need for data isolation, and the purpose of the restoration (such as testing, recovery from corruption, or analysis).

## Restore database from backup

Restoring to the same cluster is useful in the following scenarios:

- **When restoring from a Point-in-time recovery (PITR) timestamp**: Currently, PITR doesn't support restoration to a new database, making the same cluster restoration essential.
- **For faster recovery**: It's typically quicker to restore data to an existing database as it eliminates the need for creating a new database structure.
- **Database consistency:** Maintains the same database ID, configurations, and dependencies, ensuring consistency within the existing environment.

To restore a database from a backup:
{.power-number}

1. In the <i class="uil uil-database"></i> **Databases** view, select the database you want to restore.
2. Click the <i class="uil uil-ellipsis-h"></i> Actions menu next to the backup you want to restore from, then click **Restore from a backup**.
3. In the **Restore database** popup, specify whether you want to restore from a backup artifact or from a PITR timestamp, in which case you can select the specific recovery point from the drop-down menu.
4. Select **Restore** to restore the backup of your database.

## Restore backup to a new database

There are specific situations that require the creation of a new database from a backup instead of restoring the data to the original database:

- **When the original database is compromised**: Restoring a backup directly to a compromised DB could reintroduce the same issues. Creating a new database from the backup ensures that the restored data is isolated from the original database, preserving data integrity.

- **When you want to debug a problem**: In a disaster recovery situation, it's essential to understand the root problem that led to the need for recovery. Creating a new database allows you to examine the original database for vulnerabilities or issues before restoring the data. This can help identify weaknesses that need to be addressed.

- **When you want to validate backup data before restore**: By creating a new database, you can test the integrity and consistency of the backup data before making it the primary production data. This validation process ensures that the backup is clean and free from corruption, reducing the risk of propagating issues from the backup to the new database.

- **Before upgrading or patching**: In some cases, a disaster recovery event might coincide with the need to upgrade or patch the database software. Creating a new database allows you to apply the necessary upgrades or patches to the new environment, ensuring that the production environment is up-to-date and secure.

- **To create a safety net for rollbacks**: Restoring the backup directly to the original database leaves little room for rolling back the recovery process if issues are discovered later. Creating a new database provides a safety net, as you can decide whether to promote the new database to the production environment or keep the original one if necessary.

To create a new database from backup:
{.power-number}

1. In the <i class="uil uil-database"></i> **Databases** view, select the database you want to replicate.
2. Click the <i class="uil uil-ellipsis-h"></i> Actions menu next to the backup you want to replicate from, then click **Create new DB**.
3. Select **Create** to start database provisioning for the DB replica.
4. In the **Basic information** window, change the default backup name if required, then select one of the classes created by your Kubernetes administrator. 
Storage classes define what storage configuration and features will be used for storing your database data. Different classes map to different quality-of-service levels, backup policies, persistent volumes, or to arbitrary policies determined by your cluster administrator. For more information, see [Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/){:target="_blank"} in the Kubernetes documentation. 
5. On the **Resources** page, select the number of nodes and set the resources. For more information see, [Provision a database](../use/db_provision.md).
6. On the **Advanced Configurations** page, enable external access and database engine parameters by turning the toggle button on. For more information on configuring specific database parameters, see the [MySQL](https://dev.mysql.com/doc/refman/8.0/en/option-files.html){:target="_blank"}, [MongoDB](https://www.mongodb.com/docs/manual/reference/configuration-options){:target="_blank"}, and [PostgreSQL](https://www.postgresql.org/docs/current/config-setting.html#CONFIG-SETTING-CONFIGURATION-FILE){:target="_blank"} configuration documentation.
7. If you've enabled monitoring during CLI provisioning, this option will show as active on the **Monitoring** page and you can disable it if required.
8. Click **Create database**.


# Provision a database

Provisioning a database instance involves setting up and configuring a database instance on the Percona Everest platform.


!!! warning
    Refrain from changing the password of administrative users (e.g., root, monitor, or operator) manually in the database. This action may cause inconsistencies with the secrets stored in Kubernetes, which are crucial for the proper functioning of the cluster. Such modifications have the potential to disrupt your cluster.

    We are developing a new feature that will allow you to modify these settings directly from the user interface (UI).


## Procedure


To provision a new database:
{.power-number}

1. Log into the Percona Everest UI.

2. On the Percona Everest homepage, click **Create Database**. The menu for the different database types will open. Select the database that you wish to provision. The **Basic Information** page will then be displayed.

     ![!image](../images/everest_db_provision.png)

3. On the **Basic information** page, provide the following details:

       - Select the **Namespace** where you want to create your database.

       - Choose a name for your database. The name is auto-populated, but you can modify it according to your needs.

       - Select the **Database version** from the dropdown.

       - In the **Storage class** field, select one of the classes created by your Kubernetes administrator. 
       
        Storage classes define what storage configuration and features will be used for storing your database data. Different classes map to different quality-of-service levels, backup policies, persistent volumes, or to arbitrary policies determined by your cluster administrator. For more information, see [Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/){:target="_blank"} in the Kubernetes documentation. 


        ![!image](../images/everest_multi-namespaces.png)

4. Click **Continue**. The **Resources** page will be displayed.

5. On the **Resources** page, select the **Number of nodes**. Also, set **Resources size per node **by selecting one of the predefined presets or by specifying the CPU, Memory, and Disk. For more information on resources, see the [Scale database deployment](../use/scaling.md) section.

    Additionally, based on the database technology you’re working with, select the following:

    - MySQL: On the **Proxies** panel, select the **Number of proxies** and **Resource size per proxy**.

        !!! info
            Proxies are used primarily to ensure high availability, load balancing, and database failover management. They act as intermediaries, ensuring client requests are directed to the appropriate database instances.

        ![!image](../images/resources_proxies_page.png)

    - PostgreSQL: On the **PG Bouncers** panel, select the **Number of PG Bouncers** and **Resource size per PG Bouncer**.

        !!! info
            [PgBouncer](https://www.pgbouncer.org/) manages PostgreSQL connections, particularly in high traffic environments.

        ![!image](../images/resources_pgbouncer.png)

    - MongoDB: If you enable sharding, you can see the **Routers** panel on the **Resources** page. Select the **Number of routers** and the **Resource size per router**.

        ![!image](../images/resources_routers.png)

6. Click **Continue**. The **Scheduled Backups** page will be displayed.

7. On the **Scheduled Backups** page, set up a schedule to run backup jobs for your new database.

    Click **Create backup schedule**. The backup schedule pop-up is displayed.

    Provide the following details on this page:

      - Choose a name for your backup schedule. The name is auto-populated, but you can modify it according to your needs.
    
      - Select the **Backup storage** from the dropdown.
    
      - Enter the number of **Retention copies** for the backups.

        !!! note
            Currently, Retention copies are not supported for PostgreSQL databases.      
        
        Retention copies refer to the number of backup instances that should be kept.

        Example: When you set retention copies to 3, it means that you want to keep a maximum of 3 backup copies at any given time. So, if you have 3 backups already and then run a 4th backup, the oldest backup will get deleted automatically. 

         ![!image](../images/everest_scheduled_backups.png)    

7. On the **Scheduled Backups** page, you can also enable Point-in-time Recovery (PITR) by turning the toggle on.

8. Click **Continue**. The **Advanced Configurations** page will be displayed.

9. On the **Advanced Configurations** page, you can enable external access and customise database engine parameters by turning the toggle on. For in-depth information, see the [configure database engine](../use/db_engine_config.md) section.

10. Click **Continue**. The **Monitoring** page will be displayed.

11. On the **Monitoring** page, you can enable monitoring by turning the toggle on and selecting the **Monitoring endpoint** from the drop down.
 
    If you have not added any monitoring endpoint, click **Add monitoring endpoint**. For information on adding monitoring endpoints, see the [monitoring endpoints](../use/monitor_endpoints.md) section.

12. Click **Create Database**.

13. Click **Go to list of my databases** to see the database that you provisioned.


## Video tutorial

You can also learn about creating databases by checking the video tutorial below:

<iframe width="560" height="315" src="https://www.youtube.com/embed/Oq1XKB8VXUk?si=JBLVJ9zBfpHGxL2I" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

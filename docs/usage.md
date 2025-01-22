| [Home](../README.md) |
|--------------------------------------------|

# Usage

Following are the methods to use FortiSOAR Health Assessment
- Configure FortiSOAR Health Assessment Connector
- You can use below steps to generate record
    - **Usage 1**: Health Assessment
        - Navigate to Health Assessment.
        - Click on **Assess System Health**.
        - A Health Assessment Record will be generated. [Click here](#health-assessment) for more details.
    - **Usage 2**: Configuration Recommendation
        - Navigate to Health Assessment.
        - Click on **Recommend System Configuration**.
        - A Configuration Recommendation Record will be generated. [Click here](#configuration-recommendation) for more details.
- Once record is generated you can apply recommendation generated. [Click Here](#step-to-apply-generated-configuration-recommendations) for step to apply

# Health Assessment
How to read Health Assessment Record
- When you navigate to Health Assessment Record's details view. There will be following tabs
    - **Assessment** : Assessment Tab will contain following things:
        - ***System Resources*** : System resources such as vCPUs, RAM, IOPS, and Disk Latency are crucial for determining the overall performance of an application or system.
            - **vCPUs** represent the processing power allocated to a virtual machine, impacting the system's ability to handle concurrent tasks.
            - **RAM** is vital for holding active data and instructions, influencing how efficiently applications run.
            - **IOPS (Input/Output Operations Per Second)** measures the speed of disk read/write operations, essential for data-intensive tasks.
            - **Disk Latency** refers to the time delay in accessing data from storage, with lower latency improving responsiveness.
        - ***FortiSOAR Details*** :
            - *Alerts Trend : Number of Alerts Ingested* : This metric provides a comprehensive view of the volume of alerts being ingested into the system, helping to track trends and system load over time.
            - *Playbook : Most Frequently Executed* : Displays the top ten most executed playbooks, giving insight into which automated processes are most frequently used.
            - *Playbook : Most Failing* : Lists the top ten playbooks that fail most often, providing a focus area for troubleshooting and improvement.
            - *Playbook : Running In Debug Mode* : Identifies the top ten playbooks currently running in debug mode, typically for development or issue resolution purposes.
            - *Playbook : Most Time Consuming* : Shows the top ten playbooks consuming the most time, helping to identify performance bottlenecks or areas for optimization.
    - **Recommendation** : Recommendation Tab will contain following things
        - *PostgreSQL* : Adjust database settings for improved performance.
        - *PHP-FPM* : Adjust php-fpm settings to boost processing speed.
        - *Workflow Engine* : Fine-tune worker configurations for better task execution and to enhance request handling.
        - *RabbitMQ* : Streamline message queuing to improve communication between services.
        - *SWAP SPACE* : Ensure adequate swap space to maintain stability under heavy load.
# Configuration Recommendation
How to read Configuration Recommendation Record
- When you navigate to Configuration Recommendation Record's details view. There will be following tabs
    - **Assessment** : Assessment Tab will contain following things:
        - ***System Resources*** : System resources such as vCPUs, RAM, IOPS, and Disk Latency are crucial for determining the overall performance of an application or system.
            - **vCPUs** represent the processing power allocated to a virtual machine, impacting the system's ability to handle concurrent tasks.
            - **RAM** is vital for holding active data and instructions, influencing how efficiently applications run.
            - **IOPS (Input/Output Operations Per Second)** measures the speed of disk read/write operations, essential for data-intensive tasks.
            - **Disk Latency** refers to the time delay in accessing data from storage, with lower latency improving responsiveness.
    - **Recommendation** : Recommendation Tab will contain following things:
        - *PostgreSQL* : Adjust database settings for improved performance.
        - *PHP-FPM* : Adjust php-fpm settings to boost processing speed.
        - *Workflow Engine* : Fine-tune worker configurations for better task execution and to enhance request handling.
        - *RabbitMQ* : Streamline message queuing to improve communication between services.
        - *SWAP SPACE* : Ensure adequate swap space to maintain stability under heavy load.

# Step to Apply Generated Configuration Recommendations
Steps to incorporate the recommendations
1. Login to Terminal of Your VM via SSH
2. Following are the ways to implement above configuration either using cli command or by manually editing configuration file:
    - Method 1 :
        1. Run Following command to apply latest configuration recommended in Health Assessment record
            - Command : `sudo csadm system config --mode optimal`
    - Method 2 : 
        1. Edit the following files with mentioned changes
            - celeryd
                * File Location :`/etc/celery/celeryd.conf`
            - sealab_wsgi
                * File Location :`/etc/uwsgi.d/sealab_wsgi.ini`
            - integrations_wsgi
                * File Location : `/etc/uwsgi.d/integrations_wsgi.ini`
            - PHP-FPM
                *  File Location : `/etc/php-fpm.d/cyops-api.conf`
            - RabbitMQ
                * File Location : `/etc/rabbitmq/rabbitmq-env.conf`
            - PostgreSQL
                * Verify if the parameter is present in `/var/lib/pgsql/16/data/postgresql.auto.conf`. If it exists, edit this file. If not, proceed to edit `/var/lib/pgsql/16/data/postgresql.conf`
        2. Restart services using csadm commands: 
            - Command : `csadm services --restart`
3. Swap Space
    - Use the [documentation](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/managing_storage_devices/getting-started-with-swap_managing-storage-devices#creating-a-swap-file_getting-started-with-swap) for creating swap space


# Note 
* We recommend using the first method to update configuration changes.
* For HA setups apply the recommended configuration to all the system and then restart the services starting with primary
* If you have changed some parameters in the `/var/lib/pgsql/16/data/postgresql.conf` file and the same parameter is present in the `/var/lib/pgsql/16/data/postgresql.auto.conf` file, the parameter in `/var/lib/pgsql/16/data/postgresql.conf` will be overridden by the one in `/var/lib/pgsql/16/data/postgresql.auto.conf`. Therefore, we recommend using the first method to edit system resources.


# Know Issues
* If your system has the Global Playbook Logging Level set to **INFO** and individual playbook-level logging settings are disabled to override global settings, the solution pack will still count them as Debug if your playbook's logging level is set to **DEBUG**.


***

| [Installation](./setup.md#installation) | [Configuration](./setup.md#configuration) | [Contents](./contents.md) |
|-----------------------------------------|-------------------------------------------|---------------------------|

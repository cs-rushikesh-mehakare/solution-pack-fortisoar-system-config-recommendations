| [Home](../README.md) |
|--------------------------------------------|

# Usage

FortiSOAR Health Assessment can be used in following ways
- **Usage 1**: Health Assessment
    - Configure FortiSOAR Health Assessment Connector
    - Navigate to Health Assessment
    - Click on **Assess System Health**. 
    - A Health Assessment Record will be generated. [Click here](#health-assessment) for more details
- **Usage 2**: Configuration Recommendation
    - Configure FortiSOAR Health Assessment Connector
    - Navigate to Health Assessment
    - Click on **Recommend System Configuration**. A Configuration Recommendation Record will be generated. [Click here](#configuration-recommendation) for more details
- Once record is generated you can apply recommendation generated. [Click Here](#step-to-apply-generated-configuration-recommendations) for step to apply

# Health Assessment
How to read Health Assessment Record
- When you navigate to Health Assessment Record's details view. There will be following tabs
    - **Assessment** : Assessment Tab contains following details:
        - ***System Resources*** : System resources such as vCPUs, RAM, IOPS, and Disk Latency are crucial for determining the overall performance of an application or system.
            - **vCPUs**
            - **RAM** 
            - **IOPS (Input/Output Operations Per Second)** measures the speed of disk read/write operations, essential for data-intensive tasks.
            - **Disk Latency** refers to the time delay in accessing data from storage. Lower the latency greater the responsiveness.
        - ***FortiSOAR Information*** :
            - *Alerts Trend : Number of Alerts Ingested* : This metric provides a comprehensive view of the volume of alerts being ingested into the system, helping to track trends and system load over time.
            - *Playbooks : Most Frequently Executed* : Displays the top ten most executed playbooks, giving insight into which automated processes are frequently used.
            - *Playbooks : Most Failing* : Lists the top ten playbooks those fail often, providing a focus area for troubleshooting and improvement.
            - *Playbooks : Running In Debug Mode* : Identifies the top ten playbooks currently running in debug mode.
            - *Playbooks : Most Time Consuming* : Shows the top ten playbooks which take more time for completing the execution, helping to identify performance bottlenecks or areas for optimization.
    - **Recommendation** : Recommendation Tab contains following details:
        - *PostgreSQL* : Database settings for improved performance.
        - *PHP-FPM* :  PHP-FPM settings to boost processing speed.
        - *Workflow Engine* : Fine-tune worker configurations for better task execution and to enhance request handling.
        - *RabbitMQ* : Streamline message queuing to improve communication between services.
        - *SWAP SPACE* : Ensure adequate swap space to maintain stability under heavy load.
# Configuration Recommendation
How to read Configuration Recommendation Record
- When you navigate to Configuration Recommendation Record's details view. There will be following tabs
    - **Assessment** : Assessment Tab contains following details:
        - ***System Resources*** : System resources such as vCPUs, RAM, IOPS, and Disk Latency are crucial for determining the overall performance of an application or system.
            - **vCPUs** 
            - **RAM** 
            - **IOPS (Input/Output Operations Per Second)** measures the speed of disk read/write operations, essential for data-intensive tasks.
            - **Disk Latency** refers to the time delay in accessing data from storage. Lower the latency greater the responsiveness.
    - **Recommendation** : Recommendation Tab contains following details:
        - *PostgreSQL* : Database settings for improved performance.
        - *PHP-FPM* :  PHP-FPM settings to boost processing speed.
        - *Workflow Engine* : Fine-tune worker configurations for better task execution and to enhance request handling.
        - *RabbitMQ* : Streamline message queuing to improve communication between services.
        - *SWAP SPACE* : Ensure adequate swap space to maintain stability under heavy load.

# Step to Apply Recommended Configuration 
Steps to incorporate the recommendations
1. Connect SSH session to your VM
2. Recommended configuration can be applied using cli command or by manually editing configuration files:
    - CLI Way (Recommended):
        1. Run Following command to apply latest configuration recommended in Health Assessment record
            - Command : `sudo csadm system config --mode optimal`
    - Manual Way : 
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
* For HA setups apply the recommended configuration to all the systems. Restart the services on primary node first then secondary nodes.
* If you have updated some parameters in the `/var/lib/pgsql/16/data/postgresql.conf` file and the same parameter is present in the `/var/lib/pgsql/16/data/postgresql.auto.conf` file, the parameter in `/var/lib/pgsql/16/data/postgresql.conf` will be overridden by the one in `/var/lib/pgsql/16/data/postgresql.auto.conf`. Therefore, we recommend using the first method to edit system resources.


# Known Issues
* Irrespective of Global Playbook Logging level settings, playbooks with logging level is set to **Debug** will be counted as **Debug** .


***

| [Installation](./setup.md#installation) | [Configuration](./setup.md#configuration) | [Contents](./contents.md) |
|-----------------------------------------|-------------------------------------------|---------------------------|

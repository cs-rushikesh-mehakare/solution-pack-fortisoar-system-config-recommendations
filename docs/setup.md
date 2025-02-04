| [Home](../README.md) |
|----------------------|
# Installation

1. To install a solution pack, click **Content Hub** > **Discover**.   
2. From the list of solution pack that appears, search for and select **FortiSOAR Health Assessment**.    
3. Click the **FortiSOAR Health Assessment** solution pack card.   
4. Click the **Install** button on the bottom to begin the installation.
5. Once installed check [configuration](#configuration) for configuring the connector.


# Configuration

For optimal performance of the **FortiSOAR Health Assessment** solution pack, you must configure:

- FortiSOAR Health Assessment Connector
    - This connector is used to get required data from FortiSOAR&trade; system like playbook statistics, system resources, current configuration settings, etc to anazlise and suggest configuration changes. The connector uses following Authentication Method
        - Password Based : This method uses basic credential for authentication. Super User Password field is manditory and Fill the field with csadmin cli user's password. 
        - Certificate Based : This method uses certifcate for autentication. Fields involved :
            - SSH Key Password : Enter the password for the SSH private key, if the key is encrypted.
            - Private Key : Provide the private key for SSH authentication.
            
        Check FortiSOAR&trade; [documentation](https://docs.fortinet.com/document/fortisoar/7.6.1/deployment-guide/158469/deploying-fortisoar#Credentials) for more details.
    

> [!NOTE] 
> All data captured and processed by this solution pack is stored solely on the your system. No data is transmitted to or stored by the company.


| [Usage](./usage.md) | [Contents](./contents.md) |
|---------------------|---------------------------|

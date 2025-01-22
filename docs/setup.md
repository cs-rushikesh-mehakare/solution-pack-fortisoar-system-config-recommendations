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
    - This connector is used to get details from  FortiSOAR system. This connector uses following Authentication Method
        - Password Based : Use this method when you use password based authentication method. Fill the following field : 
            - Super User Password : Enter the csadmin user password
        - Certificate Based : Use this method when you use certificate based authentication. Fill the following fields :
            - SSH Key Password : Enter the password for the SSH private key, if the key is encrypted. This password is required to decrypt the key for authentication during the SSH connection.
            - Private Key : Provide the private key for SSH authentication.



| [Usage](./usage.md) | [Contents](./contents.md) |
|---------------------|---------------------------|

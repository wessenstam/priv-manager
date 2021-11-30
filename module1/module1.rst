.. _m1:

----------------------------
Installing Privilege Manager
----------------------------

Introduction
------------

This first module will cover:

1. What are the Secret Server components?
2. What are the pre-requirements (minimum and recommended)?
3. What ports does Secret Server use?
4. Lab exercises
5. Managing the Secret Server encryption key

Secret Server components
************************

- Front end ASP.NET web Application
- Back end SQL database

Pre-Requisites
**************
 
**Minimum Requirements - Basic Deployments**

.. list-table::
    :widths: 50 50
    :header-rows: 1

    * - Web Server
      - Database Server
    * - 2 CPU Cores
      - 2 CPU Cores
    * - 4 GB RAM
      - 4 GB RAM
    * - 25 GB Disk Space
      - 50 GB Disk Space
    * - Windows Server 2008 R2 SP1 or newer
      - Windows Server 2008 R2 SP1 or newer
    * - IIS 7 or newer
      - SQL Server 2012 or newer
    * - .NET 4.5.1. or newer
      - 

.. note::
    SQL Express is supported but not recommended for production environments

**Recommended Requirements - Basic Deployments**

.. list-table::
    :widths: 50 50
    :header-rows: 1

    * - Web Server
      - Database Server
    * - 4 CPU Cores
      - 4 CPU Cores
    * - 16 GB RAM
      - 16 GB RAM
    * - 25 GB Disk Space
      - 100+ GB Disk Space
    * - Windows Server 2008 R2 SP1 or newer
      - Windows Server 2008 R2 SP1 or newer
    * - IIS 7 or newer
      - SQL Server 2012 or newer
    * - .NET 4.6.1. or newer
      - 

.. warning::
    For advanced deployments where discovery, session recording or increased numbers of distributed engines are being used, please see feature specific knowledge base guides for detailed requirements.

Ports used by Secret Server
***************************
The table below identifies ports and/or port ranges that may be required by Secret Server

.. list-table:: Ports and/or port ranges used
    :widths: 40 30 30
    :header-rows: 1

    * - Process
      - Type of traffic
      - Port number/range
    * - Active Directory
      - LDAPS
      - 636
    * -
      - LDAP
      - 389
    * -
      - Kerberos
      - 88
    * -
      - NTLM
      - 445 
    * - Discovery
      - RPC Dynamic Port Range*
      - 49152 - 65535
    * - 
      - Microsoft DS
      - 445
    * - 
      - Epmap
      - 135
    * - 
      - SSH
      - 22
    * - Remote Password Changing
      - RPC Dynamic Port Range*
      - 49152 - 65535
    * - 
      - SSH
      - 22
    * - 
      - Telnet
      - 23
    * - 
      - MS SQL
      - 1433
    * - 
      - NTLM
      - 445
    * - 
      - LDAP
      - 389
    * - 
      - LDAPS
      - 636
    * - 
      - Sybase
      - 5000
    * - 
      - Oracle
      - 1521
    * - 
      - Kerberos
      - 88
    * - Ports Incoming to Webserver
      - HTTP
      - 80
    * - 
      - HTTPS
      - 443
    * - Ports Incoming to Database Server
      - SQL Connection TCP and UDP
      - 1433
    * - Email 
      - SMTP
      - 25
    * - RADIUS Server
      - RADIUS
      - 1812

* The RPC Dynamic Port ranges are a range of ports utilized by Microsoft’s Remote Procedure Call (RPC) functionality. This port range varies by operating system. For Windows Server 2008 or greater, this port range is 49152 to 65535 and this entire port range must be open for RPC technology to work. The RPC range is needed to perform Remote Password Changing since Secret Server will need to connect to the computer using DCOM protocol. To see your ipv4 dynamic range on a given machine, type netsh int ipv4 show dynamicport tcp in the commandline. To specify a specific port on your environment that Secret Server will communicate to, you can also `enable WMI ports on Windows client machines <https://thycotic.force.com/support/s/article/Enabling-WMI-ports-on-Windows-client-machines>`_.
    

Lab Exercise 1 – Connecting to the lab environment
**************************************************

In this exercise will access the Thycotic training lab environment.

#. Navigate to the URL of the training lab environment provided by the Thycotic training team.
#. Click the power on instances button, the virtual machines within the lab environment will now be powered on. They should be available in one to two minutes
#. Select and copy in the IP address of the win machine as in the image below:
   
   .. figure:: images/000002.png
   
.. note::
    this IP address is dynamic and will change every time the lab environment is stopped and restarted.
      
#. From the start menu on your host machine, type remote desktop connection and open the matching application
#. In the remote desktop connection dialogue, past the IP address and click connect

   .. figure:: images/000003.png

#. When prompted with the windows security credentials dialogue, select More Choices then Use a different account
#. Use the following credentials to connect, username: **thylab\\adm-training** / password: **Thycotic@2019!**
#. If prompted with the following certificate warning, select **don’t ask me again** and click **Yes**

   .. figure:: images/000004.png

#. A remote desktop connection should now be initialized into the Thycotic training lab environment. From this machine you can now remote on to the other windows machines within the lab environment.

Lab Exercise 2 – Installing Secret Server
*****************************************

In this exercise will power on and connect to the training lab environment before running through a complete installation of secret server.

#. In Lab exercise one we connected to the windows server that acts as a jump host. Initiate a remote desktop connection to **SECRETSERVER1** using the same credentials from lab 1 (thylab\administrator / Thycotic@2019!)
#. On the desktop of the secretserver1 machine you will see the secret server installer executable:

   .. figure:: images/000005.png

#. Run the setup file, when prompted with a windows User Account Control (UAC) dialogue click **Yes**
#. The installer can install both Secret Server and Privilege Manager (Thycotic endpoint least privilege solution). In this case we only want to install Secret Server so uncheck the Privilege Manager radio button as in the image below:

   .. figure:: images/000006.png

#. Click **Next**
#. Read and accept the license agreement
#. On the SQL Server Database screen we can either install SQL server express or connect to an existing database. In the lab environment SQL Express is already installed so select **Connect to an existing SQL server** then click **Next**

   .. figure:: images/000007.png

#. The installer will now perform a range of checks to ensure pre-requisites are in place. In the lab environment all requirements should be in place, click **Next**

   .. figure:: images/000008.png

#. On the next screen we need to configure the database connection. As the SQL server is installed on the same machine, in the Server name or IP field enter: **secretserver1\SQLEXPRESS** in the database name field, enter: **secretsserver**
#. On the same screen we now need to configure the authentication option that will be used to connect to the database. Although we can use SQL authentication or Windows authentication here, Thycotic recommend using Windows authentication. Select the **Windows Authentication using service account** radio button and click **Next**

   .. figure:: images/000009.png

#. On the next screen we will be asked to configure the service account that will be used to connect to the SQL database and used to run the IIS application pools. Enter the following credentials:

   - username: **thylab\\svc_secretserver**
   - password: **Thycotic@2019!**

#. To ensure the credentials are correct, click **Validate Credentials**, if they are you should see the word **success**. If not, check the credentials for any errors. Click Next
#. On the next screen we need to create our initial Secret Server user. At this point you can create your own user or use the following information to create the initial user:
   
   - Username: ss_admin
   - Display name: ss_admin
   - Email: ss_admin@thylab.com
   - Password: Thycotic@2019!
   - Confirm Password Thycotic@2019!

   .. note:: 
    If you create your own user account at this point, ensure you remember the username and password. This account is used for the initial administration of Secret Server.

#. Confirm you understand the importance of not loosing these credentials and click **Next**

   .. figure:: images/000010.png

#. On the next screen, options to configure an SMTP mail server are available. This feature will not be used during the training so click Skip Email
#. Click **Next**
#. The next screen provides a review of configured installation options and the option to modify any options if required. Click **Install**

   .. figure:: images/000011.png

Managing the Secret Server encryption key
******************************************

The Secret Server database is encrypted using a master encryption key. Each individual secret stored in the database is then encrypted with an intermediate key. When Secret Server is first installed the master encryption key is available in plain text and stored in the following location:

.. code-block:: bash

    C:\inetpub\wwwroot\SecretServer\encryption.conifg

In the next module we will be protecting this encryption config file as part of the security hardening of Secret Server. At this point, Thycotic recommend taking a copy of this master encryption key and storing it in a physical vault for disaster recovery purposes. In a worst case scenario it is possible to recover the Secret Server database and all secrets with a valid database backup and the master encryption key. 

.. danger:: 
    Thycotic does not keep copies of customer encryption keys

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#80BB01">This concludes this module</font>
    </CENTER>

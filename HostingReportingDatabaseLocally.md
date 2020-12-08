# OneConsultation Reporting: Locally hosted database

## Introduction 
By default, usage and quality reports are hosted by Modality Systems and accessible to you via PowerBI. Data is securely stored in Microsoft Azure, using sharded databases to ensure data separation. Any personally identifiable data is removed after 90 days, and data is archived to cold store after 120 days. Archived data is not available in PowerBI reports to ensure report performance, but can be accessed on demand via our Support Team.
However, customers may wish to host this reporting data themselves. This document provides the steps for achieving this. 

> :warning: **Important**: Before beginning this process please speak your OneConsultation Account Manager as configuration changes will need to be applied to your account and sequenced with the changes described below, in order to prevent potential data loss.

## Step 1: Provision a SQL Database

Data is stored in a Microsoft SQL Server Database. We recommend using Microsoft Azure to provision the database. The size of the database will be dependant on the number of consultations performed, and the amount of reporting expected. A minimum of **Standard S4: 200 DTUs** is recommended.

In the __Firewalls and virtual networks__ section of the Server configuration, set *Allow Azure services and resources to access this server* to "yes".

If this is not done (or a non-Azure SQL Server is used), ensure that SQL Server connections can be made from the following list of IP addresses:

````
191.235.217.28,191.235.220.16,191.235.220.26,191.235.209.127,40.112.91.53,40.112.94.248,40.112.94.169,40.112.92.166,40.127.169.249,40.115.109.115,40.85.74.6,40.87.140.166,40.69.21.110,13.74.47.143,13.74.44.233,13.79.242.180,13.79.240.200,191.235.208.12,13.69.228.17
````

## Step 2: Create Database

Your OneConsultation Account Manager will send you the latest [BACPAC file](https://docs.microsoft.com/en-us/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-ver15#bacpac) for your database.

#### If you are using Microsoft Azure SQL Server:

Save the BACPAC file to an Azure Storage Container. Follow the instructions in [Import a BACPAC file to a database in Azure SQL Database or Azure SQL Managed Instance](https://docs.microsoft.com/en-us/azure/azure-sql/database/database-import?tabs=azure-powershell) to create the database from the BACPAC file.

#### If you are using another hosting platform:

Follow your provider's instructions for creating and hydrating databases from BACPAC files.

---

Securely share the connection details with your OneConsultation Account Manager, being sure to include:  

1. Server address
1. Database name
1. User name
1. Password

We will then adjust your configuration so that new consultation data is set to this database. This can either be done instead of, or as well as, data being sent to the hosted database.

## Step 3: Download and Configure PowerBI Desktop

Your OneConsultation Account Manager will provide you with the OneConsultation Reporting Power BI template file. Using [PowerBI Desktop](https://powerbi.microsoft.com/en-us/desktop/), open the file and provide the server name and database when prompted.

Supply valid connection credentials when prompted.

At this point you can either view reports in PowerBI Desktop, or Publish to your tenant's PowerBI Workspace. For more information, see [Publish datasets and reports from Power BI Desktop](https://docs.microsoft.com/en-us/power-bi/create-reports/desktop-upload-desktop-files)

## Step 4: Stay up to date

Periodically, changes will be made to OneConsultation reports. This will result in new PowerBI template files being sent to you. You should repeat Step 2 for each newly received file.

Occasionally, breaking changes to how data is collected and store may result in changes needing to be made to the database structure, and am upgrade script will be released, together with instructions on how to upgrade. You should follow these instructions, otherwise newer PowerBI template files may not be compatible with your database, and data loss may occur.

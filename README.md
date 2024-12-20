test
1. Resource Group
Resource Group Name: cms

2. SQL Database
DB name: cms
Server: cms59.database.windows.net (needs to be unique)
DB region: south central us
Admin login: cmsadmin
Admin password: CMS4dmin
Resource group: cms
DB workload env: Development
DB compute + storage: DTU - Basic
Press the "Next: Networking" button, then select "Public Endpoint", and set both of the Firewall rules that appear to "Yes".
Set everything else to default
Run SQL queries in sql_scripts/ directory after completion, starting from the users table. Don't forget to take screenshots.

3. Storage Account
Basics
Resource group: cms
Storage account name: images58 (needs to be unique)
Region: Canada Central (same as app)
Primary service: Azure files

Advanced - Allow enabling anonymous access on individual containers: Enable
Advanced - Access tier: Cool
Network access: Enable public access from all networks (the default)

3a. Create container named "images". Set its access level to Container.
After creation
From Security + networking > Access keys:
Blob Storage key: hsWTxqn7CTk/7v5Tax1zI29nsr9aU6lRaP9WbJWBNHXZxQxjn9/4TCKoe68b8VatvKJUhVPKyJVq+AStv231kQ==
Blob connection string: hsWTxqn7CTk/7v5Tax1zI29nsr9aU6lRaP9WbJWBNHXZxQxjn9/4TCKoe68b8VatvKJUhVPKyJVq+AStv231kQ==


4. Microsoft Entra ID
4.1. App Registration
Name: cmsEntraID
Who can use? "Accounts in any organizational directory (Any Microsoft Entra ID tenant - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)"
4.2. Secret Creation
Secret description: cmsSecret
Secret Key (Secret ID): e041bc9c-bf68-42cc-b820-679fde57708c
Client Secret (Value): 84F8Q~ev5qZXbFLGpAmL3PDa4blQJjBX.yPGcbhB
Application (client) ID: 7319366a-9e05-45a2-98a9-d66524a2e7ee

5. Web App (easier)
Name: udacitycms2.azurewebsites.net
Runtime stack: Python 3.10
Pricing Plan: Free F1
Region: Canada Central
If you are getting a "Validation failed for a resource" error, pick a different region.

After creation:
Settings -> Environment variables - Add the following variables (sample values are included, replace them with your values):
BLOB_ACCOUNT: images58
BLOB_CONTAINER: images2
BLOB_STORAGE_KEY: hsWTxqn7CTk/7v5Tax1zI29nsr9aU6lRaP9WbJWBNHXZxQxjn9/4TCKoe68b8VatvKJUhVPKyJVq+AStv231kQ==
BLOB_CONNECTION_STRING: hsWTxqn7CTk/7v5Tax1zI29nsr9aU6lRaP9WbJWBNHXZxQxjn9/4TCKoe68b8VatvKJUhVPKyJVq+AStv231kQ==
SQL_SERVER: cms59.database.windows.net
SQL_DATABASE: cms
SQL_USER_NAME: cmsadmin
SQL_PASSWORD: CMS4dmin
CLIENT_SECRET: 84F8Q~ev5qZXbFLGpAmL3PDa4blQJjBX.yPGcbhB
SECRET_KEY: e041bc9c-bf68-42cc-b820-679fde57708c
CLIENT_ID: 4cec6730-afad-4714-b5bb-9b2c6666eaba
Deployment Center
Source: GitHub
Pick the repo that contains the starter files.
6. Setting up OAuth2
At this point, your application should already be running. You should already be able to log in with username admin and password pass and you can create new posts or update existing ones.

The next part is getting the OAuth2 login to work.

Go to Microsoft Entra ID > App Registrations, click on the App Registration created earlier, and then pick Authentication from the left sidebar.

6.1. Microsoft Entra ID - Authentication - Add a Platform - Web
Redirect URIs: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/getAToken
logout URL: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/login
# Monitoring Office365 using Dynatrace Synthetic

### Step 1: Create an App Registration on Azure

Register a new application on [Azure](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).
You need to configure a couple of permissions. Delegated permissions won't do it - you need to configure Application Permissions. It's also a requirement in order to access the required APIs without logging into Azure as a registered user.

![Permissions](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/permissions.png)

### Step 2: Download the Postman Collection
Download the [Postman Collection](https://raw.githubusercontent.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/main/Office365.postman_collection.json) from this repository and import it into your local Postman installation.

### Step 3: Configure environment variables
The Postman Collection you just imported requires a couple of global environment variables.
![Environment Variables](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/environment.png)

* The `ENVIRONMENT_URL` represents the URL your environment is reachable via WebUI.
* The `API_TOKEN` needs to get configured within Dynatrace. It requires the permission to manage API Tokens.
* ![API Token](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/token.png)
* The `AZURE_CLIENT_ID` and the `AZURE_TENANT` are available for you to look up with in the Azure Portal where you've configured the Application Registration
* ![TenantID and ClientID](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/client_tenant_id.png)
* In a different section you'll also find the `OFFICE365_CLIENT_SECRET`
* ![Client Secret](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/client_secret.png)

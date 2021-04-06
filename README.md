# Monitoring Office365 using Dynatrace Synthetic
This Postman Collection automates the creation of Synthetic Monitors within Dynatrace if you'd like to monitor Office 365 without having to install a dedicated Plugin or Extension. All you need to have installed is Postman on your workstation. Any credentials will be securely stored within the Credentials Vault of your Dynatrace Environment.

This solution also creates a preconfigured Dashboard in your environment. But needless to say it's your choice whether you'd like to visualize the metrics gathered by the Synthetic Monitors in a different way.

![Dashboard](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/dashboard.png)

### Step 1: Create an App Registration on Azure

Register a new application on [Azure](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).
You need to configure a couple of permissions. Delegated permissions won't do it - you need to configure Application Permissions. It's also a requirement in order to access the required APIs without logging into Azure as a registered user.

![Permissions](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/permissions.png)

### Step 2: Download the Postman Collection
Download the [Postman Collection](https://raw.githubusercontent.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/main/Office365.postman_collection.json) from this repository and import it into your local Postman installation.

### Step 3: Configure environment variables
The Postman Collection you just imported requires a couple of global environment variables.
![Environment Variables](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/environment.png)

The `ENVIRONMENT_URL` represents the URL your environment is reachable via WebUI.

The `API_TOKEN` needs to get configured within Dynatrace. It requires the permission to manage API Tokens.

![API Token](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/token.png)

The `AZURE_CLIENT_ID` and the `AZURE_TENANT` are available for you to look up with in the Azure Portal where you've configured the Application Registration.

![TenantID and ClientID](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/client_tenant_id.png)

In a different section you'll also find the `OFFICE365_CLIENT_SECRET`.

![Client Secret](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/client_secret.png)

### Step 4: Execute the Postman Collection
Double click on the Office365 Collection in Postman. Don't forget to choose the Environment that holds the previously configured environment variables.

![Runner](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/runner.png)

Once you click on the `Run` button, the requests stored within this collection will preconfigure everything within your Dynatrace environment.

![Runner](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/runner-2.png)

### Step 5: Validate the configuration
You'll notice that your environment now contains 3 additional synthetic monitors.

![Monitors](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/monitors.png)

* `[Office365] Token Refresh` will get executed about every 45 minutes. Its purpose is to ensure that the Access Token for accessing the Microsoft Graph API and Office365 Management API is always up to date and doesn't expire.
* `[Office365] portal.office.com` periodically tests connectivity to the Office365 servers. Feel free to reduce the frequency to something lower than a minute. Just be aware that this also lowers the resolution of the metrics gathered for Dynatrace.
* `[Office365] Reports` finally queries the Microsoft Graph API and the Office 365 Management API for various metrics. Feel free to reduce the frequency to something lower than a minute. Just be aware that this also lowers the resolution of the metrics gathered for Dynatrace. If you take a detailed look at this synthetic monitor you'll realize that the final request addresses the Metrics Ingest REST API of your Dynatrace Environment.

### You have arrived!
![Dashboard](https://github.com/Dynatrace-Reinhard-Pilz/office-365-synthetic-monitoring/raw/main/docs/dashboard.png)

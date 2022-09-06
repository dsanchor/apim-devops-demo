# Configure Github environment

## Create credential secrets

 1. Create SP

 az account list -o table

 SUBS_ID=<YOUR_SUBS_ID>

 NOTE: see if the following two SP can be unified in one

 For Github actions:

 az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/$SUBS_ID" --sdk-auth

{
  "clientId": "xxxxxx-xxx-xxxx-xxxx-xxxxxxxxxx",
  "clientSecret": "xxxxxx-xxx-xxxx-xxxx-xxxxxxxxxx",
  "subscriptionId": "xxxxxx-xxx-xxxx-xxxx-xxxxxxxxxx",
  "tenantId": "7xxxxxx-xxx-xxxx-xxxx-xxxxxxxxxx",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}

For TF:

 az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/$SUBS_ID"

 {
  "appId": "xxxxxx-xxx-xxxx-xxxx-xxxxxxxxxx",
  "displayName": "azure-cli-2022-xxxx",
  "password": "xxxxxx~xxxxxx~xxxxx",
  "tenant": "xxxxx-xxxx-xxxxx-xxxx-xxxxx"
}

 2. Github/settings/secrets/actions

    New credentials:

        TF_ARM_CLIENT_ID=<appId>
        TF_ARM_CLIENT_SECRET=<password>
        TENANT_ID=<tenant>
        SUBSCRIPTION_ID=$SUBS_ID

        AZURE_CREDENTIALS=<JSON_SP_FOR_GITHUB>

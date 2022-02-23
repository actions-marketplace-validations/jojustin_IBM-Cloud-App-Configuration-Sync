# IBM Cloud App Configuration Sync

This action syncs configuration files in the repository to an IBM Cloud App Configuration instance.  This action automatically updates an IBM Cloud App Configuration instance when the changes are made through the GitHub workflows.

.json files are supported as configuration files.  You can IBM Cloud App Configuration CLI to export the configuration from an existing instance.  Refer https://cloud.ibm.com/docs/app-configuration?topic=app-configuration-cli-plugin-app-configuration-cli#ac-ibmcloud-ac-export for details.

To start using this GitHub action, go to your repository and click the "Actions" tab. This GitHub action will be available from the marketplace under the name "IBM Cloud App Configuration Sync". 


## Secrets 

IBM Cloud API Key & App Configuration Instance GUID should be stored as [secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) in the names IBM_CLOUD_API_KEY & IBM_CLOUD_AC_INSTANCE_ID respectively

## Usage example

The following example updates the App Configuration instance when pull requests are merged with changes to appconfig.json.


```
# File: .github/workflows/appconfigsync.yml

on:
  push:
    branches:
      - 'master'

jobs:
  icappconfigsync:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - uses: jojustin/ic-appconfiguration-sync@v1
        env:
          IBM_CLOUD_API_KEY: ${{ secrets.IBM_CLOUD_API_KEY }}
          IBM_CLOUD_REGION: us-south
          IBM_CLOUD_RESOURCE_GROUP: default
          AC_INSTANCE_ID: ${{ secrets.IBM_CLOUD_AC_INSTANCE_ID }}
          CONFIG_FILE_NAME: appconfig.json
```


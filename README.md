# SharePointBackup
Simple Azure serverless SharePoint backup using a logic app and storage account. It will only backup the Shared Documents part of your site.

# Installation

Blal

# Configuration

To add a site to the backup process you need to add it to the Azure storage table that you created in the previous step. First you need the siteid of you SharePoint site. You can easily retrieve the siteid by navigating to your site and appending '/_api/site/id' to the url.

<img src="https://github.com/Robert1976/SharePointBackup/blob/master/images/getsiteid.PNG" width="900" >

Then you need the webid of your SharePoint site. You can retrieve the webid by navigating to your site and appending '/_api/web/id' to the url.

Now use storage explorer (you can download storage explorer from https://azure.microsoft.com/nl-nl/features/storage-explorer/) to add a new row to your storage table. This row will contain the data that the logic app will need to backup your SharePoint files.

PartitionKey: Anything you like, in the example I choose 'Sites'

RowKey: [tenantname].sharepoint.com,[siteid],[webid] (for example: qoders.sharepoint.com,2ad13d96-af88-4aa1-9fd1-c92ca098498c,a4995daa-ce03-4a20-a317-9a21525c894d)

DeltaLink: https://graph.microsoft.com/v1.0/sites/[tenantname].sharepoint.com,[siteid],[webid]/drive/root/delta (for example: https://graph.microsoft.com/v1.0/sites/qoders.sharepoint.com,2ad13d96-af88-4aa1-9fd1-c92ca098498c,a4995daa-ce03-4a20-a317-9a21525c894d/drive/root/delta)


<img src="https://github.com/Robert1976/SharePointBackup/blob/master/images/storageexplorer.PNG" width="400" >

That's it! Your DeltaLink will be updated after each run of the logic app so that it will only pick up changes and new documents that have happened after the last run.

# Extra


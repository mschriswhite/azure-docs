---
title: Get started with Storage Explorer (Preview) | Microsoft Docs
description: Manage Azure storage resources with Storage Explorer (Preview)
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: ''

ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: cawa

---
# Get started with Storage Explorer (Preview)
## Overview
Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux. In this article, you learn several ways of connecting to and managing your Azure storage accounts.

![Microsoft Azure Storage Explorer (Preview)][0]

## Prerequisites
* [Download and install Storage Explorer (Preview)](http://www.storageexplorer.com)

## Connect to a storage account or service
Storage Explorer (Preview) provides several ways to connect to storage accounts. For example, you can:
* Connect to storage accounts associated with your Azure subscriptions.
* Connect to storage accounts and services that are shared from other Azure subscriptions.
* Connect to and manage local storage by using the Azure Storage Emulator. 

In addition, you can work with storage accounts in global and national Azure:

* [Connect to an Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong to your Azure subscription.
* [Work with local development storage](#work-with-local-development-storage): Manage local storage by using the Azure Storage Emulator.
* [Attach to external storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong to another Azure subscription or that are under national Azure clouds by using the storage account's name, key, and endpoints.
* [Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong to another Azure subscription by using a shared access signature (SAS).
* [Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs to another Azure subscription by using an SAS.
* [Connect to an Azure Cosmos DB account by using a connection string](#connect-to-an-azure-cosmos-db-account-by-using-a-connection-string): Manage Cosmos DB account by using a connection string.

## Connect to an Azure subscription
> [!NOTE]
> If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. In Storage Explorer (Preview), select **Manage Accounts** to go to the **Account Management Panel**.

    ![Manage Accounts][1]

2. The left pane now displays all the Azure accounts you've signed in to. To connect to another account, select **Add an account**

3. If you want to sign into a national cloud or an Azure Stack, click on the **Azure environment** dropdown to select which Azure cloud you want to use. Once you have chosen your environment, click the **Sign in...** button. If you are signing in to Azure Stack, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack/user/azure-stack-storage-connect-se.md) for more information.

    ![Sign In Option][2]

3. After you successfully sign in with an Azure account, the account and the Azure subscriptions associated with that account are added to the left pane. Select the Azure subscriptions that you want to work with, and then select **Apply** (Selecting **All subscriptions:** toggles selecting all or none of the listed Azure subscriptions).

    ![Select Azure subscriptions][3]

    The left pane displays the storage accounts associated with the selected Azure subscriptions.

    ![Selected Azure subscriptions][4]

## Work with local development storage
With Storage Explorer (Preview), you can work against local storage by using the Azure Storage Emulator. This approach lets you simulate working with Azure Storage without necessarily having a storage account deployed on Azure, because the storage account is being emulated by the Azure Storage Emulator.

> [!NOTE]
> The Azure Storage Emulator is currently supported only for Windows.
>
>

> [!NOTE]
> The Azure Storage Emulator does not support File Shares.
>
>

1. In the left pane of Storage Explorer (Preview), expand the **(Local and Attached)** > **Storage Accounts** > **(Development)** > **Blob Containers** node.

    ![Local development node][5]

2. If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an info bar. If the infobar is displayed, select **Download the latest version**, and then install the emulator.

    ![Download Azure Storage Emulator prompt][6]

3. After the emulator is installed, you can create and work with local blobs, queues, and tables. To learn how to work with each storage account type, refer to the following guides:

    * [Manage Azure blob storage resources](vs-azure-tools-storage-explorer-blobs.md)
    * Manage Azure file share storage resources: *Coming soon*
    * Manage Azure queue storage resources: *Coming soon*
    * Manage Azure table storage resources: *Coming soon*

## Attach or detach an external storage account
With Storage Explorer (Preview), you can attach to external storage accounts so that storage accounts can be easily shared. This section explains how to attach to (and detach from) external storage accounts.

### Get the storage account credentials
To share an external storage account, the owner of that account must first get the credentials (account name and key) for the account and then share that information with the person who wants to attach to said account. You can obtain the storage account credentials via the Azure portal by doing the following steps:

1. Sign in to the [Azure portal](https://portal.azure.com).

2. Select **Browse**.

3. Select **Storage Accounts**.

4. In the list of **Storage Accounts**, select the desired storage account.

5. Under **Settings**, select **Access keys**.

    ![Access Keys option][7]

6. Copy the **Storage account name** and **key1**.

    ![Access keys][8]

### Attach to an external storage account
To attach to an external storage account, you need the account's name and key. The "Get the storage account credentials" section explains how to obtain these values from the Azure portal. However, in the portal, the account key is called **key1**. So, when Storage Explorer (Preview) asks for an account key, you enter the **key1** value.

1. In Storage Explorer (Preview), open the **Connect Dialog**.

    ![Connect to Azure storage option][9]

2. In the **Connect Dialog**, choose **Use a storage account name and key**

    ![Add with name and key option][10]

3. Paste your account name in the **Account name** text box, and paste your account key (the **key1** value from the Azure portal) into the **Account key** text box, and then select **Next**.

    ![Name and key page][11]

    > [!NOTE]
    > To use a name and key from a national cloud, use the **Storage endpoints domain:** dropdown to select the appropriate endpoints domain: 
    >
    >

4. In the **Connection Summary** dialog box, verify the information. If you want to change anything, select **Back** and reenter the desired settings. 

5. Select **Connect**.

6. After the storage account has successfully been attached, the storage account is displayed with **(External)** appended to its name.

    ![Result of connecting to an external storage account][12]

### Detach from an external storage account
1. Right-click the external storage account that you want to detach, and then select **Detach**.

    ![Detach from storage option][13]

2. In the confirmation message, select **Yes** to confirm the detachment from the external storage account.

## Attach a storage account by using a Shared Access Signature (SAS)
A Shared Access Signature, or [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md), lets the admin of an Azure subscription grant temporary access to a storage account without having to provide Azure subscription credentials.

To illustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:

1. UserA generates a SAS connection string for a specific time period and with the desired permissions.

2. UserA shares the SAS with the person (UserB, in this example) who wants access to the storage account.  

3. UserB uses Storage Explorer (Preview) to attach to the account that belongs to UserA by using the supplied SAS.

### Generate a SAS connection string for the account you want to share
1. In Storage Explorer (Preview), right-click the storage account you want share, and then select **Get Shared Access Signature...**.

    ![Get SAS context menu option][14]

2. In the **Generate Shared Access Signature** dialog box, specify the time frame and permissions that you want for the account, and then click the **Create** button.

    ![Get SAS dialog box][15]  

3. Next to the **Connection String** text box, select **Copy** to copy it to your clipboard, and then click **Close**.

### Attach to a storage account by using a SAS Connection String
1. In Storage Explorer (Preview), open the **Connect Dialog**.

    ![Connect to Azure storage option][9]

2. In the **Connect Dialog** dialog, choose **Use a connection string or shared access signature URI** and then click **Next**.

    ![Connect to Azure storage dialog box][16]

3. Choose **Use a connection string** and paste your connection string into the **Connection string:** field. Click the **Next** button.

    ![Connect to Azure storage dialog box][17]

4. In the **Connection Summary** dialog box, verify the information. To make changes, select **Back**, and then enter the settings you want. 

5. Select **Connect**.

6. After the storage account has successfully been attached, the storage account is displayed with **(SAS)** appended to its name.

    ![Result of attached to an account by using SAS][18]

## Attach a service by using a Shared Access Signature (SAS)
The "Attach a storage account by using a SAS" section explains how an Azure subscription admin can grant temporary access to a storage account by generating and sharing a SAS for the storage account. Similarly, a SAS can be generated for a specific service (blob container, queue, table, or file share) within a storage account.  

### Generate an SAS for the service that you want to share
In this context, a service can be a blob container, queue, table, or file share. To generate the SAS for a listed service, see:

* [Get the SAS for a blob container](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Get the SAS for a file share: *Coming soon*
* Get the SAS for a queue: *Coming soon*
* Get the SAS for a table: *Coming soon*

### Attach to the shared account service by using a SAS URI
1. In Storage Explorer (Preview), open the **Connect Dialog**.

    ![Connect to Azure storage option][9]

2. In the **Connect Dialog** dialog box, choose **Use a connection string or shared access signature URI** and then click **Next**.

    ![Connect to Azure storage dialog box][16]

3. Choose **Use a SAS URI** and paste your URI into the **URI:** field. Click the **Next** button.

    ![Connect to Azure storage dialog box][19]

3. In the **Connection Summary** dialog box, verify the information. To make changes, select **Back**, and then enter the settings you want. 

4. Select **Connect**.

5. After the service is successfully attached, the service is displayed under the **(SAS-Attached Services)** node.

    ![Result of attaching to a shared service by using an SAS][20]

## Connect to an Azure Cosmos DB account by using a connection string
Besides manage Azure Cosmos DB accounts through Azure subscription, an alternative way of connecting to an Azure Cosmos DB is to use a connection string. Use the following steps to connect using a connection string.

1. Find **Local and Attached** in the left tree, right-click **Azure Cosmos DB Accounts**, choose **Connect to Azure Cosmos DB...**

    ![connect to Azure Cosmos DB by connection string][21]

2. Choose Azure Cosmos DB API, paste your **Connection String**, and then click **OK** to connect Azure Cosmos DB account. For information on retrieving the connection string, see [Get the connection string](https://docs.microsoft.com/azure/cosmos-db/manage-account#get-the--connection-string).

    ![connection-string][22]

 ## Connect to Azure Data Lake Store by URI
If you want to get access to the resources, which do not exist in your subscription. But others grant you to get the Uri for the resources. In this case, you can connect to Data Lake Store using the Uri after you have signed in. Refer to following steps.
1. Open Storage Explorer (Preview).
2. In the left pane, expand **Local and Attached**.
3. Right-click **Data Lake Store**, and - from the context menu - select **Connect to Data Lake Store...**.

    ![connect to Data Lake Store context menu](./media/vs-azure-tools-storage-manage-with-storage-explorer/storageexplorer-adls-uri-attach.png)

4. Enter the Uri, then the tool navigates to the location of the URL you just entered.

    ![connect to Data Lake Store context dialog](./media/vs-azure-tools-storage-manage-with-storage-explorer/storageexplorer-adls-uri-attach-dialog.png)

    ![connect to Data Lake Store result](./media/vs-azure-tools-storage-manage-with-storage-explorer/storageexplorer-adls-attach-finish.png)

## Search for storage accounts
If you need to find a storage resource and do not know where it is, you can use the search box at the top of the left pane to search for the resource.

As you type in the search box, the left pane displays all resources that match the search value you've entered up to that point. For example, a search for **endpoints** is shown in the following screenshot:

![Storage account search][23]

> [!NOTE]
> Use the **Account Management Panel** to deselect any subscriptions that do not contain the item you are searching for to improve the execution time of your search. You can also right-click on a node and choose **Search From Here** to start searching from a specific node.
>
>

## Next steps
* [Manage Azure Blob Storage resources with Storage Explorer (Preview)](vs-azure-tools-storage-explorer-blobs.md)
* [Manage Azure Cosmos DB in Azure Storage Explorer  (Preview)](./cosmos-db/storage-explorer.md)
* [Manage Azure Data Lake Store resources with Storage Explorer (preview)](./data-lake-store/data-lake-store-in-storage-explorer.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/Overview.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/ManageAccounts.png
[2]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/ConnectDialog-SignInSelected.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/AccountPanel.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/SubscriptionNode.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/DevelopmentNode.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/EmulatorNotInstalled.png
[7]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/PortalAccessKeys.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/AccessKeys.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/ConnectDialog.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/ConnectDialog-AddWithKeySelected.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/ConnectDialog-NameAndKeyPage.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/AttachedWithKeyAccount.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/AttachedWithKeyAccount-Detach.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/GetSharedAccessSignature.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/SharedAccessSignatureDialog.png
[16]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/ConnectDialog-WithConnStringOrSASSelected.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/ConnectDialog-ConnStringOrSASPage-1.png
[18]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/AttachedWithSASAccount.png
[19]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/ConnectDialog-ConnStringOrSASPage-2.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/ServiceAttachedWithSAS.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-db-by-connection-string.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connection-string.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/Search.png

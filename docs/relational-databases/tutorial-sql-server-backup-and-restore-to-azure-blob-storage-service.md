---
title: 教學課程：SQL Server 備份及還原至 Windows Azure Blob 儲存體服務 | Microsoft 文件
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a33c2bd47bae8bede7fa71e1654627c123e7cdbc
ms.sourcegitcommit: 8dccf20d48e8db8fe136c4de6b0a0b408191586b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2018
ms.locfileid: "48874316"
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>教學課程：SQL Server 備份及還原至 Azure Blob 儲存體服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
本教學課程可協助您了解如何將備份寫入 Azure Blob 儲存體服務以及從中還原。  本教學課程說明如何建立 Azure Blob 容器、建立認證以存取儲存體帳戶、將備份寫入 Blob 服務，然後執行簡單還原。
  
### <a name="prerequisites"></a>Prerequisites  
若要完成本教學課程，您必須熟悉 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份與還原概念以及 T-SQL 語法。 若要使用本教學課程，您需要 Azure 儲存體帳戶、SQL Server Management Studio (SSMS)、執行 SQL Server 伺服器的存取權，以及 AdventureWorks 資料庫。 此外，用來發出 BACKUP 或 RESTORE 命令的帳戶，應該位於擁有 **ALTER ANY CREDENTIAL** 權限的 **db_backupoperator** 資料庫角色中。 

- 取得免費 [Azure 帳戶](https://azure.microsoft.com/offers/ms-azr-0044p/)。
- 建立 [Azure 儲存體帳戶](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal)。
- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks2016 範例資料庫](https://docs.microsoft.com/sql/samples/adventureworks-install-configure) \(英文\)。
- 將使用者帳戶指派給 [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) 的角色，並授與 [ALTER ANY CREDENTIAL](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql) 權限。 


## <a name="create-azure-blob-container"></a>建立 Azure Blob 容器
容器會提供一組 Blob 的群組。 所有 Blob 都必須位於容器中。 帳戶可以包含不限數目的容器，但是至少必須具有一個容器。 容器可以儲存不限數目的 Blob。 

若要建立容器，請遵循下列步驟：

1. 開啟 Azure 入口網站。 
1. 巡覽至您的儲存體帳戶。 
   1. 選取儲存體帳戶，向下捲動至 [Blob 服務]。
   1. 選取 [Blob]，然後選取 [+容器] 以新增新的容器。 
   1. 輸入容器名稱，並記下您指定的容器名稱。 這項資訊會用於本教學課程稍後的 T-SQL 陳述式 URL (備份檔的路徑) 中。 
   1. 選取 [確定]。 
    
    ![新增容器](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/new-container.png)


  >[!NOTE]
  >即使您選擇建立公用容器，SQL Server 備份與還原仍然需要儲存體帳戶的驗證。 您也可以使用 REST API，以程式設計方式建立容器。 如需詳細資訊，請參閱[建立容器](https://docs.microsoft.com/rest/api/storageservices/Create-Container)


## <a name="create-a-sql-server-credential"></a>建立 SQL Server 認證
SQL Server 認證是用來儲存連接到 SQL Server 外部資源所需之驗證資訊的物件。 此處，SQL Server 備份和還原程序會使用認證，向 Windows Azure Blob 儲存體服務驗證。 認證會儲存儲存體帳戶的名稱以及儲存體帳戶的 **存取金鑰** 值。 一旦建立認證之後，您必須在發出 BACKUP/RESTORE 陳述式時，在 WITH CREDENTIAL 選項中指定認證。 如需認證的詳細資訊，請參閱[認證](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/credentials-database-engine)。 

  >[!IMPORTANT]
  >以下所述建立 SQL Server 認證的需求是特別針對 SQL Server 備份程序 ([SQL Server 備份至 URL](backup-restore/sql-server-backup-to-url.md) 及 [SQL Server Managed Backup to Microsoft Azure](backup-restore/sql-server-managed-backup-to-microsoft-azure.md)) 的需求。 在存取 Azure 儲存體以寫入或讀取備份時，SQL Server 會使用儲存體帳戶名稱與存取金鑰資訊。

### <a name="access-keys"></a>存取金鑰
在 Azure 入口網站仍為開啟狀態時，請儲存建立認證所需的存取金鑰。 

1. 巡覽至 Azure 入口網站的 [儲存體帳戶]。 
1. 向下捲動至 [設定]，然後選取 [存取金鑰]。 
1. 儲存金鑰和連接字串，以便稍後用於本教學課程。 

   ![存取金鑰](media/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service/access-keys.png)

### <a name="create-a-sql-server-credential"></a>建立 SQL Server 認證
使用您儲存的存取金鑰，遵循下列步驟以建立 SQL Server 認證。 

1. 使用 SQL Server Management Studio 連線到 SQL Server 
1. 選取 **AdventureWorks2016** 資料庫，並開啟 [新增查詢] 視窗。 
1. 將下列範例複製並貼入查詢視窗中，視需要修改並執行： 

  ```sql
  CREATE CREDENTIAL mycredential   
  WITH IDENTITY= 'msftutorialstorage', -- this is the name of the storage account you specified when creating a storage account   
  SECRET = '<storage account access key>' -- this should be either the Primary or Secondary Access Key for the storage account 
  ```
1. 執行陳述式以建立認證。 

## <a name="backup-database-to-the-windows-azure-blob-storage-service"></a>Windows Azure Blob 儲存體服務的資料庫備份
在本節中，您將使用 T-SQL 陳述式來執行 Windows Azure Blob 儲存體服務的完整資料庫備份。 

1. 使用 SQL Server Management Studio 連線到 SQL Server 
1. 選取 **AdventureWorks2016** 資料庫，並開啟 [新增查詢] 視窗。 
1. 將下列範例複製並貼入查詢視窗中，並視需要修改： 

 ```sql
 BACKUP DATABASE [AdventureWorks2016] 
 TO URL = 'https://msftutorialstorage.blob.core.windows.net/sql-backup/AdventureWorks2016.bak' 
 /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/ 
 WITH CREDENTIAL = 'mycredential';
 /* name of the credential you created in the previous step */ 
 GO
 ```
1. 執行陳述式，將 AdventureWorks2016 資料庫備份至 URL。 

 
## <a name="restore-database-from-windows-azure-blob-storage-service"></a>從 Windows Azure Blob 儲存體服務還原資料庫
在本節中，您將使用 T-SQL 陳述式，還原完整資料庫備份。 

1. 使用 SQL Server Management Studio 連線到 SQL Server 
1. 開啟 [新增查詢] 視窗。 
1. 將下列範例複製並貼入查詢視窗中，並視需要修改： 

 ```sql
 RESTORE DATABASE AdventureWorks2016 
 FROM URL = 'https://msftutorialstorage.blob.core.windows.net/sql-backup/AdventureWorks2016.bak' 
 WITH CREDENTIAL = 'mycredential',
 STATS = 5 -- use this to see monitor the progress
 GO
 ``` 

## <a name="see-also"></a>另請參閱 
下列是一些建議閱讀的主題，這些主題可讓您了解針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份使用 Azure Blob 儲存體服務的概念與最佳做法。  
  
-   [使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
-   [SQL Server 備份至 URL 的最佳作法和疑難排解](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  

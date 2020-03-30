---
title: 建立加密的備份 | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: e29061d3-c2ab-4d98-b9be-8e90a11d17fe
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e8f0c38d7dd712c5727fc5e9f7f62a35c1b886e1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "70280813"
---
# <a name="create-an-encrypted-backup"></a>建立加密的備份
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題說明使用 Transact-SQL 建立加密備份所需的步驟。  如需使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的範例，請參閱 [建立完整資料庫備份 (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)。 
  
## <a name="backup-to-disk-with-encryption"></a>使用加密備份到磁碟  
 **必要條件：**  
  
-   必須能夠存取用以建立資料庫備份的本機磁碟或具有足用空間的儲存體。  
  
-   主要資料庫的資料庫主要金鑰，以及 SQL Server 執行個體所提供的憑證或非對稱金鑰。 如需加密需求及權限的資訊，請參閱 [備份加密](../../relational-databases/backup-restore/backup-encryption.md)。  
  
 使用下列步驟建立要存放到本機磁碟的資料庫加密備份。 此範例會使用稱為 MyTestDB 的使用者資料庫。  
  
1.  **建立 master 資料庫的資料庫主要金鑰：** 選擇密碼以加密即將儲存於資料庫的主要金鑰副本。 連接到 Database Engine，再啟動新的查詢視窗，將下列範例複製並貼到新的查詢視窗中，然後按一下 [執行]  。  
  
    ```  
    -- Creates a database master key.   
    -- The key is encrypted using the password "<master key password>"  
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
2.  **建立備份憑證：** 在 master 資料庫中建立備份憑證。 將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**  
  
    ```  
    Use Master  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDB Backup Encryption Certificate';  
    GO  
  
    ```  
  
3.  **備份資料庫：** 指定要使用的加密演算法與憑證。 複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  

    ```
    BACKUP DATABASE [MyTestDB]  
    TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      COMPRESSION,  
      ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO
    ```  
  
 如需加密受 EKM 保護的備份的範例，請參閱[使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)。  
  
### <a name="backup-to-azure-storage-with-encryption"></a>將儲存到 Azure 儲存體的備份加密  
 如果使用 [SQL Server 備份至 URL]  選項建立要儲存到 Azure 儲存體的備份，其加密步驟完全相同，但您必須使用 URL 作為目的地，並使用 SQL 認證向 Azure 儲存體進行驗證。 如果您要將 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 設定成使用加密選項，請參閱 [啟用 SQL Server Managed Backup 到 Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)。  
  
 **必要條件：**  
  
-   一個視窗儲存體帳戶和容器。 如需詳細資訊，請參閱。 [第 1 課：建立 Azure 儲存體物件](https://msdn.microsoft.com/library/74edd1fd-ab00-46f7-9e29-7ba3f1a446c5)。  
  
-   主要資料庫的資料主要金鑰，以及 SQL Server 執行個體的憑證或非對稱金鑰。 如需加密需求及權限的資訊，請參閱 [備份加密](../../relational-databases/backup-restore/backup-encryption.md)。  
  
1.  **建立 SQL Server 認證：** 若要建立 SQL Server 認證，請連線到 Database Engine、開啟新的查詢視窗、複製並貼上下列範例，然後按一下 [執行]  。  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account    
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account  
    ```  
  
2.  **建立資料庫主要金鑰：** 選擇密碼以加密即將儲存於資料庫的主要金鑰副本。 連接到 Database Engine，再啟動新的查詢視窗，將下列範例複製並貼到新的查詢視窗中，然後按一下 [執行]  。  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
3.  **建立備份憑證：** 在 master 資料庫中建立備份憑證。 複製下列範例，並將其貼到查詢視窗中，然後按一下 [執行]  。  
  
    ```  
    USE Master;  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDBBackupEncryptCert ';  
    GO  
  
    ```  
  
4.  **備份資料庫：** 指定要使用的加密演算法與憑證。 複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO URL = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      CREDENTIAL 'mycredential' - this is the name of the credential created in the first step.  
      ,COMPRESSION  
      ,ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
  

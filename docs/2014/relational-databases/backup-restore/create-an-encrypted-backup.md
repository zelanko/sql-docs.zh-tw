---
title: 建立加密的備份 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: e29061d3-c2ab-4d98-b9be-8e90a11d17fe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7fcfdf8a6d25d950970952d9f5dec93a523dc37f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205628"
---
# <a name="create-an-encrypted-backup"></a>建立加密的備份
  本主題說明使用 Transact-SQL 建立加密備份所需的步驟。  
  
## <a name="backup-to-disk-with-encryption"></a>使用加密備份到磁碟  
 **必要條件：**  
  
-   必須能夠存取用以建立資料庫備份的本機磁碟或具有足用空間的儲存體。  
  
-   主要資料庫的資料庫主要金鑰，以及 SQL Server 執行個體所提供的憑證或非對稱金鑰。 如需加密需求及權限的資訊，請參閱 [備份加密](backup-encryption.md)。  
  
 使用下列步驟建立要存放到本機磁碟的資料庫加密備份。 此範例會使用稱為 MyTestDB 的使用者資料庫。  
  
1.  **建立主要資料庫的資料庫主要金鑰︰** 選擇要儲存在資料庫中之主要金鑰複本的加密密碼。 連接到 Database Engine，再啟動新的查詢視窗，將下列範例複製並貼到新的查詢視窗中，然後按一下 [執行]。  
  
    ```  
    -- Creates a database master key.   
    -- The key is encrypted using the password "<master key password>"  
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
2.  **建立備份憑證︰** 建立主要資料庫的備份憑證。 將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**  
  
    ```  
    Use Master  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDB Backup Encryption Certificate';  
    GO  
  
    ```  
  
3.  **備份資料庫：** 指定要使用的加密演算法與憑證。 複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
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
  
 如需加密受 EKM 保護的備份的範例，請參閱[使用 Azure 金鑰保存庫進行可延伸金鑰管理 &#40;SQL Server&#41;](../security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)。  
  
### <a name="backup-to-windows-azure-storage-with-encryption"></a>加密要儲存到 Windows Azure 儲存體的備份  
 如果使用 [SQL Server 備份至 URL] 選項建立要儲存到 Windows Azure 儲存體的備份，其加密步驟完全相同，但您必須使用 URL 作為目的地，並使用 SQL 認證向 Windows Azure 儲存體進行驗證。 如果您想要設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]使用加密選項，請參閱[設定 SQL Server Managed Backup to Windows Azure](enable-sql-server-managed-backup-to-microsoft-azure.md)和[設定 SQL Server Managed Backup to Windows Azure 的可用性群組](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md).  
  
 **必要條件：**  
  
-   一個視窗儲存體帳戶和容器。 如需詳細資訊，請參閱。 [第 1 課：建立 Windows Azure 儲存體物件](../../tutorials/lesson-1-create-windows-azure-storage-objects.md)。  
  
-   主要資料庫的資料主要金鑰，以及 SQL Server 執行個體的憑證或非對稱金鑰。 如需加密需求及權限的資訊，請參閱[備份加密](backup-encryption.md)。  
  
1.  **建立 SQL Server 認證：** 若要建立 SQL Server 認證，請連接到 Database Engine，再開啟新的查詢視窗，複製並貼上下列範例，然後按一下 [執行]。  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' – this is the name of the storage account you specified when creating a storage account    
    , SECRET = '<storage account access key>' – this should be either the Primary or Secondary Access Key for the storage account  
    ```  
  
2.  **建立資料庫主要金鑰︰** 選擇要儲存在資料庫中之主要金鑰複本的加密密碼。 連接到 Database Engine，再啟動新的查詢視窗，將下列範例複製並貼到新的查詢視窗中，然後按一下 [執行]。  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
3.  **建立備份憑證︰** 建立主要資料庫的備份憑證。 複製下列範例，並將其貼到查詢視窗中，然後按一下 [執行]。  
  
    ```  
    USE Master;  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDBBackupEncryptCert ';  
    GO  
  
    ```  
  
4.  **備份資料庫：** 指定要使用的加密演算法與憑證。 複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO URL = N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      CREDENTIAL 'mycredential' – this is the name of the credential created in the first step.  
      ,COMPRESSION  
      ,ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
  

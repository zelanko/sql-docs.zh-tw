---
title: 第 2 課：建立 SQL Server 認證 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 64f8805c-1ddc-4c96-a47c-22917d12e1ab
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fbea11b0500c075105bff885cdb1cd8264b320d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62931639"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>第 2 課：建立 SQL Server 認證
  **認證：** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認證是用來儲存連線到 SQL Server 外部資源所需之驗證資訊的物件。  此處， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份和還原程序會使用認證，向 Windows Azure BLOB 儲存體服務驗證。 認證會儲存儲存體帳戶的名稱以及儲存體帳戶的 **存取金鑰** 值。 一旦建立認證之後，您必須在發出 BACKUP/RESTORE 陳述式時，在 WITH CREDENTIAL 選項中指定認證。 如需有關如何檢視、 複製或重新產生儲存體帳戶**存取金鑰**，請參閱[儲存體帳戶存取金鑰](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx)。  
  
 如需有關認證的一般資訊，請參閱 [認證](../relational-databases/security/authentication-access/credentials-database-engine.md)。  
  
 如需有關使用認證之其他範例的詳細資訊，請參閱 [建立 SQL Server Agent Proxy](../ssms/agent/create-a-sql-server-agent-proxy.md)。  
  
> [!IMPORTANT]  
>  建立 SQL Server 認證，如下所述的需求專屬於 SQL Server 備份程序 ([SQL Server 備份至 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)，並[SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md))。 SQL Server 在存取 Azure 儲存體以寫入或讀取備份時，會使用儲存體帳戶名稱與存取金鑰資訊。  如需有關如何建立認證以在 Azure 儲存體中儲存資料庫檔案的詳細資訊，請參閱[第 3 課：建立 SQL Server 認證](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="create-a-sql-server-credential"></a>建立 SQL Server 認證  
 若要建立 SQL Server 認證，請使用下列步驟：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  在 [物件總管] 中，連接到已安裝 AdventureWorks2012 資料庫的 Database Engine 執行個體，或使用您計畫要用於此教學課程的自訂資料庫。  
  
3.  在 **[標準]** 工具列上，按一下 **[新增查詢]** 。  
  
4.  將下列範例複製並貼入查詢視窗中，並視需要修改。  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account (See Lesson 1)   
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account (See Lesson 1)  
  
    ```  
  
     ![對應至 sql 認證的儲存體帳戶](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "對應至 sql 認證的儲存體帳戶")  
  
5.  確認 T-SQL 陳述式，然後按一下**Execute**。  
  
 如需有關 Windows Azure Blob 儲存體服務之備份概念與需求的詳細資訊，請參閱 < [SQL Server 備份及還原與 Windows Azure Blob 儲存體服務](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
### <a name="next-lesson"></a>下一課  
 [第 3 課：完整資料庫備份寫入 Windows Azure Blob 儲存體服務](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)。  
  
  

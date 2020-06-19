---
title: 第2課：建立 SQL Server 認證 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 64f8805c-1ddc-4c96-a47c-22917d12e1ab
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 95118647df945840d306d2f549f9d6b1f9b5c04d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063973"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>第 2 課：建立 SQL Server 認證
  **認證：** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認證是用來儲存連線到 SQL Server 外部資源所需之驗證資訊的物件。  在這裡， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份和還原程式會使用認證來向 Azure Blob 儲存體服務進行驗證。 認證會儲存儲存體帳戶的名稱以及儲存體帳戶的 **存取金鑰** 值。 一旦建立認證之後，您必須在發出 BACKUP/RESTORE 陳述式時，在 WITH CREDENTIAL 選項中指定認證。 如需有關如何查看、複製或重新產生儲存體帳戶**存取金鑰**的詳細資訊，請參閱[儲存體帳戶存取金鑰](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx)。  
  
 如需認證的一般資訊，請參閱[認證](../relational-databases/security/authentication-access/credentials-database-engine.md)。  
  
 如需使用認證之其他範例的詳細資訊，請參閱[建立 SQL Server Agent Proxy](../ssms/agent/create-a-sql-server-agent-proxy.md)。  
  
> [!IMPORTANT]  
>  以下所述建立 SQL Server 認證的需求專屬於 SQL Server 備份程式（[SQL Server 備份至 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)，以及[SQL Server 受控備份至 Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)）。 SQL Server 在存取 Azure 儲存體以寫入或讀取備份時，會使用儲存體帳戶名稱與存取金鑰資訊。  如需建立認證以在 Azure 儲存體中儲存資料庫檔案的詳細資訊，請參閱 [Lesson 3: Create a SQL Server Credential](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="create-a-sql-server-credential"></a>建立 SQL Server 認證  
 若要建立 SQL Server 認證，請使用下列步驟：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  在 [物件總管] 中，連接到已安裝 AdventureWorks2012 資料庫的 Database Engine 執行個體，或使用您計畫要用於此教學課程的自訂資料庫。  
  
3.  在 **[標準]** 工具列上，按一下 **[新增查詢]**。  
  
4.  將下列範例複製並貼入查詢視窗中，並視需要修改。  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account (See Lesson 1)   
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account (See Lesson 1)  
  
    ```  
  
     ![將儲存體帳戶對應至 SQL 認證](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "將儲存體帳戶對應至 SQL 認證")  
  
5.  確認 T-sql 語句，然後按一下 [**執行**]。  
  
 如需有關 Azure Blob 儲存體服務的備份概念和需求的詳細資訊，請參閱[使用 Azure Blob 儲存體服務 SQL Server 備份和還原](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
### <a name="next-lesson"></a>下一課  
 [第3課：將完整資料庫備份寫入 Azure Blob 儲存體服務](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)。  
  
  

---
title: 第 5 課 （選擇性）使用 TDE 加密資料庫 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c8ef2e904c197822721a5c48f811a2a895b5ca59
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145382"
---
# <a name="lesson-5-optional-encrypt-your-database-using-tde"></a>第 5 課 (選擇性) 使用 TDE 加密資料庫
  您可以選擇加密新建立的資料庫。 透明資料加密 (TDE) 會執行資料和記錄檔的即時 I/O 加密和解密。 這類加密會使用資料庫加密金鑰 (DEK)，該金鑰儲存於資料庫開機記錄中，以便在復原期間可供使用。 如需詳細資訊，請參閱[透明資料加密&#40;TDE&#41; ](security/encryption/transparent-data-encryption.md)和[將 TDE 保護的資料庫移至另一個 SQL Server](security/encryption/move-a-tde-protected-database-to-another-sql-server.md)。  
  
 這個課程假設您已完成下列步驟：  
  
-   您擁有 Windows Azure 儲存體帳戶。  
  
-   您已在 Windows Azure 儲存體帳戶下建立容器。  
  
-   您已在容器上建立具有讀取、寫入和列出權限的原則。 您也已經產生 SAS 金鑰。  
  
-   您已在來源電腦上建立 SQL Server 認證。  
  
-   您已依照第 4 課所述的步驟建立資料庫。  
  
 如果您想要加密資料庫，請遵循下列步驟：  
  
1.  在來源電腦上，於查詢視窗中修改並執行下列陳述式：  
  
    ```  
  
    -- Create a master key and a server certificate   
    USE master   
    GO   
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01';   
    GO   
    CREATE CERTIFICATE MySQLCert WITH SUBJECT = 'SQL - Azure Storage Certification'   
    GO   
    -- Create a backup of the server certificate in the master database.   
    -- Store TDS certificates in the source machine locally.   
    BACKUP CERTIFICATE MySQLCert   
    TO FILE = 'C:\certs\MySQLCert.CER'   
    WITH PRIVATE KEY   
    (   
    FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
    ENCRYPTION BY PASSWORD = 'MySQLKey01'   
    );  
  
    ```  
  
2.  然後，依照下列步驟加密來源電腦中的新資料庫：  
  
    ```  
  
    -- Switch to the new database.   
    -- Create a database encryption key, that is protected by the server certificate in the master database.    
    -- Alter the new database to encrypt the database using TDE.   
    USE TestDB1;   
    GO   
    -- Encrypt your database   
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE MySQLCert   
    GO   
  
    ALTER DATABASE TestDB1   
    SET ENCRYPTION ON   
    GO  
  
    ```  
  
 如果您想要了解資料庫的加密狀態及相關聯的資料庫加密金鑰，請執行下列陳述式：  
  
```  
  
SELECT * FROM sys.dm_database_encryption_keys;   
GO  
  
```  
  
 For detailed information the Transact-SQL statements that have been used in this lesson, see [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql), [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql), [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql), [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql), and [sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql).  
  
 **下一課：**  
  
 [第 6 課： 將資料庫移轉來源的內部部署至 Windows Azure 中的目的地電腦的電腦](lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  

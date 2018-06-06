---
title: 還原 TDE-Parallel Data Warehouse 所保護的資料庫 |Microsoft 文件
description: 使用下列步驟來還原資料庫，Analytics Platform System 平行資料倉儲中使用透明資料加密來加密。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a791d4110dc70c506025f8f11fb06b9ba2e5dcb3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>還原平行處理資料倉儲的 TDE 所保護的資料庫
使用下列步驟將使用透明資料加密來加密的資料庫還原。  
  
[使用透明資料加密](transparent-data-encryption.md#using-tde)範例有程式碼上啟用 TDE`AdventureWorksPDW2012`資料庫。 下列程式碼會繼續執行該範例中，原始 Analytics Platform System (APS) 應用裝置上建立資料庫的備份，然後將還原的憑證，為不同的應用裝置上的資料庫。  
  
第一個步驟是建立來源資料庫的備份。  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
針對 TDE 準備新的 SQL Server PDW，請建立主要金鑰、 啟用加密，以及建立網路認證。  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
最後兩個步驟使用 從原始的 SQL Server PDW 備份，重新建立憑證。 使用您在建立憑證的備份時使用的密碼。  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert  
    FROM FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'   
    WITH PRIVATE KEY (FILE = '\\SECURE_SERVER\cert\MyServerCert.key',   
    DECRYPTION BY PASSWORD = '<password>');  
  
RESTORE DATABASE AdventureWorksPDW2012   
    FROM DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>另請參閱  
[備份資料庫](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md) 
[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[建立憑證](../t-sql/statements/create-certificate-transact-sql.md)  
[還原資料庫](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  

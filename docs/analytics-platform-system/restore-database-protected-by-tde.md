---
title: 還原 TDE-Parallel Data Warehouse 所保護的資料庫 |Microsoft Docs
description: 您可以使用下列步驟，還原使用 Analytics Platform System 平行處理資料倉儲的透明資料加密來加密資料庫。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a791d4110dc70c506025f8f11fb06b9ba2e5dcb3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157012"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>還原平行處理資料倉儲的 TDE 所保護的資料庫
您可以使用下列步驟，還原使用透明資料加密來加密資料庫。  
  
[使用透明資料加密](transparent-data-encryption.md#using-tde)範例有程式碼上啟用 TDE`AdventureWorksPDW2012`資料庫。 下列程式碼繼續該範例中，原始的 Analytics Platform System (APS) 設備，建立資料庫的備份，然後將還原的憑證和不同的設備上的資料庫。  
  
第一個步驟是建立來源資料庫的備份。  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
準備新的 SQL Server PDW tde，建立主要金鑰、 啟用加密，並建立網路認證。  
  
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
  
最後兩個步驟使用原始的 SQL Server PDW 備份，重新建立憑證。 使用您在建立憑證的備份時使用的密碼。  
  
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
[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  

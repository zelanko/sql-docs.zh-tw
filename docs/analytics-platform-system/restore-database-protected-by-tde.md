---
title: 還原 TDE 所保護的資料庫
description: 使用下列步驟，在 Analytics Platform System 平行處理資料倉儲中還原使用透明資料加密來加密的資料庫。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: bfd345ff4f55311de41140d5675809838eb06297
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766717"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>在平行處理資料倉儲中還原受 TDE 保護的資料庫
使用下列步驟還原使用透明資料加密來加密的資料庫。  
  
[Using 透明資料加密](transparent-data-encryption.md#using-tde)範例的程式碼可讓您在資料庫上啟用 TDE `AdventureWorksPDW2012` 。 下列程式碼會繼續該範例，方法是在原始的分析平臺系統上建立資料庫的備份 (AP) 設備，然後在不同的設備上還原憑證和資料庫。  
  
第一個步驟是建立源資料庫的備份。  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
建立主要金鑰、啟用加密，以及建立網路認證，以準備新的 SQL Server PDW TDE。  
  
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
  
最後兩個步驟會使用原始 SQL Server PDW 的備份來重新建立憑證。 使用您在建立憑證備份時所使用的密碼。  
  
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
[BACKUP DATABASE](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016)  
[建立主要金鑰](../t-sql/statements/create-master-key-transact-sql.md)  
[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[CREATE CERTIFICATE](../t-sql/statements/create-certificate-transact-sql.md)  
[還原資料庫](../t-sql/statements/restore-statements-transact-sql.md?view=aps-pdw-2016)

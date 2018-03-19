---
title: DROP DATABASE ENCRYPTION KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP DATABASE ENCRYPTION KEY
- DROP_DATABASE_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database encryption key, drop
- DROP DATABASE ENCRYPTION KEY statement
ms.assetid: 9231bd89-75e1-45c4-b4c8-13f08695af68
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ff97d0217b7d172c66cd47cb2f33d8920ff86ef6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="drop-database-encryption-key-transact-sql"></a>DROP DATABASE ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  卸除資料庫透明加密中所使用的資料庫加密金鑰。 如需透明資料庫加密的詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)。  
  
> [!IMPORTANT]  
>  凡是用於保護資料庫加密金鑰的憑證都應該保留備份，即便是資料庫已經不再啟用加密。 就算資料庫已不再加密，交易記錄的某些部分可能仍受到保護，因而有些作業截至資料庫執行完整備份為止或許都需要此憑證。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DROP DATABASE ENCRYPTION KEY  
```  
  
## <a name="remarks"></a>Remarks  
 如果資料庫經過加密，您必須使用 ALTER DATABASE 陳述式，先從資料庫移除加密。 等候解密完成，然後再移除資料庫加密金鑰。 如需 ALTER DATABASE 陳述式的詳細資訊，請參閱 [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。 若要檢視資料庫的狀態，請使用 [sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 動態管理檢視。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會移除資料庫加密並卸除資料庫加密金鑰。  
  
```  
ALTER DATABASE AdventureWorks2012  
SET ENCRYPTION OFF;  
GO  
/* Wait for decryption operation to complete, look for a   
value of  1 in the query below. */  
SELECT encryption_state  
FROM sys.dm_database_encryption_keys;  
GO  
USE AdventureWorks2012;  
GO  
DROP DATABASE ENCRYPTION KEY;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會移除 TDE 加密再卸除資料庫加密金鑰。  
  
```  
ALTER DATABASE AdventureWorksPDW2012  
    SET ENCRYPTION OFF;  
GO  
/* Wait for decryption operation to complete, look for a   
value of  1 in the query below. */  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
           ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM  dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;   
GO  
USE AdventureWorksPDW2012;  
GO  
DROP DATABASE ENCRYPTION KEY;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server 加密](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server 和資料庫加密金鑰 &#40;Database Engine&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)  
  
  


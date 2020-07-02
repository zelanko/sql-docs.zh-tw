---
title: sys.databases dm_database_encryption_keys （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_database_encryption_keys
- sys.dm_database_encryption_keys_TSQL
- dm_database_encryption_keys
- dm_database_encryption_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_database_encryption_keys dynamic management view
ms.assetid: 56fee8f3-06eb-4fff-969e-abeaa0c4b8e4
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3d42cc2873c1e3e03e2af3e0a01080cdb18c349a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754284"
---
# <a name="sysdm_database_encryption_keys-transact-sql"></a>sys.dm_database_encryption_keys (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回關於資料庫加密狀態及其相關聯之資料庫加密金鑰的資訊。 如需資料庫加密的詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)。  
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|**int**|資料庫的識別碼。|  
|encryption_state|**int**|指出資料庫已加密或未加密。<br /><br /> 0 = 沒有資料庫加密金鑰存在，未加密<br /><br /> 1 = 未加密<br /><br /> 2 = 加密進行中<br /><br /> 3 = 已加密<br /><br /> 4 = 金鑰變更進行中<br /><br /> 5 = 解密進行中<br /><br /> 6 = 保護變更進行中 (正在變更用於加密資料庫加密金鑰的憑證或非對稱金鑰)。|  
|create_date|**datetime**|顯示建立加密金鑰的日期（UTC）。|  
|regenerate_date|**datetime**|顯示重新產生加密金鑰的日期（UTC）。|  
|modify_date|**datetime**|顯示已修改加密金鑰的日期（UTC）。|  
|set_date|**datetime**|顯示加密金鑰套用至資料庫的日期（UTC）。|  
|opened_date|**datetime**|顯示上次開啟資料庫索引鍵的時間（UTC）。|  
|key_algorithm|**nvarchar(32)**|顯示用於金鑰的演算法。|  
|key_length|**int**|顯示金鑰的長度。|  
|encryptor_thumbprint|**varbinary(20)**|顯示加密程式的指模。|  
|encryptor_type|**nvarchar(32)**|**適用**于： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （ [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至[目前版本](https://go.microsoft.com/fwlink/p/?LinkId=299658)）。<br /><br /> 描述加密程式。|  
|percent_complete|**real**|資料庫加密狀態變更的完成百分比。 如果沒有狀態變更，這將會是 0。|
|encryption_state_desc|**nvarchar(32)**|**適用對象**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 及更新版本。<br><br> 指出資料庫是否已加密或未加密的字串。<br><br>NONE<br><br>未經<br><br>加密<br><br>DECRYPTION_IN_PROGRESS<br><br>ENCRYPTION_IN_PROGRESS<br><br>KEY_CHANGE_IN_PROGRESS<br><br>PROTECTION_CHANGE_IN_PROGRESS|
|encryption_scan_state|**int**|**適用對象**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 及更新版本。<br><br>指出加密掃描的目前狀態。 <br><br>0 = 未起始任何掃描，TDE 未啟用<br><br>1 = 掃描正在進行中。<br><br>2 = 掃描正在進行中，但已暫停，使用者可以繼續。<br><br>3 = 掃描因某些原因而中止，需要手動介入。 如需更多協助，請聯絡 Microsoft 支援服務。<br><br>4 = 掃描已成功完成，已啟用 TDE 且加密已完成。|
|encryption_scan_state_desc|**nvarchar(32)**|**適用對象**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 及更新版本。<br><br>表示加密掃描目前狀態的字串。<br><br> NONE<br><br>RUNNING<br><br>SUSPENDED<br><br>ABORTED<br><br>套|
|encryption_scan_modify_date|**datetime**|**適用對象**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 及更新版本。<br><br> 顯示上次修改加密掃描狀態的日期（UTC）。|
  
## <a name="permissions"></a>權限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在高階 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 層級上，需要 `VIEW DATABASE STATE` 資料庫的許可權。 在 [ [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   

## <a name="see-also"></a>另請參閱  

 [安全性相關的動態管理 Views 和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server 加密](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server 和資料庫加密金鑰 &#40;資料庫引擎&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [建立資料庫加密金鑰 &#40;Transact-sql&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  

---
title: "sys.dm_database_encryption_keys (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_database_encryption_keys
- sys.dm_database_encryption_keys_TSQL
- dm_database_encryption_keys
- dm_database_encryption_keys_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_database_encryption_keys dynamic management view
ms.assetid: 56fee8f3-06eb-4fff-969e-abeaa0c4b8e4
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bb177f781bee54b908624e1f940c12d5bdaf5a13
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdatabaseencryptionkeys-transact-sql"></a>sys.dm_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回關於資料庫加密狀態及其相關聯之資料庫加密金鑰的資訊。 如需有關資料庫加密的詳細資訊，請參閱[透明資料加密 &#40;TDE &#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|資料庫的識別碼。|  
|encryption_state|**int**|指出資料庫已加密或未加密。<br /><br /> 0 = 沒有資料庫加密金鑰存在，未加密<br /><br /> 1 = 未加密<br /><br /> 2 = 加密進行中<br /><br /> 3 = 已加密<br /><br /> 4 = 金鑰變更進行中<br /><br /> 5 = 解密進行中<br /><br /> 6 = 保護變更進行中 (正在變更用於加密資料庫加密金鑰的憑證或非對稱金鑰)。|  
|create_date|**datetime**|顯示建立加密金鑰的日期。|  
|regenerate_date|**datetime**|顯示重新產生加密金鑰的日期。|  
|modify_date|**datetime**|顯示修改加密金鑰的日期。|  
|set_date|**datetime**|顯示加密金鑰套用到資料庫的日期。|  
|opened_date|**datetime**|顯示上次開啟資料庫索引鍵的日期。|  
|key_algorithm|**nvarchar （32)**|顯示用於金鑰的演算法。|  
|key_length|**int**|顯示金鑰的長度。|  
|encryptor_thumbprint|**varbinary(20)**|顯示加密程式的指模。|  
|encryptor_type|**nvarchar （32)**|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。<br /><br /> 描述加密程式。|  
|percent_complete|**real**|資料庫加密狀態變更的完成百分比。 如果沒有狀態變更，這將會是 0。|  
  
## <a name="permissions"></a>Permissions  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。  
  
## <a name="see-also"></a>請參閱＜  

 [安全性相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server 加密](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server 和資料庫加密金鑰 &#40;Database Engine&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [建立資料庫加密金鑰 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  

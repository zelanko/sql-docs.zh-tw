---
title: 系統dm_database_encryption_keys(轉算-SQL) |微軟文件
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e716c826fd366fda4505b7fcf9ec8e3b756ec25
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531055"
---
# <a name="sysdm_database_encryption_keys-transact-sql"></a>sys.dm_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回關於資料庫加密狀態及其相關聯之資料庫加密金鑰的資訊。 如需資料庫加密的詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)。  
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|**int**|資料庫的識別碼。|  
|encryption_state|**int**|指出資料庫已加密或未加密。<br /><br /> 0 = 沒有資料庫加密金鑰存在，未加密<br /><br /> 1 = 未加密<br /><br /> 2 = 加密進行中<br /><br /> 3 = 已加密<br /><br /> 4 = 金鑰變更進行中<br /><br /> 5 = 解密進行中<br /><br /> 6 = 保護變更進行中 (正在變更用於加密資料庫加密金鑰的憑證或非對稱金鑰)。|  
|create_date|**datetime**|顯示創建加密金鑰的日期(以 UTC 表示)。|  
|regenerate_date|**datetime**|顯示重新產生加密密鑰的日期(以 UTC 表示)。|  
|modify_date|**datetime**|顯示已修改加密金鑰的日期(以 UTC 表示)。|  
|set_date|**datetime**|顯示加密金鑰應用於資料庫的日期(以 UTC 表示)。|  
|opened_date|**datetime**|顯示上次打開資料庫金鑰時(以 UTC 表示)。|  
|key_algorithm|**nvarchar(32)**|顯示用於金鑰的演算法。|  
|key_length|**int**|顯示金鑰的長度。|  
|encryptor_thumbprint|**varbinary(20)**|顯示加密程式的指模。|  
|encryptor_type|**nvarchar(32)**|**套用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (透過[目前版本](https://go.microsoft.com/fwlink/p/?LinkId=299658))。<br /><br /> 描述加密程式。|  
|percent_complete|**real**|資料庫加密狀態變更的完成百分比。 如果沒有狀態變更，這將會是 0。|
|encryption_state_desc|**nvarchar(32)**|**適用對象**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 及更新版本。<br><br> 指示資料庫是否加密的字串。<br><br>無<br><br>加密<br><br>加密<br><br>DECRYPTION_IN_PROGRESS<br><br>ENCRYPTION_IN_PROGRESS<br><br>KEY_CHANGE_IN_PROGRESS<br><br>PROTECTION_CHANGE_IN_PROGRESS|
|encryption_scan_state|**int**|**適用對象**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 及更新版本。<br><br>指示加密掃描的當前狀態。 <br><br>0 = 未啟動掃描,未開啟 TDE<br><br>1 = 掃描正在進行中。<br><br>2 = 掃描正在進行中,但已暫停,用戶可以繼續。<br><br>3 = 掃描由於某種原因中止,需要手動干預。 請與微軟支援部門聯繫以獲得更多説明。<br><br>4 = 掃描已成功完成,TDE 已啟用,加密已完成。|
|encryption_scan_state_desc|**nvarchar(32)**|**適用對象**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 及更新版本。<br><br>指示加密掃描的當前狀態的字串。<br><br> 無<br><br>RUNNING<br><br>SUSPENDED<br><br>ABORTED<br><br>完成|
|encryption_scan_modify_date|**datetime**|**適用對象**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 及更新版本。<br><br> 顯示上次修改的加密掃描狀態的日期(以 UTC 表示)。|
  
## <a name="permissions"></a>權限

打開[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]`VIEW SERVER STATE`時 ,需要許可權。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高級層上,需要資料庫中`VIEW DATABASE STATE`的許可權。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層上,需要**伺服器管理員**或 Azure**活動目錄管理員**帳戶。   

## <a name="see-also"></a>另請參閱  

 [與安全相關的動態管理檢視和功能&#40;處理-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [透明資料加密&#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL 伺服器加密](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL 伺服器和資料庫加密金鑰&#40;資料庫引擎&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [加密層次結構](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [變更資料庫集選項&#40;轉算-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [建立資料庫加密金鑰&#40;交易-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [變更資料庫加密金鑰&#40;轉算-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  

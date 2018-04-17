---
title: sys.dm_pdw_nodes_database_encryption_keys (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e7fd02b2-5d7e-4816-a0af-b58ae2ac3f7a
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ea3221e859093667883109c1e3977daa753230c1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmpdwnodesdatabaseencryptionkeys-transact-sql"></a>sys.dm_pdw_nodes_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  傳回關於資料庫加密狀態及其相關聯之資料庫加密金鑰的資訊。 **sys.dm_pdw_nodes_database_encryption_keys**提供這項資訊的每個節點。 如需有關資料庫加密的詳細資訊，請參閱[透明資料加密 (SQL Server PDW)](http://msdn.microsoft.com/en-us/b82ad21d-09dd-43dd-8fab-bcf2c8c3ac6d)。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|每個節點上的實體資料庫的識別碼。|  
|encryption_state|**int**|表示此節點上的資料庫是否經過加密或未加密。<br /><br /> 0 = 沒有資料庫加密金鑰存在，未加密<br /><br /> 1 = 未加密<br /><br /> 2 = 加密進行中<br /><br /> 3 = 已加密<br /><br /> 4 = 金鑰變更進行中<br /><br /> 5 = 解密進行中<br /><br /> 6 = 保護變更進行 （加密資料庫加密金鑰的憑證已經變更。）|  
|create_date|**datetime**|顯示建立加密金鑰的日期。|  
|regenerate_date|**datetime**|顯示重新產生加密金鑰的日期。|  
|modify_date|**datetime**|顯示修改加密金鑰的日期。|  
|set_date|**datetime**|顯示加密金鑰套用到資料庫的日期。|  
|opened_date|**datetime**|顯示上次開啟資料庫索引鍵的日期。|  
|key_algorithm|**varchar(?)**|顯示用於金鑰的演算法。|  
|key_length|**int**|顯示金鑰的長度。|  
|encryptor_thumbprint|**varbin**|顯示加密程式的指模。|  
|percent_complete|**real**|資料庫加密狀態變更的完成百分比。 如果沒有狀態變更，這將會是 0。|  
|node_id|**int**|與節點相關聯的唯一數值識別碼。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例聯結`sys.dm_pdw_nodes_database_encryption_keys`其他系統資料表，以指出每個節點的 TDE 保護的資料庫加密狀態。  
  
```  
SELECT D.database_id AS DBIDinMaster, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName,   
keys.encryption_state  
FROM sys.dm_pdw_nodes_database_encryption_keys AS keys  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON keys.database_id = PD.database_id AND keys.pdw_node_id = PD.pdw_node_id  
JOIN sys.pdw_database_mappings AS DM  
    ON DM.physical_name = PD.physical_name  
JOIN sys.databases AS D  
    ON D.database_id = DM.database_id  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  


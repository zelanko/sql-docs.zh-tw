---
title: sp_pdw_database_encryption_regenerate_system_keys (SQL 資料倉儲) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: bb13e323-a984-4462-8b6d-6019c38ddd9d
author: ronortloff
ms.author: rortloff
ms.reviewer: ''
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c3b0101630a45ee7d4084a1b61a3b20ee0b2779b
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173205"
---
# <a name="sp_pdw_database_encryption_regenerate_system_keys-sql-data-warehouse"></a>sp_pdw_database_encryption_regenerate_system_keys (SQL 資料倉儲) 

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  使用**sp_pdw_database_encryption_regenerate_system_keys**在設備上啟用 TDE 時，針對已加密的內部資料庫，旋轉憑證和資料庫加密金鑰。 這包括 `tempdb`。 只有在啟用 TDE 時，才會成功。  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption_regenerate_system_keys  ;  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)   
  
## <a name="remarks"></a>備註  
 程式沒有任何參數。  
  
 當設備中的流量偏低時，應使用此程式。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定資料庫角色中的成員資格，或**CONTROL SERVER**許可權。  
  
## <a name="example"></a>範例  
 下列範例會重新產生資料庫加密金鑰。  
  
```sql  
EXEC sys.sp_pdw_database_encryption_regenerate_system_keys;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_pdw_database_encryption &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  

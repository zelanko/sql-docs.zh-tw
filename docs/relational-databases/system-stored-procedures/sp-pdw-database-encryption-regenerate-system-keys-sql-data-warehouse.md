---
title: sp_pdw_database_encryption_regenerate_system_keys (Azure Synapse Analytics) Microsoft Docs
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
ms.openlocfilehash: aa0f0f3afb40492e398e316095a3458169d03eaf
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92059306"
---
# <a name="sp_pdw_database_encryption_regenerate_system_keys-azure-synapse-analytics"></a>sp_pdw_database_encryption_regenerate_system_keys (Azure Synapse Analytics) 

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  使用 **sp_pdw_database_encryption_regenerate_system_keys** 來輪替在設備上啟用 TDE 時所加密內部資料庫的憑證和資料庫加密金鑰。 這包括 `tempdb`。 只有當 TDE 已啟用時，才會成功。  
  
## <a name="syntax"></a>Syntax  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_database_encryption_regenerate_system_keys  ;  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 此程式沒有參數。  
  
 當設備中的流量較低時，應使用此程式。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員（sysadmin** ）固定資料庫角色中的成員資格或 **CONTROL SERVER** 許可權。  
  
## <a name="example"></a>範例  
 下列範例會重新產生資料庫加密金鑰。  
  
```sql  
EXEC sys.sp_pdw_database_encryption_regenerate_system_keys;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_pdw_database_encryption &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  

---
description: 'sp_pdw_database_encryption (Azure Synapse Analytics) '
title: sp_pdw_database_encryption (Azure Synapse Analytics) Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 142ebd04c32491a800dbc7651fe91fbcdd715a56
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92059226"
---
# <a name="sp_pdw_database_encryption-azure-synapse-analytics"></a>sp_pdw_database_encryption (Azure Synapse Analytics) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  使用 **sp_pdw_database_encryption** 來啟用設備的透明資料加密 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 當 **sp_pdw_database_encryption** 設定為1時，請使用 **ALTER database** 語句來加密資料庫，方法是使用 TDE。  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

#### <a name="parameters"></a>參數  
`[ @enabled = ] enabled` 判斷是否已啟用透明資料加密。 *enabled* 是 **int**，它可以是下列其中一個值：  
  
-   0 = 停用  
  
-   1 = 啟用  
  
 執行不含參數的 **sp_pdw_database_encryption** 會將設備上 TDE 的目前狀態傳回為純量結果集：0表示已停用，或1表示已啟用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 使用 **sp_pdw_database_encryption**啟用 TDE 時，會卸載 tempdb 資料庫、重新建立和加密。 基於這個理由，當使用 tempdb 的其他使用中會話時，無法在設備上啟用 TDE。 在設備上啟用或停用 TDE 是變更設備狀態的動作，在大部分情況下，預期會在設備存留期內執行一次，而且應該在設備上沒有流量時執行。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員（sysadmin** ）固定資料庫角色中的成員資格或 **CONTROL SERVER** 許可權。  
  
## <a name="example"></a>範例  
 下列範例會在設備上啟用 TDE。  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  

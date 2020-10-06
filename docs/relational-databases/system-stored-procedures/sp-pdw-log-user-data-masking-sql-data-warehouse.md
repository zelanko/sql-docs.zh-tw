---
description: 'sp_pdw_log_user_data_masking (SQL 資料倉儲) '
title: sp_pdw_log_user_data_masking (SQL 資料倉儲) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4b13e74eb5b40d76f6cbdec049a8680299d0c86f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723842"
---
# <a name="sp_pdw_log_user_data_masking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (SQL 資料倉儲) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  使用 **sp_pdw_log_user_data_masking** 來啟用活動記錄中的使用者資料遮罩 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 使用者資料遮罩會影響設備上所有資料庫上的語句。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]受**sp_pdw_log_user_data_masking**影響的活動記錄是特定的 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 活動記錄。 **sp_pdw_log_user_data_masking** 不會影響資料庫交易記錄檔或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔。  
  
 **背景：** 在預設的設定 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 活動記錄中包含完整 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的語句，而且在某些情況下，可能會包含包含在作業中的使用者資料，例如 **INSERT**、 **UPDATE**和 **SELECT** 語句。 如果設備發生問題，這允許分析造成問題的狀況，而不需要重現問題。 為了防止使用者資料寫入 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 活動記錄，客戶可以選擇使用此預存程式來開啟使用者資料遮罩。 這些語句仍會寫入至 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 活動記錄，但是語句中可能包含使用者資料的所有常值都會被遮罩，並取代為一些預先定義的常數值。  
  
 在設備上啟用透明資料加密時，會 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 自動開啟活動記錄中的使用者資料遮罩。  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
#### <a name="parameters"></a>參數  
`[ @masking_mode = ] masking_mode` 判斷是否已啟用透明資料加密記錄使用者資料遮罩。 *masking_mode* 是 **int**，而且可以是下列其中一個值：  
  
-   0 = 已停用，使用者資料會出現在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 活動記錄中。  
  
-   1 = 啟用，使用者資料語句會出現在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 活動記錄中，但會遮罩使用者資料。  
  
-   2 = 包含使用者資料的語句不會寫入 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 活動記錄中。  
  
 在沒有參數的情況下執行 **sp_pdw_ log_user_data_masking** 會傳回設備上 TDE 記錄使用者資料遮罩的目前狀態，作為純量結果集。  
  
## <a name="remarks"></a>備註  
 活動記錄中的使用者資料遮罩可讓您將 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 常值取代為 **SELECT** 和 DML 語句中預先定義的常數值，因為它們可以包含使用者資料。 將 *masking_mode* 設定為1不會遮罩中繼資料，例如資料行名稱或資料表名稱。 將 *masking_mode* 設定為2會移除具有中繼資料的語句，例如資料行名稱或資料表名稱。  
  
 活動記錄中的使用者資料遮罩 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 會以下列方式實作為：  
  
-   預設會關閉活動記錄中的 TDE 和使用者資料遮罩 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 如果設備上未啟用資料庫加密，將不會自動遮罩這些語句。  
  
-   在設備上啟用 TDE 會自動開啟活動記錄中的使用者資料遮罩 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。  
  
-   停用 TDE 並不會影響活動記錄中的使用者資料遮罩 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。  
  
-   您可以 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 使用 **sp_pdw_log_user_data_masking** 程式，在活動記錄中明確啟用使用者資料遮罩。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員（sysadmin** ）固定資料庫角色中的成員資格或 **CONTROL SERVER** 許可權。  
  
## <a name="example"></a>範例  
 下列範例會在設備上啟用 TDE 記錄使用者資料遮罩。  
  
```sql  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_pdw_database_encryption &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  

---
title: sp_pdw_log_user_data_masking （SQL 資料倉儲） |Microsoft Docs
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
ms.openlocfilehash: 18798dece1c801ad0cc4854b7fccc15529a56d5c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68056456"
---
# <a name="sp_pdw_log_user_data_masking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking （SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用**sp_pdw_log_user_data_masking** ，在活動記錄中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]啟用使用者資料遮罩。 使用者資料遮罩會影響設備上所有資料庫上的語句。  
  
> [!IMPORTANT]  
>  受[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] **sp_pdw_log_user_data_masking**影響的活動記錄是特定[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]的活動記錄。 **sp_pdw_log_user_data_masking**不會影響資料庫交易記錄檔[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或錯誤記錄檔。  
  
 **背景：**[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]在預設設定活動記錄中包含完整[!INCLUDE[tsql](../../includes/tsql-md.md)]的語句，而且在某些情況下，可以包含**INSERT**、 **UPDATE**和**SELECT**語句等作業中包含的使用者資料。 在設備上發生問題時，這會允許分析造成問題的狀況，而不需要重現問題。 為了避免將使用者資料寫入[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄，客戶可以選擇使用這個預存程式來開啟使用者資料遮罩。 這些語句仍然會寫入[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄中，但是語句中可能包含使用者資料的所有常值都會被遮罩;已取代為一些預先定義的常數值。  
  
 在設備上啟用透明資料加密時，會自動開啟 [活動記錄] [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]中的使用者資料遮罩。  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>參數  
`[ @masking_mode = ] masking_mode`決定是否啟用透明資料加密記錄使用者資料遮罩。 *masking_mode*是**int**，而且可以是下列其中一個值：  
  
-   0 = 已停用，使用者資料會[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]出現在活動記錄中。  
  
-   1 = 已啟用，使用者資料語句會出現[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]在活動記錄中，但使用者資料已遮罩。  
  
-   2 = 包含使用者資料的[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]語句不會寫入活動記錄中。  
  
 不使用參數執行**sp_pdw_ log_user_data_masking** ，會以純量結果集的形式傳回設備上 TDE 記錄使用者資料遮罩的目前狀態。  
  
## <a name="remarks"></a>備註  
 活動記錄中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]的使用者資料遮罩可讓您使用**SELECT**和 DML 語句中預先定義的常數值來取代常值，因為它們可以包含使用者資料。 將*masking_mode*設定為1並不會遮罩中繼資料，例如資料行名稱或資料表名稱。 將*masking_mode*設定為2時，會移除含有中繼資料的語句，例如資料行名稱或資料表名稱。  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄中的使用者資料遮罩會以下列方式執行：  
  
-   預設會關閉活動記錄中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]的 TDE 和使用者資料遮罩。 如果設備上未啟用資料庫加密，將不會自動遮罩這些語句。  
  
-   在設備上啟用 TDE 會自動開啟活動記錄中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]的使用者資料遮罩。  
  
-   停用 TDE 不會影響活動記錄中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]的使用者資料遮罩。  
  
-   您可以使用**sp_pdw_log_user_data_masking**程式，在活動[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]記錄中明確啟用使用者資料遮罩。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定資料庫角色中的成員資格，或**CONTROL SERVER**許可權。  
  
## <a name="example"></a>範例  
 下列範例會在設備上啟用 TDE 記錄使用者資料遮罩。  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_pdw_database_encryption &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  

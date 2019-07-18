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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056456"
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking （SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用**sp_pdw_log_user_data_masking**若要啟用使用者資料遮罩中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。 使用者資料遮罩會影響應用裝置上的所有資料庫的陳述式。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔受到**sp_pdw_log_user_data_masking**確定[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。 **sp_pdw_log_user_data_masking**不會影響資料庫交易記錄檔，或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]錯誤記錄檔。  
  
 **背景：** 在預設組態[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔包含完整[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式，以及在某些情況下可以包含使用者資料包含 operations**插入**， **UPDATE**，和**選取**陳述式。 如果發生在應用裝置上的問題，這可讓分析造成問題，而不需要重現問題的原因。 若要防止使用者資料寫入至[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄，客戶可以選擇使用此預存程序開啟使用者資料遮罩。 陳述式仍會寫入至[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔，但所有可能包含使用者資料的陳述式中的常值會加上遮罩; 取代一些預先定義的常數值。  
  
 在應用裝置上啟用透明資料加密時，遮罩中的使用者資料[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔會自動開啟。  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>參數  
`[ @masking_mode = ] masking_mode` 判斷是否已啟用透明資料加密記錄使用者資料遮罩。 *masking_mode*已**int**，而且可以是下列值之一：  
  
-   0 = 停用，使用者資料會出現在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。  
  
-   1 = 啟用，使用者資料陳述式出現在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔，但使用者資料已遮罩。  
  
-   2 = 陳述式包含使用者資料不會寫入至[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。  
  
 執行**sp_pdw_ log_user_data_masking**沒有參數傳回做為純量結果集的應用裝置上的 TDE 記錄使用者資料遮罩的目前狀態。  
  
## <a name="remarks"></a>備註  
 遮罩中的使用者資料[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]預先定義的常值中的活動記錄的常值的可取代**選取**和 DML 陳述式，因為它們可以包含使用者資料。 設定*masking_mode* 1 不會加上遮罩中繼資料，例如資料行名稱或資料表名稱。 設定*masking_mode*為 2 會在命令提示字元中移除陳述式與中繼資料，例如資料行名稱或資料表名稱。  
  
 遮罩中的使用者資料[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔實作方式如下：  
  
-   遮罩中的 TDE 」 和 「 使用者資料[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔預設會關閉。 陳述式將不會自動遮罩如果設備上未啟用資料庫加密。  
  
-   在應用裝置上啟用 TDE 時，也將會自動開啟中之使用者的資料遮罩[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。  
  
-   停用 TDE 不會影響使用者資料遮罩中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。  
  
-   您可以明確地啟用使用者資料在遮罩[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]使用的活動記錄**sp_pdw_log_user_data_masking**程序。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定資料庫角色，或**CONTROL SERVER**權限。  
  
## <a name="example"></a>範例  
 下列範例會啟用 TDE 記錄檔的使用者資料遮罩應用裝置上。  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_pdw_database_encryption &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  

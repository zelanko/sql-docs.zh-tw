---
title: sp_pdw_log_user_data_masking （SQL 資料倉儲） |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: data-warehouse
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6b158d6c0ea65159d6e310512ee45abb4916a0e7
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
ms.locfileid: "33701798"
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking （SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用**sp_pdw_log_user_data_masking**可啟用使用者資料遮罩中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。 使用者資料遮罩會影響應用裝置上的所有資料庫的陳述式。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔受到**sp_pdw_log_user_data_masking**確定[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。 **sp_pdw_log_user_data_masking**不會影響資料庫交易記錄檔，或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]錯誤記錄檔。  
  
 **背景：** 預設組態中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔包含完整[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式，以及在某些情況下可以包含這類作業中所包含的使用者資料**插入**， **更新**，和**選取**陳述式。 如果發生問題的應用裝置上，這可讓分析造成問題而需要在重現問題的原因。 若要防止使用者資料寫入至[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔中，客戶可以選擇使用這個預存程序開啟使用者資料遮罩。 陳述式仍會寫入[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔，但所有可能包含使用者資料的陳述式中的常值的遮罩; 某些預先定義的常值取代。  
  
 應用裝置上啟用透明資料加密時，遮罩中的使用者資料的[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔會自動開啟。  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>參數  
 [ **@masking_mode=** ] *masking_mode*  
 判斷是否已啟用透明資料加密記錄使用者資料遮罩。 *masking_mode*是**int**，而且可以是下列值之一：  
  
-   0 = 停用，使用者資料會出現在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。  
  
-   1 = 啟用，使用者資料陳述式出現在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]遮罩 活動記錄檔，但是使用者資料。  
  
-   2 = 陳述式不會包含使用者資料寫入至[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。  
  
 執行**sp_pdw_ log_user_data_masking**沒有參數傳回做為純量結果集的應用裝置上的 TDE 記錄使用者資料遮罩的目前狀態。  
  
## <a name="remarks"></a>備註  
 使用者資料遮罩中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄可讓取代常值的預先定義的常值中**選取**和 DML 陳述式，因為它們可以包含使用者資料。 設定*masking_mode* 1 未加上遮罩中繼資料，例如資料行名稱或資料表名稱。 設定*masking_mode*為 2 會在命令提示字元中移除陳述式與中繼資料，例如資料行名稱或資料表名稱。  
  
 使用者資料遮罩中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔以下列方式實作：  
  
-   TDE 和使用者資料遮罩中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔預設會關閉。 陳述式不會自動遮罩如果應用裝置上未啟用資料庫加密。  
  
-   應用裝置上啟用 TDE 時，也將會自動開啟中之使用者資料遮罩[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。  
  
-   停用 TDE 不會影響使用者資料遮罩中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔。  
  
-   您可以明確地啟用使用者資料遮罩中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]活動記錄檔使用**sp_pdw_log_user_data_masking**程序。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定資料庫角色或**CONTROL SERVER**權限。  
  
## <a name="example"></a>範例  
 下列範例會啟用 TDE 記錄使用者資料遮罩應用裝置上。  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_pdw_database_encryption &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  

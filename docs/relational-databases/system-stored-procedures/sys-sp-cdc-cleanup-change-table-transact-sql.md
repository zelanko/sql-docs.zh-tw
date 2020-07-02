---
title: sys.databases sp_cdc_cleanup_change_table （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_cleanup_change_table
- sp_cdc_cleanup_change_table_TSQL
- sys.sp_cdc_cleanup_change_table
- sys.sp_cdc_cleanup_change_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_cleanup_change_tables
- sp_cdc_cleanup_change_tables
ms.assetid: 02295794-397d-4445-a3e3-971b25e7068d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 061321d6fdefb52890a54fb7e18aa0a618cd986f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85626244"
---
# <a name="syssp_cdc_cleanup_change_table-transact-sql"></a>sys.sp_cdc_cleanup_change_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  根據指定的*low_water_mark*值，從目前資料庫的變更資料表中移除資料列。 這個預存程序會提供給想要直接管理變更資料表清除程序的使用者。 不過，請謹慎使用，因為此程序會影響變更資料表中資料的所有取用者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_cleanup_change_table   
  [ @capture_instance = ] 'capture_instance',   
  [ @low_water_mark = ] low_water_mark ,  
  [ @threshold = ]'delete threshold'  
```  
  
## <a name="arguments"></a>引數  
 [ @capture_instance =] '*capture_instance*'  
 是與變更資料表相關聯之擷取執行個體的名稱。 *capture_instance*是**sysname**，沒有預設值，而且不能是 Null。  
  
 *capture_instance*必須為存在於目前資料庫中的 capture 實例命名。  
  
 [ @low_water_mark =] *low_water_mark*  
 這是一個記錄序號（LSN），用來當做*capture 實例*的新下限標準。 *low_water_mark*是**binary （10）**，沒有預設值。  
  
 如果此值為非 null，它就必須顯示為[cdc. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)資料表中目前專案的 start_lsn 值。 如果 cdc.lsn_time_mapping 中的其他項目與新下限標準所識別的項目共用相同的認可時間，系統就會選擇與該項目群組相關聯的最小 LSN 做為下限標準。  
  
 如果將此值明確設定為 Null，則會使用*capture 實例*目前的*下限*標準來定義清除作業的上限。  
  
 [ @threshold =] '*刪除閾值*'  
 是可以使用單一清除陳述式來刪除的最大刪除項目數。 *delete_threshold*是**Bigint**，預設值是5000。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 sys.sp_cdc_cleanup_change_table 會執行下列作業：  
  
1.  如果 @low_water_mark 參數不是 Null，它會將*capture 實例*的 start_lsn 值設定為新的*下限*標準。  
  
    > [!NOTE]  
    >  新下限標準可能不是預存程序呼叫中指定的下限標準。 如果 cdc.lsn_time_mapping 資料表中的其他項目共用相同的認可時間，系統就會選取在項目群組中表示的最小 start_lsn 做為已調整的下限標準。 如果 @low_water_mark 參數為 Null，或目前的下限標準大於新的 lowwatermark，則會將 capture 實例的 start_lsn 值保持不變。  
  
2.  然後，系統會刪除 __$start_lsn 值小於下限標準的變更資料表項目。 此 delete threshold 是用來限制在單一交易中刪除的資料列數目。 雖然系統會回報無法成功刪除項目，但是不會影響對擷取執行個體下限標準所做的任何變更，因為這些變更可能已經根據呼叫完成了。  

 您可以在下列情況中使用 sys.sp_cdc_cleanup_change_table：  
  
-   清除代理程式作業回報刪除失敗。  
  
     管理員可以明確執行這個預存程序來重試失敗的作業。 若要針對指定的 capture 實例重試清除，請執行 sys. sp_cdc_cleanup_change_table，並為 @low_water_mark 參數指定 Null。  
  
-   清除代理程式作業所使用的簡單保留性原則不足。  
  
     因為這個預存程序會針對單一擷取執行個體執行清除作業，所以它可用來建立自訂清除策略，以便為個別擷取執行個體修改清除規則。  
  
## <a name="permissions"></a>權限  
 需要 db_owner 固定資料庫角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [cdc. fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [fn_cdc_get_min_lsn &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [sys.fn_cdc_increment_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)  
  
  

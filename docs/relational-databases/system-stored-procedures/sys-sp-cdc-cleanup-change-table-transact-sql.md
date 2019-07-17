---
title: sys.sp_cdc_cleanup_change_table (TRANSACT-SQL) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dcf68e23652eb81e163722f69d9645c7502af5b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106518"
---
# <a name="sysspcdccleanupchangetable-transact-sql"></a>sys.sp_cdc_cleanup_change_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  根據指定的目前資料庫中的變更資料表中移除資料列*low_water_mark&lt*值。 這個預存程序會提供給想要直接管理變更資料表清除程序的使用者。 不過，請謹慎使用，因為此程序會影響變更資料表中資料的所有取用者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_cleanup_change_table   
  [ @capture_instance = ] 'capture_instance',   
  [ @low_water_mark = ] low_water_mark ,  
  [ @threshold = ]'delete threshold'  
```  
  
## <a name="arguments"></a>引數  
 [ @capture_instance = ] '*capture_instance*'  
 是與變更資料表相關聯之擷取執行個體的名稱。 *capture_instance*已**sysname**，沒有預設值，不能是 NULL。  
  
 *擷取執行個體*必須命名為存在於目前資料庫中的擷取執行個體。  
  
 [ @low_water_mark = ] *low_water_mark*  
 記錄序號 (LSN) 來作為新下限標準所*擷取執行個體*。 *low_water_mark&lt*已**binary(10)** ，沒有預設值。  
  
 如果值為非 null，它必須顯示成中目前項目的 start_lsn 值[cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)資料表。 如果 cdc.lsn_time_mapping 中的其他項目與新下限標準所識別的項目共用相同的認可時間，系統就會選擇與該項目群組相關聯的最小 LSN 做為下限標準。  
  
 如果此值明確設定為 NULL，目前*低水位線*for*擷取執行個體*用來定義清除作業的上限。  
  
 [ @threshold=] '*刪除閾值*'  
 是可以使用單一清除陳述式來刪除的最大刪除項目數。 *delete_threshold*已**bigint**，預設值是 5000。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 sys.sp_cdc_cleanup_change_table 會執行下列作業：  
  
1.  如果@low_water_mark參數不是 NULL，它會設定的 start_lsn 值*擷取執行個體*新*下限標準*。  
  
    > [!NOTE]  
    >  新下限標準可能不是預存程序呼叫中指定的下限標準。 如果 cdc.lsn_time_mapping 資料表中的其他項目共用相同的認可時間，系統就會選取在項目群組中表示的最小 start_lsn 做為已調整的下限標準。 如果@low_water_mark參數為 NULL 或目前的下限標準大於新的下限標準、 start_lsn 值的擷取執行個體就會維持不變。  
  
2.  然後，系統會刪除 __$start_lsn 值小於下限標準的變更資料表項目。 此 delete threshold 是用來限制在單一交易中刪除的資料列數目。 雖然系統會回報無法成功刪除項目，但是不會影響對擷取執行個體下限標準所做的任何變更，因為這些變更可能已經根據呼叫完成了。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 您可以在下列情況中使用 sys.sp_cdc_cleanup_change_table：  
  
-   清除代理程式作業回報刪除失敗。  
  
     管理員可以明確執行這個預存程序來重試失敗的作業。 若要重試清除針對給定的擷取執行個體，請執行 sys.sp_cdc_cleanup_change_table，並指定 NULL@low_water_mark參數。  
  
-   清除代理程式作業所使用的簡單保留性原則不足。  
  
     因為這個預存程序會針對單一擷取執行個體執行清除作業，所以它可用來建立自訂清除策略，以便為個別擷取執行個體修改清除規則。  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 固定資料庫角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [sys.fn_cdc_increment_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)  
  
  

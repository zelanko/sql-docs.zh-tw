---
title: sp_post_msx_operation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f36ad40a2b16401218fe2a5927407464fe6ac11b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536122"
---
# <a name="sppostmsxoperation-transact-sql"></a>sp_post_msx_operation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將動作 （資料列） 插入**sysdownloadlist**下載並執行的目標伺服器的系統資料表。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_post_msx_operation  
     [ @operation = ] 'operation'  
     [ , [ @object_type = ] 'object' ]   
     { , [ @job_id = ] job_id }   
     [ , [ @specific_target_server = ] 'target_server' ]   
     [ , [ @value = ] value ]  
     [ , [ @schedule_uid = ] schedule_uid ]  
```  
  
## <a name="arguments"></a>引數  
`[ @operation = ] 'operation'` 所公佈之作業的類型。 *作業*已**varchar(64)**，沒有預設值。 有效的動作會隨著*object_type*。  
  
|物件類型|運算|  
|-----------------|---------------|  
|**JOB**|Insert<br /><br /> UPDATE<br /><br /> DELETE<br /><br /> START<br /><br /> STOP|  
|**SERVER**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**排程**|Insert<br /><br /> UPDATE<br /><br /> DELETE|  
  
`[ @object_type = ] 'object'` 要張貼作業的物件型別。 有效的類型為**作業**，**伺服器**，並**排程**。 *物件*已**varchar(64)**，預設值是**作業**。  
  
`[ @job_id = ] job_id` 要套用作業的工作作業識別碼。 *job_id*已**uniqueidentifier**，沒有預設值。 **0x00**表示所有作業。 如果*物件*是**伺服器**，然後*job_id*並非必要。  
  
`[ @specific_target_server = ] 'target_server'` 指定的作業所適用的目標伺服器的名稱。 如果*job_id*未指定，但*target_server*未指定，作業會張貼的所有作業之作業的伺服器。 *target_server*已**nvarchar(30)**，預設值是 NULL。  
  
`[ @value = ] value` 輪詢間隔，以秒為單位。 *value* 是 **int**，預設值是 NULL。 指定此參數才*作業*是**集民意調查**。  
  
`[ @schedule_uid = ] schedule_uid` 要套用作業的排程唯一識別碼。 *schedule_uid*已**uniqueidentifier**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_post_msx_operation**必須從執行**msdb**資料庫。  
  
 **sp_post_msx_operation**可以永遠安全呼叫它首先會判斷如果目前的伺服器是多伺服器的 Microsoft SQL Server Agent，若是如此，因為是否*物件*是多伺服器作業。  
  
 尚未公佈作業之後，它會出現在**sysdownloadlist**資料表。 建立和公佈作業之後，也必須通知目標伺服器 (TSX) 後續的作業變更。 這也可以利用下載清單加以完成。  
  
 我們強烈建議您利用 SQL Server Management Studio 來管理下載清單。 如需詳細資訊，請參閱 <<c0> [ 檢視或修改工作](../../ssms/agent/view-or-modify-jobs.md)。  
  
## <a name="permissions"></a>Permissions  
 若要執行這個預存程序，使用者必須授與**sysadmin**固定的伺服器角色。  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

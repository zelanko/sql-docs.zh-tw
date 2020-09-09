---
description: sp_post_msx_operation (Transact-SQL)
title: sp_post_msx_operation (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 304eef1c0e707ecb77fb8d13d5e2b524eb9e9e00
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545971"
---
# <a name="sp_post_msx_operation-transact-sql"></a>sp_post_msx_operation (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將 (資料列的作業插入) 至目標伺服器的 **sysdownloadlist** 系統資料表中，以下載並執行。  
  
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
`[ @operation = ] 'operation'` 已張貼作業的作業類型。 *運算*是 **Varchar (64) **，沒有預設值。 有效的作業取決於 *object_type*。  
  
|物件類型|作業|  
|-----------------|---------------|  
|**工作**|Insert<br /><br /> UPDATE<br /><br /> 刪除<br /><br /> 開始<br /><br /> STOP|  
|**伺服器**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**附表**|Insert<br /><br /> UPDATE<br /><br /> 刪除|  
  
`[ @object_type = ] 'object'` 要在其中張貼作業的物件類型。 有效的類型為 **JOB**、 **SERVER**和 **SCHEDULE**。 *物件* 是 **Varchar (64) **，預設值是 **JOB**。  
  
`[ @job_id = ] job_id` 作業所套用之作業的作業識別碼。 *job_id* 是 **uniqueidentifier**，沒有預設值。 **0x00** 表示所有作業。 如果 *物件* 為 **SERVER**，則不需要 *job_id*。  
  
`[ @specific_target_server = ] 'target_server'` 要套用指定作業的目標伺服器名稱。 如果指定 *job_id* ，但未指定 *target_server* ，則會針對作業的所有作業伺服器張貼作業。 *target_server* 是 **Nvarchar (30) **，預設值是 Null。  
  
`[ @value = ] value` 輪詢間隔（以秒為單位）。 *value* 是 **int**，預設值是 NULL。 只有在作業**設定為輪詢***時，才*指定此參數。  
  
`[ @schedule_uid = ] schedule_uid` 作業所套用之排程的唯一識別碼。 *schedule_uid* 是 **uniqueidentifier**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_post_msx_operation** 必須從 **msdb** 資料庫執行。  
  
 您一律可以安全地呼叫**sp_post_msx_operation** ，因為它會先判斷目前伺服器是否為多伺服器 Microsoft SQL Server 代理程式，如果是，*物件*是否為多伺服器作業。  
  
 在作業張貼之後，它會出現在 **sysdownloadlist** 資料表中。 建立和公佈作業之後，也必須通知目標伺服器 (TSX) 後續的作業變更。 這也可以利用下載清單加以完成。  
  
 我們強烈建議您利用 SQL Server Management Studio 來管理下載清單。 如需詳細資訊，請參閱 [查看或修改作業](../../ssms/agent/view-or-modify-jobs.md)。  
  
## <a name="permissions"></a>權限  
 若要執行這個預存程式，使用者必須被授與 **系統管理員（sysadmin** ）固定伺服器角色。  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

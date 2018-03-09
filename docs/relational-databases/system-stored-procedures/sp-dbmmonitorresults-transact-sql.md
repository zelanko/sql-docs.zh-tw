---
title: "sp_dbmmonitorresults (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorresults
- sp_dbmmonitorresults_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorresults
- database mirroring [SQL Server], monitoring
ms.assetid: d575e624-7d30-4eae-b94f-5a7b9fa5427e
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ce88354c3d378dbfa2e7bc71acd57ed52aaf5131
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="spdbmmonitorresults-transact-sql"></a>sp_dbmmonitorresults (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從儲存資料庫鏡像監視記錄的狀態資料表傳回受監視資料庫的狀態資料列，並讓您選擇此程序是否要事前取得最新的狀態。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbmmonitorresults database_name   
   , rows_to_return  
    , update_status   
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 指定要傳回其鏡像狀態的資料庫。  
  
 *rows_to_return*  
 指定傳回的資料列數量：  
  
 0 = 最後一個資料列  
  
 1 = 最後兩個小時的資料列  
  
 2 = 最後四個小時的資料列  
  
 3 = 最後八個小時的資料列  
  
 4 = 最後一天的資料列  
  
 5 = 最後兩天的資料列  
  
 6 = 最後一個 100 個資料列  
  
 7 = 500 最後一個資料列  
  
 8 = 最後 1,000 資料列  
  
 9 = 最後 1,000,000 個資料列  
  
 *update_status*  
 指定傳回結果之前，程序的條件如下：  
  
 0 = 不要更新資料庫的狀態。 只會使用最後兩個資料列來計算結果，而資料列的存在時間是依狀態資料表於何時重新整理而定。  
  
 1 = 呼叫以更新資料庫的狀態**sp_dbmmonitorupdate**計算結果之前。 不過，如果在前 15 秒或使用者已更新狀態資料表不是成員的**sysadmin**固定伺服器角色、 **sp_dbmmonitorresults**執行時不會更新的狀態。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
 針對指定的資料庫傳回所要求的記錄狀態資料列數目。 每個資料列都包含下列資訊：  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|鏡像資料庫名稱。|  
|**角色**|**int**|伺服器執行個體目前的鏡像角色：<br /><br /> 1 = 主體<br /><br /> 2 = 鏡像|  
|**mirroring_state**|**int**|資料庫狀態：<br /><br /> 0 = 已暫停<br /><br /> 1 = 已中斷連接<br /><br /> 2 = 正在同步處理<br /><br /> 3 = 暫止容錯移轉<br /><br /> 4 = 已同步處理|  
|**witness_status**|**int**|資料庫的資料庫鏡像工作階段中的見證連接狀態可以是下列值：<br /><br /> 0 = 未知<br /><br /> 1 = 已連接<br /><br /> 2 = 已中斷連接|  
|**log_generation_rate**|**int**|自從此資料庫先前的鏡像狀態更新之後產生的記錄量 (以 KB/秒為單位)。|  
|**unsent_log**|**int**|在主體的傳送佇列中未傳送之記錄的大小 (以 KB 為單位)。|  
|**send_rate**|**int**|從主體到鏡像之記錄的傳送速率 (以 KB/秒為單位)。|  
|**unrestored_log**|**int**|鏡像上的重做佇列大小 (以 KB 為單位)。|  
|**recovery_rate**|**int**|鏡像上的重做速率 (以 KB/秒為單位)。|  
|**transaction_delay**|**int**|所有交易的總延遲時間 (以毫秒為單位)。|  
|**transactions_per_sec**|**int**|主體伺服器執行個體上每秒發生的交易數。|  
|**average_delay**|**int**|由於資料庫鏡像而在主體伺服器執行個體上造成的每個交易平均延遲。 在高效能模式中 (也就是當 SAFETY 屬性設定為 OFF 時)，這個值通常是 0。|  
|**time_recorded**|**datetime**|資料庫鏡像監視器記錄資料列的時間。 這是主體的系統時間。|  
|**time_behind**|**datetime**|鏡像資料庫目前所跟上之主體的近似系統時間。 這個值只有在主體伺服器執行個體上才有意義。|  
|**local_time**|**datetime**|更新這個資料列時本機伺服器執行個體上的系統時間。|  
  
## <a name="remarks"></a>備註  
 **sp_dbmmonitorresults**可以只在內容中執行**msdb**資料庫。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定的伺服器角色或**dbm_monitor**固定的資料庫角色中**msdb**資料庫。 **Dbm_monitor**角色可讓其成員檢視資料庫鏡像狀態，但不是加以更新，但不是檢視或設定資料庫鏡像事件。  
  
> [!NOTE]  
>  第一次**sp_dbmmonitorupdate**執行時，它會建立**dbm_monitor**固定的資料庫角色中**msdb**資料庫。 成員**sysadmin**固定的伺服器角色可以新增任何使用者到**dbm_monitor**固定的資料庫角色。  
  
## <a name="examples"></a>範例  
 下列範例會傳回在前兩個小時期間記錄的資料列，而不會更新資料庫的狀態。  
  
```  
USE msdb;  
EXEC sp_dbmmonitorresults AdventureWorks2012, 2, 0;  
```  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitoraddmonitoring &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
  

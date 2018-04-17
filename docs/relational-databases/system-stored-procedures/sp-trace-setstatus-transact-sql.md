---
title: (transact-sql) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_trace_setstatus_TSQL
- sp_trace_setstatus
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setstatus
ms.assetid: 29e7a7d7-b9c1-414a-968a-fc247769750d
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a6f6aacf619df24477528b4d39ad9551be321e61
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sptracesetstatus-transact-sql"></a>sp_trace_setstatus (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改指定追蹤的目前狀態。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用擴充事件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_trace_setstatus [ @traceid = ] trace_id , [ @status = ] status  
```  
  
## <a name="arguments"></a>引數  
 [ **@traceid=** ] *trace_id*  
 這是要修改的追蹤識別碼。 *trace_id*是**int**，沒有預設值。 使用者會利用這*trace_id*值來識別、 修改和控制追蹤。 如需擷取資訊*trace_id*，請參閱[sys.fn_trace_getinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)。  
  
 [  **@status=** ]*狀態*  
 指定追蹤所實作的動作。 *狀態*是**int**，沒有預設值。  
  
 下表列出可能指定的狀態。  
  
|狀態|Description|  
|------------|-----------------|  
|**0**|停止指定的追蹤。|  
|**1**|啟動指定的追蹤。|  
|**2**|關閉指定的追蹤，並從伺服器中刪除其定義。|  
  
> [!NOTE]  
>  您必須先關閉追蹤，才能將它刪除。 您必須先停止和關閉追蹤，才能檢視它。  
  
## <a name="return-code-values"></a>傳回碼值  
 下表描述在預存程序完成之後，使用者可能得到的代碼值。  
  
|傳回碼|Description|  
|-----------------|-----------------|  
|**0**|沒有錯誤。|  
|**1**|未知的錯誤。|  
|**8**|指定的狀態無效。|  
|**9**|指定的追蹤控制代碼無效。|  
|**13**|記憶體用完。 當沒有足夠的記憶體可以執行指定的動作時，便傳回這個代碼。|  
  
 如果追蹤已處於指定狀態[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會傳回**0**。  
  
## <a name="remarks"></a>備註  
 參數的所有 SQL 追蹤預存程序 (**sp_trace_xx**) 都有強制類型。 如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。  
  
 如需使用追蹤預存程序的範例，請參閱[建立追蹤 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 使用者必須有 ALTER TRACE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.fn_trace_geteventinfo &#40;Transact SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)  
  
  

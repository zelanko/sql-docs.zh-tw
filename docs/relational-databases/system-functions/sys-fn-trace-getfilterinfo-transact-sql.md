---
title: sys.fn_trace_getfilterinfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_trace_getfilterinfo
- fn_trace_getfilterinfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], filters
- sys.fn_trace_getfilterinfo function
- filters [SQL Server], traces
- fn_trace_getfilterinfo function
ms.assetid: 09fe4a28-ff8a-4655-9da1-4654d5bc514d
caps.latest.revision: 36
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1f55c02dfd91edbb964b87e74e2d413f9066501d
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37971873"
---
# <a name="sysfntracegetfilterinfo-transact-sql"></a>sys.fn_trace_getfilterinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定追蹤所套用之篩選的相關資訊。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用擴充事件。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
fn_trace_getfilterinfo ( trace_id )  
```  
  
## <a name="arguments"></a>引數  
 *trace_id*  
 這是追蹤的識別碼。 *trace_id*已**int**，沒有預設值。  
  
## <a name="tables-returned"></a>傳回的資料表  
 傳回下列資訊。 如需有關資料行的詳細資訊，請參閱[sp_trace_setfilter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**columnid**|**int**|套用篩選之資料行的識別碼。|  
|**logical_operator**|**int**|指定套用 AND 或 OR 運算子。|  
|**comparison_operator**|**int**|指定比較類型：<br /><br /> 0 = 等於<br /><br /> 1 = 不等於<br /><br /> 2 = 大於<br /><br /> 3 = 小於<br /><br /> 4 = 大於或等於<br /><br /> 5 = 小於或等於<br /><br /> 6 = 類似<br /><br /> 7 = 不類似|  
|**value**|**sql_variant**|指定套用篩選的值。|  
  
## <a name="remarks"></a>備註  
 使用者會設定*trace_id*值來識別、 修改和控制追蹤。 在傳遞特定的追蹤識別碼**fn_trace_getfilterinfo**傳回該追蹤的任何篩選條件的相關資訊。 如果指定的追蹤沒有篩選，此函數就會傳回空的資料列集。 當傳遞無效的識別碼時，這個函數會傳回空的資料列集。 如需有關追蹤的類似資訊，請參閱[sys.fn_trace_geteventinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 ALTER TRACE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回追蹤編號 2 之所有篩選的相關資訊。  
  
```  
SELECT * FROM fn_trace_getfilterinfo(2) ;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立追蹤 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_generateevent &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys.fn_trace_geteventinfo &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [sys.fn_trace_gettable &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)  
  
  

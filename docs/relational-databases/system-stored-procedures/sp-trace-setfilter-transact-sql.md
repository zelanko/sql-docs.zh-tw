---
description: sp_trace_setfilter (Transact-SQL)
title: sp_trace_setfilter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setfilter
- sp_trace_setfilter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setfilter
ms.assetid: 11e7c7ac-a581-4a64-bb15-9272d5c1f7ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cf2b3eb0d8d71ce85ac7a5de4fddcd5a34ae97a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480973"
---
# <a name="sp_trace_setfilter-transact-sql"></a>sp_trace_setfilter (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將篩選套用在追蹤上。 **sp_trace_setfilter** 可能只會在已停止 (*狀態* 為 **0**) 的現有追蹤上執行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果此預存程式是在不存在的追蹤上執行，或其 *狀態* 不是 **0**，則會傳回錯誤。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用擴充事件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_trace_setfilter [ @traceid = ] trace_id   
          , [ @columnid = ] column_id  
          , [ @logical_operator = ] logical_operator  
          , [ @comparison_operator = ] comparison_operator  
          , [ @value = ] value  
```  
  
## <a name="arguments"></a>引數  
`[ @traceid = ] trace_id` 這是設定篩選的追蹤識別碼。 *trace_id* 是 **int**，沒有預設值。 使用者會使用這個 *trace_id* 值來識別、修改和控制追蹤。  
  
`[ @columnid = ] column_id` 這是套用篩選之資料行的識別碼。 *column_id* 是 **int**，沒有預設值。 如果 *column_id* 為 Null， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 則會清除指定追蹤的所有篩選準則。  
  
`[ @logical_operator = ] logical_operator` 指定是否套用和 (**0**) 或 (**1**) 運算子。 *logical_operator* 是 **int**，沒有預設值。  
  
`[ @comparison_operator = ] comparison_operator` 指定要進行的比較類型。 *comparison_operator* 是 **int**，沒有預設值。 這份資料表包含比較運算子及其代表值。  
  
|值|比較運算子|  
|-----------|-------------------------|  
|**0**|= (等於)|  
|**1**|<>  (不等於) |  
|**2**|> (大於)|  
|**3**|< (小於)|  
|**4**|>= (大於或等於) |  
|**5**|<= (小於或等於) |  
|**6**|LIKE|  
|**7**|不相似|  
  
`[ @value = ] value` 指定要篩選的值。 *值*的資料類型必須符合要篩選之資料行的資料類型。 例如，如果在屬於 **int** 資料類型的物件識別碼資料行上設定篩選，則 *值* 必須是 **int**。如果 *值* 為 **Nvarchar** 或 **Varbinary**，則最大長度為8000。  
  
 當比較運算子是 LIKE 或 NOT LIKE 時，邏輯運算子可以併入 "%" 或 LIKE 運算所適用的其他篩選。  
  
 您可以針對 *值* 指定 null，以篩選出具有 null 資料行值的事件。 只有 **0** (= 等於) 和 **1** ( # B0 不等於) 運算子適用于 Null。 在此情況下，這些運算子相當於 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 和 IS NOT NULL 運算子。  
  
 若要在資料行值範圍之間套用篩選， **sp_trace_setfilter** 必須執行兩次--一次是大於或等於 ( ' >= ' ) 比較運算子，另一次使用小於或等於 ( ' <= ' ) 運算子。  
  
 如需資料行資料類型的詳細資訊，請參閱 [SQL Server 事件類別參考](../../relational-databases/event-classes/sql-server-event-class-reference.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 下表描述在預存程序完成之後，使用者可能得到的代碼值。  
  
|傳回碼|描述|  
|-----------------|-----------------|  
|0|沒有錯誤。|  
|1|未知的錯誤。|  
|2|追蹤目前在執行中。 此時變更追蹤會產生錯誤。|  
|4|指定的資料行無效。|  
|5|不允許指定的資料行進行篩選。 只有 **sp_trace_setfilter**才會傳回這個值。|  
|6|指定的比較運算子無效。|  
|7|指定的邏輯運算子無效。|  
|9|指定的追蹤控制代碼無效。|  
|13|記憶體用完。 當沒有足夠的記憶體可以執行指定的動作時，便傳回這個代碼。|  
|16|函數對於這項追蹤無效。|  
  
## <a name="remarks"></a>備註  
 **sp_trace_setfilter** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程式，它會執行先前舊版中提供的擴充預存程式所執行的許多動作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 使用 **sp_trace_setfilter** 而不是 **xp_trace_set \* 篩選** 擴充預存程式，來建立、套用、移除或操作追蹤的篩選。 如需詳細資訊，請參閱 [篩選追蹤](../../relational-databases/sql-trace/filter-a-trace.md)。  
  
 特定資料行的所有篩選都必須在一次執行 **sp_trace_setfilter**時一起啟用。 例如，如果使用者想要在應用程式名稱資料行上套用兩個篩選，並在使用者名稱資料行上套用一個篩選，則使用者必須依序指定應用程式名稱的篩選。 如果使用者嘗試在一個預存程序呼叫中指定應用程式名稱的篩選，後面接著使用者名稱的篩選，以及應用程式名稱的另一個篩選，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回錯誤。  
  
 所有 SQL 追蹤預存程式 (**sp_trace_xx**) 的參數都是嚴格輸入的。 如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。  
  
## <a name="permissions"></a>權限  
 使用者必須有 ALTER TRACE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會在「追蹤 `1`」上設定三個篩選。 `N'SQLT%'` 和 `N'MS%'` 篩選會利用 "`AppName`" 比較運算子來處理一個資料行 (`10`，值是 `LIKE`)。 `N'joe'` 這個篩選利用 "`UserName`" 比較運算子來處理另一個資料行 (`11`，值是 `EQUAL`)。  
  
```  
sp_trace_setfilter  1, 10, 0, 6, N'SQLT%';  
sp_trace_setfilter  1, 10, 0, 6, N'MS%';  
sp_trace_setfilter  1, 11, 0, 0, N'joe';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys. fn_trace_getfilterinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)  
  
  

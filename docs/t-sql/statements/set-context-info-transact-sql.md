---
title: "SET CONTEXT_INFO (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_CONTEXT_INFO_TSQL
- SET CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- context information [SQL Server]
- CONTEXT_INFO option
- SET CONTEXT_INFO statement
ms.assetid: a0b7b9f3-dbda-4350-a274-bd9ecd5c0a74
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f74a45830a295467552c8fdc9f4781260339d9a6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-contextinfo-transact-sql"></a>SET CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  最多可讓 128 個位元組的二進位資訊與目前的工作階段或連接發生關聯。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET CONTEXT_INFO { binary_str | @binary_var }  
```  
  
## <a name="arguments"></a>引數  
 *binary_str*  
 是**二進位**常數或常數，它是隱含地轉換成**二進位**、 要與目前工作階段或連接產生關聯。  
  
 **@***binary_var*  
 是**varbinary**或**二進位**持有要關聯於目前的工作階段或連接的內容值的變數。  
  
## <a name="remarks"></a>備註  
 擷取目前工作階段的內容資訊，最好的方法是使用 CONTEXT_INFO 函數。 工作階段內容資訊也儲存在**context_info**下列系統檢視表中的資料行：  
  
-   **sys.dm_exec_requests**  
  
-   **sys.dm_exec_sessions**  
  
-   **sys.sysprocesses**  
  
 在使用者自訂函數中，不能指定 SET CONTEXT_INFO。 您不能提供 Null 值給 SET CONTEXT_INFO，因為存放值的檢視不接受 Null 值。  
  
 SET CONTEXT_INFO 不接受常數或變數名稱以外的運算式。 若要函式呼叫的結果集的內容資訊，您必須先包含中的函式呼叫的結果**二進位**或**varbinary**變數。  
  
 當您在預存程序或觸發程序中發出 SET CONTEXT_INFO 時，和其他 SET 陳述式不同的是，在預存程序或觸發程序完成之後，為內容資訊所設定的新值將保存下來。  
  
## <a name="examples"></a>範例  
  
### <a name="a-setting-context-information-by-using-a-constant"></a>A. 利用常數來設定內容資訊  
 下列範例會示範 `SET CONTEXT_INFO`，它將設定這個值及顯示其結果。 請注意，查詢 `sys.dm_exec_sessions` 需要 SELECT 和 VIEW SERVER STATE 權限，但使用 CONTEXT_INFO 函數便沒有這項需要。  
  
```  
SET CONTEXT_INFO 0x01010101;  
GO  
SELECT context_info   
FROM sys.dm_exec_sessions  
WHERE session_id = @@SPID;  
GO  
```  
  
### <a name="b-setting-context-information-by-using-a-function"></a>B. 利用函數來設定內容資訊  
 下列範例會示範使用函式的輸出來設定內容值，其中的值從函式必須先放置在**二進位**變數。  
  
```  
DECLARE @BinVar varbinary(128);  
SET @BinVar = CAST(REPLICATE( 0x20, 128 ) AS varbinary(128) );  
SET CONTEXT_INFO @BinVar;  
  
SELECT CONTEXT_INFO() AS MyContextInfo;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys.dm_exec_requests &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [CONTEXT_INFO &#40;TRANSACT-SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)  
  
  


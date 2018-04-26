---
title: '@@FETCH_STATUS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@FETCH_STATUS'
- '@@FETCH_STATUS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- status information [SQL Server], FETCH
- '@@FETCH_STATUS function'
ms.assetid: 93659193-e4ff-4dfb-9043-0c4114921b91
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c377058e568aef6162ecadb46bee2c2b289a6f4b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="x40x40fetchstatus-transact-sql"></a>&#x40;&#x40;FETCH_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回針對連接目前開啟的任何資料指標而發出的最後一個資料指標 FETCH 陳述式的狀態。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
@@FETCH_STATUS  
```  
  
## <a name="return-type"></a>傳回類型  
 **integer**  
  
## <a name="return-value"></a>傳回值  
  
|傳回值|描述|  
|------------------|-----------------|  
|0|FETCH 陳述式成功。|  
|-1|FETCH 陳述式失敗，或資料列已超出結果集。|  
|-2|遺漏提取的資料列。|
|-9|資料指標並未執行擷取作業。|  
  
## <a name="remarks"></a>Remarks  
 由於 @@FETCH_STATUS 在連線的所有資料指標的全域範圍內有效；因此，請小心使用 @@FETCH_STATUS。 在執行 FETCH 陳述式之後，@@FETCH_STATUS 的測試必須在針對另一個資料指標執行任何其他 FETCH 陳述式之前進行。 在連線進行任何擷取之前，並未定義 @@FETCH_STATUS 的值。  
  
 例如，使用者從一個資料指標執行 FETCH 陳述式，然後再呼叫預存程序來開啟和處理來自另一個資料指標的結果。 當控制權從所呼叫的預存程序傳回時，@@FETCH_STATUS 會反映預存程序中所執行的最後一個 FETCH，而不是在呼叫預存程序之前執行的 FETCH 陳述式。  
  
 若要擷取特定資料指標的最後一個擷取狀態，請查詢 **sys.dm_exec_cursors** 動態管理函式的 **fetch_status** 資料行。  
  
## <a name="examples"></a>範例  
 下列範例使用 `@@FETCH_STATUS` 控制 `WHILE` 迴圈中的資料指標活動。  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT BusinessEntityID, JobTitle  
FROM AdventureWorks2012.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料指標函數 &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  

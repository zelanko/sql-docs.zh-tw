---
title: "@@FETCH_STATUS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9bc4027eb6be9d79599cb06f7935bd2d052bb2a2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40fetchstatus-transact-sql"></a>&#x40;&#x40;SP_DESCRIBE_CURSOR (TRANSACT-SQL)
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
  
|傳回值|Description|  
|------------------|-----------------|  
|0|FETCH 陳述式成功。|  
|-1|FETCH 陳述式失敗，或資料列已超出結果集。|  
|-2|遺漏提取的資料列。|
|-9|資料指標提取作業無法執行。|  
  
## <a name="remarks"></a>備註  
 因為 @@FETCH_STATUS全域連接上的所有資料指標使用 @@FETCH_STATUS謹慎。 在執行 FETCH 陳述式之後，@ 測試@FETCH_STATUS必須在針對另一個資料指標執行任何其他 FETCH 陳述式之前發生。 值，@@FETCH_STATUS連接上發生任何提取之前是未定義。  
  
 例如，使用者從一個資料指標執行 FETCH 陳述式，然後再呼叫預存程序來開啟和處理來自另一個資料指標的結果。 當控制權從所呼叫的預存程序，@FETCH_STATUS反映最後一次執行預存程序不 FETCH 陳述式執行之前呼叫預存程序中的擷取。  
  
 若要擷取特定資料指標的最後一個提取狀態，請查詢**sp_describe_cursor**資料行**sys.dm_exec_cursors**動態管理函數。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [資料指標函數 &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [擷取 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  

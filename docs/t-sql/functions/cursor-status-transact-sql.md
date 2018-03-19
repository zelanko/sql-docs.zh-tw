---
title: CURSOR_STATUS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
- CURSOR_STATUS
- CURSOR_STATUS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], cursors
- CURSOR_STATUS function
- cursors [SQL Server], status information
ms.assetid: 3a4a840e-04f8-43bd-aada-35d78c3cb6b0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 59a2cd382855f47d7cb37a3bc00bc723dde8f6df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="cursorstatus-transact-sql"></a>CURSOR_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

可讓預存程序的呼叫端判斷程序是否已傳回給定參數之資料指標和結果集的純量函數。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CURSOR_STATUS   
     (  
          { 'local' , 'cursor_name' }   
          | { 'global' , 'cursor_name' }   
          | { 'variable' , 'cursor_variable' }   
     )  
```  
  
## <a name="arguments"></a>引數  
'local'  
指定一個常數來指示資料指標的來源是本機資料指標名稱。
  
'*cursor_name*'  
這是資料指標的名稱。 資料指標名稱必須符合識別碼的規則。
  
'global'  
指定一個常數來指示資料指標的來源是全域資料指標名稱。
  
'variable'  
指定一個常數來指示資料指標的來源是本機變數。
  
'*cursor_variable*'  
這是資料指標變數的名稱。 您必須使用 **cursor** 資料類型來定義資料指標變數。
  
## <a name="return-types"></a>傳回型別
**smallint**
  
|傳回值|資料指標名稱|資料指標變數|  
|---|---|---|
|@shouldalert|資料指標的結果集至少有一個資料列。<br /><br /> 非機密資料指標和索引鍵集資料指標，其結果集至少有一個資料列。<br /><br /> 動態資料指標的結果集可以有零、一或多個資料列。|配置給這個變數的資料指標是開啟的。<br /><br /> 非機密資料指標和索引鍵集資料指標，其結果集至少有一個資料列。<br /><br /> 動態資料指標的結果集可以有零、一或多個資料列。|  
|0|資料指標的結果集是空的。*|配置給這個變數的資料指標是開啟的，但結果集確定空白。*|  
|-1|資料指標已關閉。|配置給這個變數的資料指標已關閉。|  
|-2|不適用。|可為以下項目：<br /><br /> 先前呼叫的程序未指派任何資料指標給這個 OUTPUT 變數。<br /><br /> 先前呼叫的程序指派一個資料指標給這個 OUTPUT 變數，但程序完成時，這個資料指標在關閉狀態中。 因此，這個資料指標已取消配置，並未傳回給發出呼叫的程序。<br /><br /> 沒有指派給宣告的資料指標變數之資料指標。|  
|-3|含指定名稱的資料指標不存在。|含指定名稱的資料指標變數不存在，或這個變數存在，但還沒有配置資料指標。|  
  
*動態資料指標永遠不會傳回這個結果。
  
## <a name="examples"></a>範例  
下列範例會利用 `CURSOR_STATUS` 函數來顯示資料指標在開啟和關閉前後的狀態。
  
```sql
CREATE TABLE #TMP  
(  
   ii int  
)  
GO  
  
INSERT INTO #TMP(ii) VALUES(1)  
INSERT INTO #TMP(ii) VALUES(2)  
INSERT INTO #TMP(ii) VALUES(3)  
  
GO  
  
--Create a cursor.  
DECLARE cur CURSOR  
FOR SELECT * FROM #TMP  
  
--Display the status of the cursor before and after opening  
--closing the cursor.  
  
SELECT CURSOR_STATUS('global','cur') AS 'After declare'  
OPEN cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Open'  
CLOSE cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Close'  
  
--Remove the cursor.  
DEALLOCATE cur  
  
--Drop the table.  
DROP TABLE #TMP  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
After declare
---------------
-1  
  
After Open
----------
1  
  
After Close
-----------
-1
```  
  
## <a name="see-also"></a>另請參閱
[資料指標函式 &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

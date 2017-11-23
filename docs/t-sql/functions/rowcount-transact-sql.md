---
title: "@@ROWCOUNT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@ROWCOUNT_TSQL'
- '@@ROWCOUNT'
dev_langs: TSQL
helpviewer_keywords:
- '@@ROWCOUNT function'
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 97a47998-81d9-4331-a244-9eb8b6fe4a56
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: dd23d2af2f35dd0d76557723639f1870ee22e0ee
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40rowcount-transact-sql"></a>&#x40;&#x40;ROWCOUNT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回受到前一個陳述式所影響的資料列數。 如果資料列數目超過 2 億，請使用[ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@ROWCOUNT  
```  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式可以設定中的值，@@ROWCOUNT如下：  
  
-   Set @@ROWCOUNT的資料列數目會受到影響或讀取。 資料列不一定會傳送到用戶端。  
  
-   保留@ROWCOUNT從上一個陳述式執行。  
  
-   重設@ROWCOUNT設為 0，但不是會傳回值給用戶端。  
  
 請永遠設定為簡單指派的陳述式 @@ROWCOUNT值設為 1。 它不會傳送任何資料列給用戶端。 這些陳述式的範例包括： SET @*local_variable*、 RETURN、 READTEXT 以及 select without query 如 SELECT getdate （） 或選取的陳述式**'***一般文字***'**.  
  
 陳述式，在查詢中進行指派，或在 查詢設定中使用 RETURN @@ROWCOUNT值的資料列數目受到影響或讀取查詢，例如： SELECT @*local_variable* = c1 FROM t1。  
  
 資料操作語言 (DML) 陳述式會設定 @@ROWCOUNT值的查詢所影響的資料列數目，並且將該值傳回給用戶端。 DML 陳述式可能不會傳送任何資料列給用戶端。  
  
 DECLARE CURSOR 和 FETCH 設定 @@ROWCOUNT值設為 1。  
  
 EXECUTE 陳述式會保留上一個 @@ROWCOUNT。  
  
 陳述式使用時，例如設定\<選項 >、 DEALLOCATE CURSOR、 CLOSE CURSOR、 BEGIN TRANSACTION，或認可的交易重設為 0 的資料列計數值。  
  
 原生編譯的預存程序會保留上一個 @@ROWCOUNT。 [!INCLUDE[tsql](../../includes/tsql-md.md)]原生編譯的預存程序內的陳述式未設定@ROWCOUNT。 如需詳細資訊，請參閱[Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)。  
  
## <a name="examples"></a>範例  
 下列範例會執行 `UPDATE` 陳述式，並且使用 `@@ROWCOUNT` 來偵測是否有任何資料列變更。  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee   
SET JobTitle = N'Executive'  
WHERE NationalIDNumber = 123456789  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were updated';  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [SET ROWCOUNT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  

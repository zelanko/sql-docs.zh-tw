---
title: "取消配置 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DEALLOCATE
- DEALLOCATE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- locking [SQL Server], cursors
- DEALLOCATE statement
- deallocations [SQL Server]
- deleting cursor references
- removing cursor references
ms.assetid: c75cf73d-0268-4c57-973d-b8a84ff801fa
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fb05fdd9da2f4f724976092bf027f5dde5edd412
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="deallocate-transact-sql"></a>DEALLOCATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  移除資料指標參考。 當取消配置最後一個資料指標參考時，會釋放組成資料指標的資料結構[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DEALLOCATE { { [ GLOBAL ] cursor_name } | @cursor_variable_name }  
```  
  
## <a name="arguments"></a>引數  
 *cursor_name*  
 這是已宣告的資料指標名稱。 如果全域和本機資料指標同時存在與*cursor_name*做為其名稱， *cursor_name*參考全域資料指標，否則指定全域和本機資料指標，如果未指定 GLOBAL。  
  
 @*cursor_variable_name*  
 名稱**游標**變數。 @*cursor_variable_name*必須是型別**游標**。  
  
## <a name="remarks"></a>備註  
 處理資料指標的陳述式會利用資料指標名稱或資料指標變數來參考資料指標。 DEALLOCATE 會移除資料指標和資料指標名稱或資料指標變數之間的關聯。 如果名稱或變數是最後一個參考資料指標的項目，就會取消配置資料指標，釋出資料指標所用的任何資源。 在 DEALLOCATE 時，會釋出用來保護提取隔離的捲動鎖定。 用來保護更新 (其中包括透過資料指標所進行的定位更新) 的交易鎖定，會保留到交易結束時。  
  
 DECLARE CURSOR 陳述式會配置資料指標，將資料指標關聯於資料指標名稱。  
  
```  
DECLARE abc SCROLL CURSOR FOR  
SELECT * FROM Person.Person;  
```  
  
 在資料指標名稱關聯於資料指標之後，直到取消配置這個資料指標之前，相同範圍 (GLOBAL 或 LOCAL) 的其他資料指標不能使用這個名稱。  
  
 資料指標變數會利用兩種方法之一來關聯於資料指標：  
  
-   依名稱，利用 SET 陳述式將資料指標設為資料指標變數。  
  
    ```  
    DECLARE @MyCrsrRef CURSOR;  
    SET @MyCrsrRef = abc;  
    ```  
  
-   不需要定義資料指標名稱，也可以建立資料指標以及將資料指標與變數產生關聯。  
  
    ```  
    DECLARE @MyCursor CURSOR;  
    SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Person.Person;  
    ```  
  
 DEALLOCATE @*cursor_variable_name*陳述式只會移除參考的具名變數至游標處。 要等到批次、預存程序或觸發程序結束而離開範圍之後，此變數才會取消配置。 在 DEALLOCATE @ 之後*cursor_variable_name*陳述式，此變數可與相關聯使用 SET 陳述式的另一個資料指標。  
  
```  
USE AdventureWorks2012;  
GO  
  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
  
DEALLOCATE @MyCursor;  
  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesTerritory;  
GO  
```  
  
 您不需要明確取消配置資料指標變數。 當變數離開範圍時，會隱含地取消配置。  
  
## <a name="permissions"></a>Permissions  
 DEALLOCATE 權限預設會授與任何有效的使用者。  
  
## <a name="examples"></a>範例  
 下列指令碼會顯示資料指標如何保存，直到最後一個名稱或參考這些資料指標的變數取消配置為止。  
  
```  
USE AdventureWorks2012;  
GO  
-- Create and open a global named cursor that  
-- is visible outside the batch.  
DECLARE abc CURSOR GLOBAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
OPEN abc;  
GO  
-- Reference the named cursor with a cursor variable.  
DECLARE @MyCrsrRef1 CURSOR;  
SET @MyCrsrRef1 = abc;  
-- Now deallocate the cursor reference.  
DEALLOCATE @MyCrsrRef1;  
-- Cursor abc still exists.  
FETCH NEXT FROM abc;  
GO  
-- Reference the named cursor again.  
DECLARE @MyCrsrRef2 CURSOR;  
SET @MyCrsrRef2 = abc;  
-- Now deallocate cursor name abc.  
DEALLOCATE abc;  
-- Cursor still exists, referenced by @MyCrsrRef2.  
FETCH NEXT FROM @MyCrsrRef2;  
-- Cursor finally is deallocated when last referencing  
-- variable goes out of scope at the end of the batch.  
GO  
-- Create an unnamed cursor.  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
SELECT * FROM Sales.SalesTerritory;  
-- The following statement deallocates the cursor  
-- because no other variables reference it.  
DEALLOCATE @MyCursor;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [資料指標](../../relational-databases/cursors.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [擷取 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [開啟 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  

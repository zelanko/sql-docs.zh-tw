---
title: "擷取 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FETCH
- FETCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- cursors [SQL Server], fetching
- Transact-SQL cursors, fetching and scrolling
- retrieving rows
- fetching [SQL Server]
- SCROLL option
- row fetching [SQL Server]
ms.assetid: 5d68dac2-f91b-4342-bb4e-209ee132665f
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1333af6ceba4a4410fefadd1a99d8611fae88a6a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="fetch-transact-sql"></a>FETCH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器資料指標中，擷取特定資料列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
FETCH   
          [ [ NEXT | PRIOR | FIRST | LAST   
                    | ABSOLUTE { n | @nvar }   
                    | RELATIVE { n | @nvar }   
               ]   
               FROM   
          ]   
{ { [ GLOBAL ] cursor_name } | @cursor_variable_name }   
[ INTO @variable_name [ ,...n ] ]   
```  
  
## <a name="arguments"></a>引數  
 NEXT  
 在目前資料列之後立即傳回結果資料列，並將目前資料列遞增到傳回的資料列。 如果 FETCH NEXT 是針對資料指標的第一項提取，它會傳回結果集中的第一個資料列。 NEXT 是預設資料指標提取選項。  
  
 PRIOR  
 傳回結果資料列之後立即傳回目前資料列，並將目前資料列減量到傳回的資料列。 如果 FETCH PRIOR 是針對資料指標的第一項提取，就不會傳回任何資料列，而且資料指標的位置會保持在第一個資料列之前。  
  
 FIRST  
 傳回資料指標中的第一個資料列，使它成為目前資料列。  
  
 LAST  
 傳回資料指標中的最後一個資料列，使它成為目前資料列。  
  
 絕對 {  *n* | @*nvar*}  
 如果 *n* 或 @*nvar*是正數，傳回的資料列 *n* 個資料列從資料指標前端，使傳回的資料列成為新的目前資料列。 如果 *n* 或 @*nvar*是負數，傳回的資料列 *n* 個資料列資料指標結尾之前，使傳回的資料列成為新的目前資料列。 如果 *n* 或 @*nvar*是 0，會傳回任何資料列。 *n*必須是整數常數和 @*nvar*必須**smallint**， **tinyint**，或**int**。  
  
 相對 {  *n* | @*nvar*}  
 如果 *n* 或 @*nvar*是正數，傳回的資料列 *n* 個資料列目前資料列之後，使傳回的資料列成為新的目前資料列。 如果 *n* 或 @*nvar*是負數，傳回的資料列 *n* 個資料列目前資料列之前，使傳回的資料列成為新的目前資料列。 如果 *n* 或 @*nvar*是 0，則會傳回目前的資料列。 如果指定 FETCH RELATIVE 是 *n* 或 @*nvar*設為負數或 0，針對資料指標執行的第一項提取上，會傳回任何資料列。 *n*必須是整數常數和 @*nvar*必須**smallint**， **tinyint**，或**int**。  
  
 GLOBAL  
 指定*cursor_name*參考全域資料指標。  
  
 *cursor_name*  
 這是應該從中提取的開啟資料指標名稱。 如果全域和本機資料指標同時存在與*cursor_name*做為其名稱， *cursor_name*全域資料指標，否則指定全域和本機資料指標，如果未指定 GLOBAL。  
  
 @*cursor_variable_name*  
 這是資料指標變數的名稱，這個資料指標參考應該從中提取的開啟資料指標。  
  
 @ INTO*variable_name*[，...*n*]  
 可讓提取的資料行資料放在本機變數中。 清單中的各個變數會由左至右，依次與資料指標結果集中對應的資料行相關。 每個變數的資料類型都必須符合對應結果集資料行的資料類型，或必須是支援的對應結果集資料行的資料類型之隱含轉換。 變數的數目必須符合資料指標選取清單中的資料行數目。  
  
## <a name="remarks"></a>備註  
 如果 ISO 樣式 DECLARE CURSOR 陳述式並未指定 SCROLL 選項，NEXT 就是唯一支援的 FETCH 選項。 如果在 ISO 樣式 DECLARE CURSOR 中指定了 SCROLL，便支援所有 FETCH 選項。  
  
 當使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DECLARE 資料指標延伸模組時，適用下列規則：  
  
-   如果指定了 FORWARD_ONLY 或 FAST_FORWARD，NEXT 便是唯一支援的 FETCH 選項。  
  
-   如果未指定 DYNAMIC、FORWARD_ONLY 或 FAST_FORWARD，且指定了 KEYSET、STATIC 或 SCROLL，便會支援所有 FETCH 選項。  
  
-   DYNAMIC SCROLL 資料指標支援 ABSOLUTE 以外的所有 FETCH 選項。  
  
 @@FETCH_STATUS函式會報告最後一個 FETCH 陳述式的狀態。 相同的資訊記錄在 sp_describe_cursor 傳回之資料指標的 fetch_status 資料行中。 試圖在 FETCH 陳述式傳回的資料上執行任何作業之前，您應該先利用這個狀態資訊來判斷這項資料是否有效。 如需詳細資訊，請參閱[@@FETCH_STATUS &#40;TRANSACT-SQL &#41;](../../t-sql/functions/fetch-status-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 FETCH 權限預設會授與任何有效的使用者。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-fetch-in-a-simple-cursor"></a>A. 在簡單資料指標中使用 FETCH  
 這個範例會宣告 `Person.Person` 資料表中，各個姓氏開頭是 `B` 之資料列的簡單資料指標，且利用 `FETCH NEXT` 來逐步執行各個資料列。 `FETCH` 陳述式會在單一資料列結果集中，傳回 `DECLARE CURSOR` 所指定之資料行的值。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE contact_cursor CURSOR FOR  
SELECT LastName FROM Person.Person  
WHERE LastName LIKE 'B%'  
ORDER BY LastName;  
  
OPEN contact_cursor;  
  
-- Perform the first fetch.  
FETCH NEXT FROM contact_cursor;  
  
-- Check @@FETCH_STATUS to see if there are any more rows to fetch.  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   -- This is executed as long as the previous fetch succeeds.  
   FETCH NEXT FROM contact_cursor;  
END  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
### <a name="b-using-fetch-to-store-values-in-variables"></a>B. 利用 FETCH 將值儲存在變數中  
 下列範例類似於範例 A，不過，`FETCH` 陳述式的輸出是儲存在本機變數中，而不是直接傳回給用戶端。 `PRINT` 陳述式將各個變數組成單一字串，再將它們傳回用戶端。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare the variables to store the values returned by FETCH.  
DECLARE @LastName varchar(50), @FirstName varchar(50);  
  
DECLARE contact_cursor CURSOR FOR  
SELECT LastName, FirstName FROM Person.Person  
WHERE LastName LIKE 'B%'  
ORDER BY LastName, FirstName;  
  
OPEN contact_cursor;  
  
-- Perform the first fetch and store the values in variables.  
-- Note: The variables are in the same order as the columns  
-- in the SELECT statement.   
  
FETCH NEXT FROM contact_cursor  
INTO @LastName, @FirstName;  
  
-- Check @@FETCH_STATUS to see if there are any more rows to fetch.  
WHILE @@FETCH_STATUS = 0  
BEGIN  
  
   -- Concatenate and display the current values in the variables.  
   PRINT 'Contact Name: ' + @FirstName + ' ' +  @LastName  
  
   -- This is executed as long as the previous fetch succeeds.  
   FETCH NEXT FROM contact_cursor  
   INTO @LastName, @FirstName;  
END  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
### <a name="c-declaring-a-scroll-cursor-and-using-the-other-fetch-options"></a>C. 宣告 SCROLL 資料指標及使用其他 FETCH 選項  
 下列範例會建立一個 `SCROLL` 資料指標，允許使用 `LAST`、`PRIOR`、`RELATIVE` 和 `ABSOLUTE` 選項的完整捲動功能。  
  
```  
USE AdventureWorks2012;  
GO  
-- Execute the SELECT statement alone to show the   
-- full result set that is used by the cursor.  
SELECT LastName, FirstName FROM Person.Person  
ORDER BY LastName, FirstName;  
  
-- Declare the cursor.  
DECLARE contact_cursor SCROLL CURSOR FOR  
SELECT LastName, FirstName FROM Person.Person  
ORDER BY LastName, FirstName;  
  
OPEN contact_cursor;  
  
-- Fetch the last row in the cursor.  
FETCH LAST FROM contact_cursor;  
  
-- Fetch the row immediately prior to the current row in the cursor.  
FETCH PRIOR FROM contact_cursor;  
  
-- Fetch the second row in the cursor.  
FETCH ABSOLUTE 2 FROM contact_cursor;  
  
-- Fetch the row that is three rows after the current row.  
FETCH RELATIVE 3 FROM contact_cursor;  
  
-- Fetch the row that is two rows prior to the current row.  
FETCH RELATIVE -2 FROM contact_cursor;  
  
CLOSE contact_cursor;  
DEALLOCATE contact_cursor;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [關閉 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [解除配置 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [開啟 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  

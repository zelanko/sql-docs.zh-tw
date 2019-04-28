---
title: sp_cursor_list (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_list
- sp_cursor_list_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_list
ms.assetid: 7187cfbe-d4d9-4cfa-a3bb-96a544c7c883
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8c6cef14177e871f35ccd5c84af4a2b28e35aff5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724043"
---
# <a name="spcursorlist-transact-sql"></a>sp_cursor_list (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告連接目前所開啟之伺服器資料指標的屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursor_list [ @cursor_return = ] cursor_variable_name OUTPUT   
     , [ @cursor_scope = ] cursor_scope  
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ @cursor_return= ] *cursor_variable_name*OUTPUT  
 這是宣告資料指標變數的名稱。 *cursor_variable_name*已**游標**，沒有預設值。 資料指標是一個可捲動的動態唯讀資料指標。  
  
 [ @cursor_scope= ] *cursor_scope*  
 指定要報告的資料指標層級。 *cursor_scope&lt*已**int**，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|1|報告所有本機資料指標。|  
|2|報告所有全域資料指標。|  
|3|報告本機和全域資料指標。|  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="cursors-returned"></a>傳回的資料指標  
 sp_cursor_list 會將它的報表當作一個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料指標輸出參數傳回，而不是作為一份結果集傳回。 這會使 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次、預存程序和觸發程序能夠使用輸出，每次一個資料列。 另外，它也表示無法直接從資料庫 API 函數呼叫程序。 cursor 輸出參數必須繫結於程式變數，但資料庫 API 並不支援繫結資料指標參數或變數。  
  
 這是 sp_cursor_list 所傳回的資料指標格式。 資料指標的格式與 sp_describe_cursor 所傳回的格式相同。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|用來參考資料指標的名稱。 如果是利用 DECLARE CURSOR 陳述式所提供的名稱來參考資料指標，參考名稱就與資料指標名稱相同。 如果是利用變數來參考資料指標，參考名稱就是資料指標變數的名稱。|  
|cursor_name|**sysname**|DECLARE CURSOR 陳述式的資料指標名稱。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，如果資料指標是透過資料指標，設定資料指標變數**cursor_name**傳回資料指標變數的名稱。  在舊版中，這個輸出資料行會傳回系統產生的名稱。|  
|cursor_scope|**smallint**|1 = LOCAL <br /><br /> 2 = GLOBAL|  
|status|**smallint**|與 CURSOR_STATUS 系統函數所報告相同的值：<br /><br /> 1 = 資料指標名稱或變數所參考的資料指標是開啟的。 如果資料指標是不區分、靜態或索引鍵集，它至少會有一個資料列。 如果資料指標是動態的，結果集就會有零或多個資料列。<br /><br /> 0 = 資料指標名稱或變數所參考的資料指標是開啟的，但沒有資料列。 動態資料指標永不傳回這個值。<br /><br /> -1 = 資料指標名稱或變數所參考的資料指標是關閉的。<br /><br /> -2 = 只適用於資料指標變數。 沒有指派給變數的資料指標。 可能是 OUTPUT 參數將資料指標指派給變數，但傳回之前，預存程序便關閉了資料指標。<br /><br /> -3 = 含指定名稱的資料指標或資料指標變數不存在，或資料指標變數還沒有配置資料指標。|  
|model|**smallint**|1 = 不區分 (或靜態)<br /><br /> 2 = 索引鍵集<br /><br /> 3 = 動態<br /><br /> 4 = 向前快轉|  
|並行 (concurrency)|**smallint**|1 = 唯讀<br /><br /> 2 = 捲動鎖定<br /><br /> 3 = 開放式|  
|scrollable|**smallint**|0 = 順向<br /><br /> 1 = 可捲動|  
|open_status|**smallint**|0 = 已關閉<br /><br /> 1 = 開啟|  
|cursor_rows|**int**|結果集中符合的資料列數目。 如需詳細資訊，請參閱 < [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)。|  
|fetch_status|**smallint**|這個資料指標上次提取的狀態。 如需詳細資訊，請參閱 < [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md):<br /><br /> 0 = 順利提取。<br /><br /> -1 = 提取失敗，或超出資料指標界限。<br /><br /> -2 = 遺漏要求的資料列。<br /><br /> -9 = 資料指標尚無任何提取動作。|  
|column_count|**smallint**|資料指標結果集中的資料行數目。|  
|row_count|**smallint**|資料指標上次作業所影響的資料列數。 如需詳細資訊，請參閱 < [@@ROWCOUNT](../../t-sql/functions/rowcount-transact-sql.md)。|  
|last_operation|**smallint**|上次在資料指標上執行的作業：<br /><br /> 0 = 未在資料指標上執行任何作業。<br /><br /> 1 = OPEN<br /><br /> 2 = FETCH<br /><br /> 3 = 插入<br /><br /> 4 = UPDATE<br /><br /> 5 = DELETE<br /><br /> 6 = CLOSE<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|在伺服器範圍內用來識別資料指標的唯一值。|  
  
## <a name="remarks"></a>備註  
 sp_cursor_list 會產生一份連接所開啟的目前伺服器資料指標清單，且會描述每個資料指標的全域屬性，如資料指標是否可以捲動及更新。 sp_cursor_list 所列出的資料指標包括：  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器資料指標。  
  
-   API 伺服器資料指標稱為 SQLSetCursorName 資料指標名稱，ODBC 應用程式開啟。  
  
 請利用 sp_describe_cursor_columns 來取得資料指標所傳回之結果集的屬性描述。 請利用 sp_describe_cursor_tables 來取得資料指標所參考之基底資料表的報表。 sp_describe_cursor 會報告與 sp_cursor_list，但只針對指定的資料指標的相同資訊。  
  
## <a name="permissions"></a>Permissions  
 執行權限預設會授與給 public 角色。  
  
## <a name="examples"></a>範例  
 下列範例會開啟一個全域資料指標，且會利用 `sp_cursor_list` 來報告資料指標的屬性。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a keyset-driven cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_cursor_list.  
DECLARE @Report CURSOR;  
  
-- Execute sp_cursor_list into the cursor variable.  
EXEC master.dbo.sp_cursor_list @cursor_return = @Report OUTPUT,  
      @cursor_scope = 2;  
  
-- Fetch all the rows from the sp_cursor_list output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_cursor_list.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

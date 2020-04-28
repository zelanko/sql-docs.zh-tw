---
title: sp_describe_cursor_columns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor_columns
- sp_describe_cursor_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor_columns
ms.assetid: 6eaa54af-7ba4-4fce-bf6c-6ac67cc1ac94
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1dffb53a2b6436725a2b7dc19dfb209a58b1134e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68053118"
---
# <a name="sp_describe_cursor_columns-transact-sql"></a>sp_describe_cursor_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告伺服器資料指標結果集中之資料行的屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_describe_cursor_columns   
   [ @cursor_return = ] output_cursor_variable OUTPUT   
    { [ , [ @cursor_source = ] N'local' ,   
          [ @cursor_identity = ] N'local_cursor_name' ]   
    | [ , [ @cursor_source = ] N'global' ,   
          [ @cursor_identity = ] N'global_cursor_name' ]   
    | [ , [ @cursor_source = ] N'variable' ,   
          [ @cursor_identity = ] N'input_cursor_variable' ]   
   }  
```  
  
## <a name="arguments"></a>引數  
 [ @cursor_return= ]*output_cursor_variable*輸出  
 這是用來接收資料指標輸出之宣告資料指標變數的名稱。 *output_cursor_variable*是**cursor**，沒有預設值，而且在呼叫 sp_describe_cursor_columns 時，不能與任何資料指標產生關聯。 傳回的資料指標是一個可捲動的動態唯讀資料指標。  
  
 [ @cursor_source= ]{N'local ' |N'global ' |N'variable' }  
 指定報告的資料指標是利用本機資料指標、全域資料指標或資料指標變數的名稱來指定。 參數是**Nvarchar （30）**。  
  
 [ @cursor_identity= ]N '*local_cursor_name*'  
 這是具有 LOCAL 關鍵字或預設為 LOCAL 之 DECLARE CURSOR 陳述式所建立的資料指標名稱。 *local_cursor_name*為**Nvarchar （128）**。  
  
 [ @cursor_identity= ]N '*global_cursor_name*'  
 這是具有 GLOBAL 關鍵字或預設為 GLOBAL 的 DECLARE CURSOR 陳述式所建立之資料指標的名稱。 *global_cursor_name*為**Nvarchar （128）**。  
  
 *global_cursor_name*也可以是 ODBC 應用程式所開啟，然後藉由呼叫 SQLSetCursorName 來命名之 API 伺服器資料指標的名稱。  
  
 [ @cursor_identity= ]N '*input_cursor_variable*'  
 這是與開啟的資料指標相關聯的資料指標變數名稱。 *input_cursor_variable*為**Nvarchar （128）**。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="cursors-returned"></a>傳回的資料指標  
 sp_describe_cursor_columns 會將[!INCLUDE[tsql](../../includes/tsql-md.md)]其報表封裝為數據**指標**輸出參數。 這樣 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次、預存程序和觸發程序就能夠一次處理一個資料列的輸出。 另外，這也表示無法直接從資料庫 API 函數呼叫程序。 **Cursor** output 參數必須系結至程式變數，但資料庫 api 並不支援系結資料**指標**參數或變數。  
  
 下表顯示利用 sp_describe_cursor_columns 所傳回的資料指標格式。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|column_name|**sysname** （可為 null）|指派給結果集資料行的名稱。 如果指定這個資料行時未使用隨附的 AS 子句，這個資料行就是 NULL。|  
|ordinal_position|**int**|從結果集最左側資料行開始的資料行相對位置。 第一個資料行在位置 0。|  
|column_characteristics_flags|**int**|指示 OLE DB 的 DBCOLUMNFLAGS 中所儲存之資訊的位元遮罩。 它可以是下列中的任何項目或項目組合：<br /><br /> 1 = 書籤<br /><br /> 2 = 固定長度<br /><br /> 4 = 可為 Null<br /><br /> 8 = 資料列版本設定<br /><br /> 16 = 可更新資料行 (針對沒有 FOR UPDATE 子句的資料指標之預計資料行來設定，如果有這種資料行，每個資料指標只能有一個這種資料行)。<br /><br /> 當組合位元值時，適用組合之位元值的特性。 例如，如果位元值是 6，資料行便是固定長度 (2) 且可為 Null (4) 的資料行。|  
|column_size|**int**|這個資料行中的值之最大可能大小。|  
|data_type_sql|**smallint**|指出資料行之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的號碼。|  
|column_precision|**tinyint**|依據 OLE DB 中的*bPrecision*值，資料行的最大有效位數。|  
|column_scale|**tinyint**|**數值**或**十進位**資料類型小數點右邊的位數，依據 OLE DB 中的*bScale*值。|  
|order_position|**int**|如果資料行參與結果集的排序，資料行在排序索引鍵中的位置是相對於最左側的資料行。|  
|order_direction|**Varchar （1）**（nullable）|A = 資料行在排序索引鍵中，採遞增排序。<br /><br /> D = 資料行在排序索引鍵中，採遞減排序。<br /><br /> NULL = 資料行不參與排序。|  
|hidden_column|**smallint**|0 = 這個資料行出現在選取清單中。<br /><br /> 1 = 保留供日後使用。|  
|columnid|**int**|基底資料行的資料行識別碼。 如果結果集資料行是運算式所建立的，columnid 便是 -1。|  
|objectid|**int**|提供資料行之物件或基底資料表的物件識別碼。 如果結果集資料行是運算式所建立的，objectid 便是 -1。|  
|dbid|**int**|提供資料行的基底資料表所在之資料庫的識別碼。 如果結果集資料行是運算式所建立的，dbid 便是 -1。|  
|dbname|**sysname**<br /><br /> (可為 Null)|提供資料行的基底資料表所在的資料庫名稱。 如果結果集資料行是運算式所建立的，dbname 便是 NULL。|  
  
## <a name="remarks"></a>備註  
 sp_describe_cursor_columns 會描述伺服器資料指標結果集中之資料行的屬性，如每個資料指標的名稱和資料類型。 請將 sp_describe_cursor 用於伺服器資料指標之全域屬性的描述中。 請利用 sp_describe_cursor_tables 來取得資料指標所參考之基底資料表的報表。 若要取得連接上可見的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器資料指標的報表，請使用 sp_cursor_list。  
  
## <a name="permissions"></a>權限  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會開啟一個全域資料指標，且會利用 `sp_describe_cursor_columns` 來報告資料指標中所用的資料行。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person;  
GO  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_columns.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_columns into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_columns  
    @cursor_return = @Report OUTPUT  
    ,@cursor_source = N'global'   
    ,@cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_columns output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_columns.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [連筆](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40;Transact-sql&#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-sql&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_describe_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [sp_cursor_list &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor_tables &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

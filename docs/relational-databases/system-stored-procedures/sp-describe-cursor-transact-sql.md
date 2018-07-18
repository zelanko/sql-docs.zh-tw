---
title: sp_describe_cursor (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor
- sp_describe_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor
ms.assetid: 0c836c99-1147-441e-998c-f0a30cd05275
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 72278631cebc617666317df77fd62e28442b9706
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260644"
---
# <a name="spdescribecursor-transact-sql"></a>sp_describe_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告伺服器資料指標的屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_describe_cursor [ @cursor_return = ] output_cursor_variable OUTPUT   
     { [ , [ @cursor_source = ] N'local'  
    , [ @cursor_identity = ] N'local_cursor_name' ]   
   | [ , [ @cursor_source = ] N'global'  
    , [ @cursor_identity = ] N'global_cursor_name' ]   
   | [ , [ @cursor_source = ] N'variable'  
     , [ @cursor_identity = ] N'input_cursor_variable' ]   
     }   
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ @cursor_return=] *output_cursor_variable*輸出  
 這是用來接收資料指標輸出之宣告資料指標變數的名稱。 *output_cursor_variable*是**游標**，沒有預設值，而且必須在不能有相關聯的任何資料指標呼叫 sp_describe_cursor 時的時間。 傳回的資料指標是一個可捲動的動態唯讀資料指標。  
  
 [ @cursor_source=] {N'local' |N'global' |N'variable'}  
 指定報告的資料指標是利用本機資料指標、全域資料指標或資料指標變數的名稱來指定。 參數是**nvarchar （30)**。  
  
 [ @cursor_identity=] N'*local_cursor_name*']  
 這是具有 LOCAL 關鍵字或預設為 LOCAL 之 DECLARE CURSOR 陳述式所建立的資料指標名稱。 *local_cursor_name*是**nvarchar （128)**。  
  
 [ @cursor_identity=] N'*global_cursor_name*']  
 這是具有 GLOBAL 關鍵字或預設為 GLOBAL 的 DECLARE CURSOR 陳述式所建立之資料指標的名稱。 *global_cursor_name*是**nvarchar （128)**。  
  
 *global_cursor_name*也可以開啟接著是具名的 ODBC 應用程式之 API 伺服器資料指標名稱藉由呼叫 SQLSetCursorName。  
  
 [ @cursor_identity=] N'*input_cursor_variable*']  
 這是與開啟的資料指標相關聯的資料指標變數名稱。 *input_cursor_variable*是**nvarchar （128)**。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="cursors-returned"></a>傳回的資料指標  
 sp_describe_cursor 封裝其結果集[!INCLUDE[tsql](../../includes/tsql-md.md)]**游標**輸出參數。 這樣 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次、預存程序和觸發程序就能夠一次處理一個資料列的輸出。 另外，這也表示無法直接從資料庫 API 函數呼叫程序。 **游標**輸出參數必須繫結至程式變數，但資料庫 Api 不支援繫結**游標**參數或變數。  
  
 下表顯示利用 sp_describe_cursor 所傳回的資料指標格式。 資料指標的格式與利用 sp_cursor_list 所傳回的格式相同。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|reference_name|**sysname**|用來參考資料指標的名稱。 如果是利用 DECLARE CURSOR 陳述式所指定的名稱來參考資料指標，參考名稱就與資料指標名稱相同。 如果是利用變數來參考資料指標，參考名稱就是變數的名稱。|  
|cursor_name|**sysname**|DECLARE CURSOR 陳述式的資料指標名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果是設定指向資料指標的資料指標變數來建立資料指標，cursor_name 就會傳回資料指標變數的名稱。 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個輸出資料行會傳回系統產生的名稱。|  
|cursor_scope|**tinyint**|1 = LOCAL <br /><br /> 2 = GLOBAL|  
|status|**int**|與 CURSOR_STATUS 系統函數所報告相同的值：<br /><br /> 1 = 資料指標名稱或變數所參考的資料指標是開啟的。 如果資料指標是不區分、靜態或索引鍵集，它至少會有一個資料列。 如果資料指標是動態的，結果集就會有零或多個資料列。<br /><br /> 0 = 資料指標名稱或變數所參考的資料指標是開啟的，但沒有資料列。 動態資料指標永不傳回這個值。<br /><br /> -1 = 資料指標名稱或變數所參考的資料指標是關閉的。<br /><br /> -2 = 只適用於資料指標變數。 沒有指派給變數的資料指標。 可能是 OUTPUT 參數將資料指標指派給變數，但傳回之前，預存程序便關閉了資料指標。<br /><br /> -3 = 含指定名稱的資料指標或資料指標變數不存在，或資料指標變數還沒有配置資料指標。|  
|model|**tinyint**|1 = 不區分 (或靜態)<br /><br /> 2 = 索引鍵集<br /><br /> 3 = 動態<br /><br /> 4 = 向前快轉|  
|並行 (concurrency)|**tinyint**|1 = 唯讀<br /><br /> 2 = 捲動鎖定<br /><br /> 3 = 開放式|  
|scrollable|**tinyint**|0 = 順向<br /><br /> 1 = 可捲動|  
|open_status|**tinyint**|0 = 已關閉<br /><br /> 1 = 開啟|  
|cursor_rows|**decimal(10,0)**|結果集中符合的資料列數目。 如需詳細資訊，請參閱 [@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)。|  
|fetch_status|**smallint**|這個資料指標上一次提取的狀態。 如需詳細資訊，請參閱 [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)。<br /><br /> 0 = 順利提取。<br /><br /> -1 = 提取失敗，或超出資料指標界限。<br /><br /> -2 = 遺漏要求的資料列。<br /><br /> -9 = 資料指標尚無任何提取動作。|  
|column_count|**smallint**|資料指標結果集中的資料行數目。|  
|row_count|**decimal(10,0)**|資料指標上次作業所影響的資料列數。 如需詳細資訊，請參閱 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)。|  
|last_operation|**tinyint**|上次在資料指標上執行的作業：<br /><br /> 0 = 未在資料指標上執行任何作業。<br /><br /> 1 = OPEN<br /><br /> 2 = FETCH<br /><br /> 3 = 插入<br /><br /> 4 = UPDATE<br /><br /> 5 = DELETE<br /><br /> 6 = CLOSE<br /><br /> 7 = DEALLOCATE|  
|cursor_handle|**int**|伺服器範圍內的資料指標唯一值。|  
  
## <a name="remarks"></a>備註  
 sp_describe_cursor 描述伺服器資料指標的全域屬性，如捲動和更新的能力。 請利用 sp_describe_cursor_columns 來取得資料指標所傳回之結果集的屬性描述。 請利用 sp_describe_cursor_tables 來取得資料指標所參考之基底資料表的報表。 若要取得連接上可見的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器資料指標的報表，請使用 sp_cursor_list。  
  
 DECLARE CURSOR 陳述式可以要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法利用 DECLARE CURSOR 所包含之 SELECT 陳述式來支援的資料指標類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會隱含地將資料指標轉換成它能夠利用 SELECT 陳述式來支援的類型。 如果 DECLARE CURSOR 陳述式中指定 TYPE_WARNING，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會傳送一則已轉換完成的參考訊息給應用程式。 然後可以呼叫 sp_describe_cursor 來判斷已實作的資料指標的類型。  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會開啟一個全域資料指標，且會利用 `sp_describe_cursor` 來報告資料指標的屬性。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR STATIC FOR  
SELECT LastName  
FROM Person.Person;  
  
OPEN abc;  
  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor into the cursor variable.  
EXEC master.dbo.sp_describe_cursor @cursor_return = @Report OUTPUT,  
        @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor.  
CLOSE @Report;  
DEALLOCATE @Report;  
GO  
  
-- Close and deallocate the original cursor.  
CLOSE abc;  
DEALLOCATE abc;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料指標](../../relational-databases/cursors.md)   
 [CURSOR_STATUS &#40;Transact SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_cursor_list &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor_columns &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [sp_describe_cursor_tables &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
  

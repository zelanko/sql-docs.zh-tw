---
description: sp_describe_cursor_tables (Transact-SQL)
title: sp_describe_cursor_tables (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_cursor_tables_TSQL
- sp_describe_cursor_tables
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_cursor_tables
ms.assetid: 02c0f81a-54ed-4ca4-aa4f-bb7463a9ab9a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 01e7850faa83e6d8854b5ac1a0138cd4363adf4b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447241"
---
# <a name="sp_describe_cursor_tables-transact-sql"></a>sp_describe_cursor_tables (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  報告伺服器資料指標所參考的物件或基底資料表。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_describe_cursor_tables   
     [ @cursor_return = ] output_cursor_variable OUTPUT   
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
 [ @cursor_return =] *output_cursor_variable*輸出  
 這是用來接收資料指標輸出之宣告資料指標變數的名稱。 *output_cursor_variable* 是資料 **指標**，沒有預設值，而且在呼叫 sp_describe_cursor_tables 時，不能與任何資料指標產生關聯。 傳回的資料指標是一個可捲動的動態唯讀資料指標。  
  
 [ @cursor_source =] {N'local ' |N'global ' |N'variable' }  
 指定報告的資料指標是利用本機資料指標、全域資料指標或資料指標變數的名稱來指定。 參數為 **Nvarchar (30) **。  
  
 [ @cursor_identity =] N '*local_cursor_name*'  
 這是含有 LOCAL 關鍵字或預設為 LOCAL 的 DECLARE CURSOR 陳述式所建立之資料指標的名稱。 *local_cursor_name* 是 **Nvarchar (128) **。  
  
 [ @cursor_identity =] N '*global_cursor_name*'  
 這是含有 GLOBAL 關鍵字或預設為 GLOBAL 的 DECLARE CURSOR 陳述式所建立之資料指標的名稱。 *global_cursor_name* 也可以是 ODBC 應用程式所開啟的 API 伺服器資料指標名稱，然後藉由呼叫 SQLSetCursorName 來命名資料指標。*global_cursor_name* 是 **Nvarchar (128) **。  
  
 [ @cursor_identity =] N '*input_cursor_variable*'  
 這是與開啟的資料指標相關聯的資料指標變數名稱。 *input_cursor_variable* 是 **Nvarchar (128) **。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="cursors-returned"></a>傳回的資料指標  
 sp_describe_cursor_tables 將其報表封裝為數據 [!INCLUDE[tsql](../../includes/tsql-md.md)] **指標** 輸出參數。 這樣 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次、預存程序和觸發程序就能夠一次處理一個資料列的輸出。 另外，這也表示無法直接從 API 函數呼叫程序。 **Cursor** output 參數必須系結至程式變數，但 api 不支援系結資料**指標**參數或變數。  
  
 下表顯示 sp_describe_cursor_tables 所傳回的資料指標格式。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|table owner|**sysname**|資料表擁有者的使用者識別碼。|  
|Table_name|**sysname**|物件或基底資料表的名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，伺服器資料指標一律會傳回使用者指定的物件，而不是基底資料表。|  
|Optimizer_hints|**smallint**|點陣圖是由下列中的一或多項所組成：<br /><br /> 1 = 資料列層級鎖定 (ROWLOCK)<br /><br /> 4 = 頁面層級鎖定 (PAGELOCK)<br /><br /> 8 = 資料表鎖定 (TABLOCK)<br /><br /> 16 = 獨佔資料表鎖定 (TABLOCKX)<br /><br /> 32 = 更新鎖定 (UPDLOCK)<br /><br /> 64 = 無鎖定 (NOLOCK)<br /><br /> 128 = 快速第一資料列選項 (FASTFIRST)<br /><br /> 4096 = 當搭配 DECLARE CURSOR (HOLDLOCK) 時，讀取可重複的語意<br /><br /> 當提供多個選項時，系統會使用限制性最高的項目。 不過，sp_describe_cursor_tables 會顯示查詢所指定的旗標。|  
|lock_type|**smallint**|針對這個資料指標的每個基底資料表而明確或隱含地要求的捲動鎖定類型。 這個值可以是下列值之一：<br /><br /> 0 = 無<br /><br /> 1 = 共用<br /><br /> 3 = 更新|  
|server_name|**sysname，可為 null**|資料表所在連結伺服器的名稱。 當使用 OPENQUERY 或 OPENROWSET 時，便是 NULL。|  
|Objectid|**int**|資料表的物件識別碼。 當使用 OPENQUERY 或 OPENROWSET 時，便是 0。|  
|dbid|**int**|資料表所在資料庫的識別碼。 當使用 OPENQUERY 或 OPENROWSET 時，便是 0。|  
|dbname|**sysname**， **可為 null**|資料表所在資料庫的名稱。 當使用 OPENQUERY 或 OPENROWSET 時，便是 NULL。|  
  
## <a name="remarks"></a>備註  
 sp_describe_cursor_tables 會描述伺服器資料指標所參考的基底資料表。 如需資料指標所傳回之結果集的屬性描述，請使用 sp_describe_cursor_columns。 如需資料指標全域性質的描述，如它的捲動和更新的能力，請使用 sp_describe_cursor。 若要取得連接上可見的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 伺服器資料指標報表，請使用 sp_cursor_list。  
  
## <a name="permissions"></a>權限  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會開啟一個全域資料指標，且會利用 `sp_describe_cursor_tables` 來報告資料指標所參考的資料表。  
  
```  
USE AdventureWorks2012;  
GO  
-- Declare and open a global cursor.  
DECLARE abc CURSOR KEYSET FOR  
SELECT LastName  
FROM Person.Person  
WHERE LastName LIKE 'S%';  
  
OPEN abc;  
GO  
-- Declare a cursor variable to hold the cursor output variable  
-- from sp_describe_cursor_tables.  
DECLARE @Report CURSOR;  
  
-- Execute sp_describe_cursor_tables into the cursor variable.  
EXEC master.dbo.sp_describe_cursor_tables  
      @cursor_return = @Report OUTPUT,  
      @cursor_source = N'global', @cursor_identity = N'abc';  
  
-- Fetch all the rows from the sp_describe_cursor_tables output cursor.  
FETCH NEXT from @Report;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
   FETCH NEXT from @Report;  
END  
  
-- Close and deallocate the cursor from sp_describe_cursor_tables.  
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
 [CURSOR_STATUS &#40;Transact-sql&#41;](../../t-sql/functions/cursor-status-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [sp_cursor_list &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)   
 [sp_describe_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)   
 [sp_describe_cursor_columns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

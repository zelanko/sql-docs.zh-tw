---
title: sys.fn_get_sql (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_get_sql
- sys.fn_get_sql_TSQL
- fn_get_sql_TSQL
- sys.fn_get_sql
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_sql function
- text [SQL Server], SQL handles
- sys.fn_get_sql function
- valid SQL handles [SQL Server]
- SQL handles
ms.assetid: d5fe49b5-0813-48f2-9efb-9187716b2fd4
caps.latest.revision: 39
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5051b76490bc27a5e16aedf16be2bdff2dab8c95
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysfngetsql-transact-sql"></a>sys.fn_get_sql (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定 SQL 控制代碼之 SQL 陳述式的文字。  
  
> [!IMPORTANT]  
>  未來的 Microsoft SQL Server 版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 sys.dm_exec_sql_text。 如需詳細資訊，請參閱[sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)。  
  
 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.fn_get_sql ( SqlHandle )  
```  
  
## <a name="arguments"></a>引數  
 *SqlHandle*  
 控制代碼值。 *SqlHandle*是**varbinary(64)** 沒有預設值。  
  
## <a name="tables-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|dbid|**smallint**|資料庫識別碼。 對於隨選和準備的 SQL 陳述式而言，則為編譯陳述式的資料庫識別碼。|  
|objectid|**int**|資料庫物件的識別碼。 特定 SQL 陳述式的這個值是 NULL。|  
|number|**smallint**|如果將程序分組的話，便指出群組數目。<br /><br /> 0 = 項目不是程序。<br /><br /> NULL = 特定 SQL 陳述式。|  
|encrypted|**bit**|指出物件是否已經加密。<br /><br /> 0 = 未加密<br /><br /> 1 = 已加密|  
|text|**text**|這是 SQL 陳述式的文字。 加密物件的這個值是 NULL。|  
  
## <a name="remarks"></a>備註  
 您可以取得有效的 SQL 控制代碼的 sql_handle 資料行從[sys.dm_exec_requests &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)動態管理檢視。  
  
 如果您傳遞的控制代碼，不再存在於快取，fn_get_sq**l**傳回空的結果集。 如果您傳遞無效的控制代碼，批次會停止，且會傳回錯誤訊息。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]無法快取某些[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式，例如大量複製陳述式和字串常值大於 8 KB 的陳述式。 這些陳述式的控制代碼無法利用 fn_get_sql 來擷取。  
  
 **文字**篩選結果集的資料行可能包含密碼的文字。 如需儲存資訊之安全性相關的程序未受監視，請參閱[篩選追蹤](../../relational-databases/sql-trace/filter-a-trace.md)。  
  
 Fn_get_sql 函數會傳回類似的資訊[DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)命令。 以下是何時因無法使用 DBCC INPUTBUFFER 而能夠使用 fn_get_sql 函數的範例：  
  
-   當事件超出 255 個字元時。  
  
-   當您必須傳回預存程序的最高目前巢狀層級時。 例如，有名稱為 sp_1 和 sp_2 的兩個預存程序。 如果 sp_1 呼叫 sp_2，且您在 sp_2 執行時，從 sys.dm_exec_requests 動態管理檢視中取得控制代碼，fn_get_sql 函數會傳回 sp_2 的相關資訊。 另外，fn_get_sql 函數還會傳回最高目前巢狀層級的預存程序完整文字。  
  
## <a name="permissions"></a>Permissions  
 使用者需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
 資料庫管理員可以依照下列範例所示，利用 fn_get_sql 函數來協助診斷問題處理序。 在管理員識別問題工作階段識別碼之後，管理員可以擷取該工作階段的 SQL 控制代碼，利用這個控制代碼來呼叫 fn_get_sql，再利用起始和結束位移來判斷問題工作階段識別碼的 SQL 文字。  
  
```  
DECLARE @Handle varbinary(64);  
SELECT @Handle = sql_handle   
FROM sys.dm_exec_requests   
WHERE session_id = 52 and request_id = 0;  
SELECT * FROM sys.fn_get_sql(@Handle);  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DBCC INPUTBUFFER &#40;Transact SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)   
 [sys.sysprocesses &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  

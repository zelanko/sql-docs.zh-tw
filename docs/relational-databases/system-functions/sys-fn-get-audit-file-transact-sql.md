---
title: sys.fn_get_audit_file (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_get_audit_file_TSQL
- sys.fn_get_audit_file_TSQL
- fn_get_audit_file
- sys.fn_get_audit_file
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_get_audit_file function
- fn_get_audit_file function
ms.assetid: d6a78d14-bb1f-4987-b7b6-579ddd4167f5
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4ac4372d753bdc9fde231d2ec08daa957771dc46
ms.sourcegitcommit: e851f3cab09f8f09a9a4cc0673b513a1c4303d2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2018
---
# <a name="sysfngetauditfile-transact-sql"></a>sys.fn_get_audit_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器稽核建立的稽核檔案中傳回資訊。 如需詳細資訊，請參閱 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
fn_get_audit_file ( file_pattern,   
    { default | initial_file_name | NULL },   
    { default | audit_record_offset | NULL } )  
```  
  
## <a name="arguments"></a>引數  
 *file_pattern*  
 針對要讀取的稽核檔案集合指定目錄或路徑及檔案名稱。 型別是**nvarchar （260)**。 
 
 - **SQL Server**:
    
    這個引數必須同時包含路徑 (磁碟機代號或網路共用位置) 以及可包含萬用字元的檔案名稱。 單一星號 （*） 可以用來從稽核檔案集合收集多個檔案。 例如：  
  
    -   **\<路徑 >\\ \***  -收集的所有稽核檔案中指定的位置。  
  
    -   **\<路徑 > \LoginsAudit_{GUID}** -收集具有指定的名稱和 GUID 配對的檔案的所有稽核。  
  
    -   **\<路徑 > \LoginsAudit_{GUID}_00_29384.sqlaudit** -收集指定的稽核檔案。  
  
 - **Azure SQL Database**:
 
    這個引數用來指定 blob URL （包括儲存體端點和容器）。 雖然它不支援星號萬用字元，您可以使用的部分檔案 (blob) 名稱的前置詞 （而不是完整的 blob 名稱） 來收集開頭為此前置詞的多個檔案 (blob)。 例如：
 
      - **\<Storage_endpoint\>/\<容器\>/\<ServerName\>/\<DatabaseName\> /** -會收集所有稽核檔案 (blob) 的特定資料庫。    
      
      - **\<Storage_endpoint\>/\<容器\>/\<ServerName\>/\<DatabaseName\> /\<AuditName\>/\<CreationDate\>/\<FileName\>.xel** -收集指定的稽核檔案 (blob)。
  
> [!NOTE]  
>  如果傳遞路徑而沒有包含檔案名稱模式，則會產生錯誤。  
  
 *initial_file_name*  
 指定稽核檔案集合中要開始讀取稽核記錄之特定檔案的路徑和名稱。 型別是**nvarchar （260)**。  
  
> [!NOTE]  
>  *Initial_file_name*引數必須包含有效的項目，或必須包含預設 |NULL 值。  
  
 *audit_record_offset*  
 指定包含為 initial_file_name 指定之檔案的已知位置。 當使用這個引數時，此函數會開始讀取緩衝區內緊接在指定的位移之後的第一筆記錄。  
  
> [!NOTE]  
>  *Audit_record_offset*引數必須包含有效的項目，或必須包含預設 |NULL 值。 型別是**bitint**。  
  
## <a name="tables-returned"></a>傳回的資料表  
 下表描述這個函數可傳回的稽核檔案內容。  
  
|資料行名稱|類型|Description|  
|-----------------|----------|-----------------|  
|event_time|**datetime2**|可稽核的動作引發時的日期和時間。 不可為 Null。|  
|sequence_number|**int**|追蹤單一稽核記錄中太長而無法納入稽核寫入緩衝區內的記錄順序。 不可為 Null。|  
|action_id|**varchar(4)**|動作的識別碼。 不可為 Null。|  
|succeeded|**bit**|指示觸發此事件的動作是否成功。 不可為 Null。 若為登入事件以外的所有事件，這只會報告權限檢查成功或失敗，而不會報告作業成功或失敗。<br /> 1 = 成功<br /> 0 = 失敗|  
|permission_bitmask|**varbinary(16)**|在某些動作中，這就是已授與、拒絕或撤銷的權限。|  
|is_column_permission|**bit**|指出這是否為資料行層級權限的旗標。 不可為 Null。 當 permission_bitmask = 0 時會傳回 0。<br /> 1 = true<br /> 0 = false|  
|session_id|**smallint**|事件發生所在之工作階段的識別碼。 不可為 Null。|  
|server_principal_id|**int**|動作執行所在之登入環境的識別碼。 不可為 Null。|  
|database_principal_id|**int**|動作執行所在之資料庫使用者環境的識別碼。 不可為 Null。 如果不適用則傳回 0。 例如，伺服器作業。|  
|target_server_principal_id|**int**|GRANT/DENY/REVOKE 作業執行所在的伺服器主體。 不可為 Null。 如果不適用則傳回 0。|  
|target_database_principal_id|**int**|GRANT/DENY/REVOKE 作業執行所在的資料庫主體。 不可為 Null。 如果不適用則傳回 0。|  
|object_id|**int**|稽核發生所在之實體的識別碼。 這包括下列項目：<br /> 伺服器物件<br /> 資料庫<br /> 資料庫物件<br /> 結構描述物件<br /> 不可為 Null。 如果此實體為伺服器本身或是稽核並未在物件層級上執行，則會傳回 0。 例如驗證。|  
|class_type|**varchar(2)**|稽核發生所在之可稽核的實體類型。 不可為 Null。|  
|session_server_principal_name|**sysname**|工作階段的伺服器主體。 可為 Null。|  
|server_principal_name|**sysname**|目前的登入。 可為 Null。|  
|server_principal_sid|**varbinary**|目前的登入 SID。 可為 Null。|  
|database_principal_name|**sysname**|目前的使用者。 可為 Null。 如果無法使用則傳回 NULL。|  
|target_server_principal_name|**sysname**|動作的目標登入。 可為 Null。 如果不適用則傳回 NULL。|  
|target_server_principal_sid|**varbinary**|目標登入的 SID。 可為 Null。 如果不適用則傳回 NULL。|  
|target_database_principal_name|**sysname**|動作的目標使用者。 可為 Null。 如果不適用則傳回 NULL。|  
|server_instance_name|**sysname**|稽核發生所在的伺服器執行個體名稱。 使用標準的 server\instance 格式。|  
|database_name|**sysname**|動作發生所在的資料庫環境。 可為 Null。 如果是伺服器層級所發生的稽核，則會傳回 NULL。|  
|schema_name|**sysname**|動作發生所在的結構描述環境。 可為 Null。 如果是發生在結構描述外部的稽核，則傳回 NULL。|  
|object_name|**sysname**|稽核發生所在之實體的名稱。 這包括下列項目：<br /> 伺服器物件<br /> 資料庫<br /> 資料庫物件<br /> 結構描述物件<br /> 可為 Null。 如果此實體為伺服器本身或是稽核並未在物件層級上執行，則會傳回 NULL。 例如驗證。|  
|陳述式|**nvarchar(4000)**|TSQL 陳述式 (如果存在的話)。 可為 Null。 如果不適用則傳回 NULL。|  
|additional_information|**nvarchar(4000)**|只套用到單一事件的唯一資訊會以 XML 形式傳回。 少量的可稽核動作有包含這類資訊。<br /><br /> 針對具有相關聯 TSQL 堆疊的動作，以 XML 格式顯示 TSQL 堆疊的單一層級。 此 XML 格式為：<br /><br /> `<tsql_stack><frame nest_level = '%u' database_name = '%.*s' schema_name = '%.*s' object_name = '%.*s' /></tsql_stack>`<br /><br /> Frame nest_level 表示框架的目前巢狀層級。 模組名稱會以三部分格式表示 (database_name、schema_name 和 object_name)。  模組名稱將會剖析為逸出無效的 xml 字元，例如`'\<'`， `'>'`， `'/'`， `'_x'`。 它們會逸出為`_xHHHH\_`。 HHHH 代表字元的四位數十六進位 UCS-2 碼。<br /><br /> 可為 Null。 當此事件未報告其他資訊時，則會傳回 NULL。|  
|file_name|**varchar(260)**|記錄來自之稽核記錄檔的路徑和名稱。 不可為 Null。|  
|audit_file_offset|**bigint**|檔案中包含稽核記錄的緩衝區位移。 不可為 Null。|  
|user_defined_event_id|**smallint**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 做為引數傳遞使用者定義的事件識別碼**sp_audit_write**。 **NULL**系統事件 （預設值） 和非零的使用者定義的事件。 如需詳細資訊，請參閱[sp_audit_write &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md).|  
|user_defined_information|**nvarchar(4000)**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 用來記錄使用者想要記錄的任何額外資訊 |使用稽核記錄檔**sp_audit_write**預存程序。|  
|audit_schema_version |**int** | |  
|sequence_group_id |**varbinary** | 僅 SQL Server （從 2016年開始） |  
|transaction_id |**bigint** | 僅 SQL Server （從 2016年開始） |  
|client_ip |**nvarchar(128)** | Azure SQL DB + （起 2017年） 的 SQL Server |  
|application_name |**nvarchar(128)** | Azure SQL DB + （起 2017年） 的 SQL Server |  
|duration_milliseconds |**bigint** | 只有 azure SQL DB |  
|response_rows |**bigint** | 只有 azure SQL DB |  
|affected_rows |**bigint** | 只有 azure SQL DB |  
  
## <a name="remarks"></a>備註  
 如果*file_pattern*引數傳遞給**fn_get_audit_file**參考的路徑或檔案不存在，或如果檔案不是稽核檔案， **MSG_INVALID_AUDIT_FILE**會傳回錯誤訊息。  
  
## <a name="permissions"></a>Permissions  
 - **SQL Server**： 需要**CONTROL SERVER**權限。  
 - **Azure SQL DB**： 需要**CONTROL DATABASE**權限。     
    - 伺服器管理員可以存取伺服器上的所有資料庫稽核記錄的檔。
    - 非伺服器系統管理員只能存取從目前資料庫的稽核記錄檔。
    - 將略過不符合上述準則的 blob （略過的 blob 清單會顯示在查詢輸出訊息，），此函數會傳回記錄檔，只會從允許存取的 blob。  
  
## <a name="examples"></a>範例

- **SQL Server**

  此範例會從名為 `\\serverName\Audit\HIPPA_AUDIT.sqlaudit` 的檔案進行讀取。  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('\\serverName\Audit\HIPPA_AUDIT.sqlaudit',default,default);  
  GO  
  ```  

- **Azure SQL Database**

  這個範例會從名為的檔案讀取`ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`:  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  這個範例會讀取來自相同的檔案為上述項目，但具有額外的 T-SQL 子句 (**頂端**， **ORDER BY**，和**其中**子句來篩選所傳回之稽核記錄函式）：
  
  ```  
  SELECT TOP 10 * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default)
  WHERE server_principal_name = 'admin1'
  ORDER BY event_time
  GO
  ```  

  這個範例會讀取所有稽核記錄檔開頭的伺服器從`Sh`: 
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```

如需有關如何建立稽核的完整範例，請參閱[SQL Server Audit &#40; Database engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。

如需設定 Azure SQL Database 稽核的詳細資訊，請參閱[開始使用 SQL Database 稽核](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing)。
  
## <a name="see-also"></a>另請參閱  
 [建立伺服器稽核 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [建立伺服器稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [建立資料庫稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [卸除資料庫稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [建立伺服器稽核與伺服器稽核規格](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  

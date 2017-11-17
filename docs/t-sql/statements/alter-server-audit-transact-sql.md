---
title: "ALTER SERVER AUDIT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_AUDIT_TSQL
- ALTER SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
- ALTER SERVER AUDIT statement
ms.assetid: 63426d31-7a5c-4378-aa9e-afcf4f64ceb3
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6d2522a2876165f8e18222f2268dad091a6ba342
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-server-audit--transact-sql"></a>ALTER SERVER AUDIT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 功能改變伺服器稽核物件。 如需詳細資訊，請參閱 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ALTER SERVER AUDIT audit_name  
{  
    [ TO { { FILE ( <file_options> [, ...n] ) } | APPLICATION_LOG | SECURITY_LOG } ]  
    [ WITH ( <audit_options> [ , ...n] ) ]   
    [ WHERE <predicate_expression> ]  
}  
| REMOVE WHERE  
| MODIFY NAME = new_audit_name  
[ ; ]  
  
<file_options>::=  
{  
      FILEPATH = 'os_file_path'   
    | MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED }   
    | MAX_ROLLOVER_FILES = { integer | UNLIMITED }   
    | MAX_FILES = integer   
    | RESERVE_DISK_SPACE = { ON | OFF }   
}  
  
<audit_options>::=  
{  
      QUEUE_DELAY = integer   
    | ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }   
    | STATE = = { ON | OFF }   
}  
  
<predicate_expression>::=  
{  
    [NOT ] <predicate_factor>   
    [ { AND | OR } [NOT ] { <predicate_factor> } ]   
    [,...n ]  
}  
  
<predicate_factor>::=   
    event_field_name { = | < > | ! = | > | > = | < | < = } { number | ' string ' }  
```  
  
## <a name="arguments"></a>引數  
 TO { FILE | APPLICATION_LOG | SECURITY }  
 判斷稽核目標的位置。 選項有二進位檔案、Windows 應用程式記錄檔或 Windows 安全性記錄檔。  
  
 FILEPATH **= '***os_file_path***'**  
 稽核記錄的路徑。 檔案名稱是根據稽核名稱和稽核 GUID 所產生。  
  
 MAXSIZE  **=**  *max_size*  
 指定稽核檔案所能成長的大小上限。 *Max_size*值必須是整數，後面接著**MB**， **GB**， **TB**，或**UNLIMITED**。 您可以針對指定的最小大小*max_size*為 2 **MB**和最大值是 2147483647 **TB**。 當**UNLIMITED**指定，則檔案會成長到磁碟已滿。 指定低於 2 MB 的值，就會引發 MSG_MAXSIZE_TOO_SMALL 錯誤。 預設值是**UNLIMITED**。  
  
 MAX_ROLLOVER_FILES  **=** *整數* | **無限制**  
 指定檔案系統中所要保留的最大檔案數目。 當設定 MAX_ROLLOVER_FILES = 0 時，沒有加諸於所建立的換用檔案數目沒有限制。 預設值是 0。 可以指定的檔案數量上限為 2,147,483,647。  
  
 MAX_FILES =*整數*  
 指定可建立的最大稽核檔案數目。 不會不會彙總到第一個檔案達到限制時。 達到 MAX_FILES 限制時，任何可讓要產生其他稽核事件的動作會失敗並發生錯誤。  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 RESERVE_DISK_SPACE  **=**  {ON |OFF}  
 這個選項會在磁碟上將檔案預先配置為 MAXSIZE 值。 只有當 MAXSIZE 不等於 UNLIMITED 時，才會套用它。 預設值是 OFF。  
  
 QUEUE_DELAY  **=** *整數*  
 判斷在強制處理稽核動作之前經過的時間長度 (以毫秒為單位)。 值為 0 表示同步傳遞。 可設定的最小查詢延遲值為 1000 (1 秒)，這是預設值。 最大值為 2,147,483,647 (2,147,483.647 秒鐘或是 24 天 20 小時 31 分鐘又 23.647 秒鐘)。 指定無效的數字，會引發 MSG_INVALID_QUEUE_DELAY 錯誤。  
  
 ON_FAILURE  **=**  {繼續 |關機 |FAIL_OPERATION}  
 指出如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法寫入稽核記錄，則寫入目標的執行個體應該失敗、繼續還是停止。  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作業繼續進行。 系統不會保留稽核記錄。 稽核會繼續嘗試記錄事件並繼續進行，如果失敗狀況已解決。 選取 continue 選項會允許可能違反安全性原則中的未稽核的活動。 當繼續進行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 作業比維持完整稽核更重要時，請使用此選項。  
  
SHUTDOWN  
會強制執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]關閉如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將資料寫入稽核目標，因為任何原因失敗。 登入執行`ALTER`陳述式必須有`SHUTDOWN`內的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 關機問題持續發生即使`SHUTDOWN`稍後從執行的登入撤銷權限。 如果使用者沒有此權限，然後陳述式會失敗，並將不會修改稽核。 當稽核失敗可能危害系統的安全性或完整性時，請使用此選項。 如需詳細資訊，請參閱[關機](../../t-sql/language-elements/shutdown-transact-sql.md)。 
  
 FAIL_OPERATION  
 如果資料庫動作導致稽核的事件，這些動作就會失敗。 不會導致稽核的事件的動作可繼續進行，但可能會發生任何稽核的事件。 稽核會繼續嘗試記錄事件並繼續進行，如果失敗狀況已解決。 當維持完整稽核比 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的完整存取權更重要時，請使用此選項。  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。   
  
 狀態 **=**  {ON |OFF}  
 啟用或停用收集記錄的稽核。 變更執行中稽核的狀態 (從 ON 變更為 OFF) 會建立已停止稽核的稽核項目、已停止稽核的主體以及停止稽核的時間。  
  
 MODIFY NAME = *new_audit_name*  
 變更稽核的名稱。 不能搭配其他任何選項一起使用。  
  
 predicate_expression  
 指定用來判斷是否應該處理事件的述詞運算式。 述詞運算式限制為 3000 個字元，這會限制字串引數。  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 event_field_name  
 這是識別述詞來源之事件欄位的名稱。 中描述了稽核欄位[sys.fn_get_audit_file &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md). 除了 `file_name` 和 `audit_file_offset` 以外的所有欄位都可進行稽核。  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 number  
 任何數值類型包括**十進位**。 限制為缺少可用的實體記憶體，或是數字太大而不能表示為 64 位元整數。  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 ' string '  
 ANSI 或 Unicode 字串 (依述詞比較的需求而定)。 不會針對述詞比較函數執行隱含字串類型轉換。 傳遞錯誤的類型會產生錯誤。  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
## <a name="remarks"></a>備註  
 當您呼叫 ALTER AUDIT 時，您至少必須指定其中一個 TO、WITH 或 MODIFY NAME 子句。  
  
 您必須將稽核的狀態設定為 OFF 選項，才能變更稽核。 如果而且執行 ALTER AUDIT 時狀態以外的任何選項時啟用稽核 = OFF 時，您會收到 MSG_NEED_AUDIT_DISABLED 錯誤訊息。  
  
 您可以加入、改變及移除稽核規格，而不需停止稽核。  
  
 在稽核已建立之後，就不能變更稽核的 GUID。  
  
## <a name="permissions"></a>Permissions  
 若要建立、改變或卸除伺服器稽核主體，您必須具有 ALTER ANY SERVER AUDIT 或 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-a-server-audit-name"></a>A. 變更伺服器稽核名稱  
 下列範例會將伺服器稽核的名稱 `HIPPA_Audit` 變更為 `HIPAA_Audit_Old`。  
  
```  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
MODIFY NAME = HIPAA_Audit_Old;  
GO  
ALTER SERVER AUDIT HIPAA_Audit_Old  
WITH (STATE = ON);  
GO  
```  
  
### <a name="b-changing-a-server-audit-target"></a>B. 變更伺服器稽核目標  
 下列範例會將稱為 `HIPPA_Audit` 的伺服器稽核變更為檔案目標。  
  
```  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
TO FILE (FILEPATH ='\\SQLPROD_1\Audit\',  
          MAXSIZE = 1000 MB,  
          RESERVE_DISK_SPACE=OFF)  
WITH (QUEUE_DELAY = 1000,  
       ON_FAILURE = CONTINUE);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = ON);  
GO  
```  
  
### <a name="c-changing-a-server-audit-where-clause"></a>C. 變更伺服器稽核 WHERE 子句  
 下列範例會修改 where 子句之範例 C 中建立[CREATE SERVER AUDIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md). 新的 WHERE 子句篩選條件的使用者定義事件識別碼 27。  
  
```tsql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
WHERE user_defined_event_id = 27;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="d-removing-a-where-clause"></a>D. 移除 WHERE 子句  
 下列範例會移除 WHERE 子句述詞運算式。  
  
```tsql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
REMOVE WHERE;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="e-renaming-a-server-audit"></a>E. 重新命名伺服器稽核  
 下列範例會將伺服器稽核名稱從 `FilterForSensitiveData` 變更為 `AuditDataAccess`。  
  
```tsql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
MODIFY NAME = AuditDataAccess;  
GO  
ALTER SERVER AUDIT [AuditDataAccess] WITH (STATE = ON);  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DROP SERVER AUDIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [建立伺服器稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [建立資料庫稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [卸除資料庫稽核規格 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [建立伺服器稽核與伺服器稽核規格](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  


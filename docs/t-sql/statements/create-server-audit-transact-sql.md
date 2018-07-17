---
title: CREATE SERVER AUDIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/22/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_SERVER_AUDIT_TSQL
- SERVER AUDIT
- SERVER_AUDIT_TSQL
- CREATE SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- CREATE SERVER AUDIT statement
- audits [SQL Server], creating
ms.assetid: 1c321680-562e-41f1-8eb1-e7fa5ae45cc5
caps.latest.revision: 44
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 968ea430a01bddf25ccf0e477da2096b4019c7cf
ms.sourcegitcommit: 00ffbc085c5a4b792646ec8657495c83e6b851b5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2018
ms.locfileid: "36942574"
---
# <a name="create-server-audit-transact-sql"></a>CREATE SERVER AUDIT (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 來建立伺服器稽核物件。 如需詳細資訊，請參閱 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE SERVER AUDIT audit_name  
{  
    TO { [ FILE (<file_options> [ , ...n ] ) ] | APPLICATION_LOG | SECURITY_LOG }  
    [ WITH ( <audit_options> [ , ...n ] ) ]   
    [ WHERE <predicate_expression> ]  
}  
[ ; ]  
  
<file_options>::=  
{  
        FILEPATH = 'os_file_path'  
    [ , MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED } ]  
    [ , { MAX_ROLLOVER_FILES = { integer | UNLIMITED } } | { MAX_FILES = integer } ]  
    [ , RESERVE_DISK_SPACE = { ON | OFF } ]   
}  
  
<audit_options>::=  
{  
    [   QUEUE_DELAY = integer ]  
    [ , ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION } ]  
    [ , AUDIT_GUID = uniqueidentifier ]  
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
 TO { FILE | APPLICATION_LOG | SECURITY_LOG }  
 判斷稽核目標的位置。 選項有二進位檔案、Windows 應用程式記錄檔或 Windows 安全性記錄檔。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就無法寫入 Windows 安全性記錄檔。 如需詳細資訊，請參閱 [將 SQL Server Audit 事件寫入安全性記錄檔](../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)。  
  
 FILEPATH ='*os_file_path*'  
 稽核記錄檔的路徑。 檔案名稱是根據稽核名稱和稽核 GUID 所產生。  
  
 MAXSIZE = { *max_size }*  
 指定稽核檔案所能成長的大小上限。 *max_size* 值必須是整數，而且後面緊接著 MB、GB、TB 或 UNLIMITED。 您可以為 *max_size* 指定的大小下限為 2 MB，而上限則為 2,147,483,647 TB。 指定了 UNLIMITED 時，檔案會成長到磁碟已滿為止  (0 也表示 UNLIMITED)。指定低於 2 MB 的值會引發 MSG_MAXSIZE_TOO_SMALL 錯誤。 預設值為 UNLIMITED。  
  
 MAX_ROLLOVER_FILES =*{ integer* | UNLIMITED }  
 除了目前的檔案以外，指定要保留在檔案系統中的檔案數目上限。 *MAX_ROLLOVER_FILES* 值必須是整數或 UNLIMITED。 預設值為 UNLIMITED。 每當稽核重新啟動 (當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體重新啟動或者稽核先關閉然後再次開啟時，就可能會發生此情況) 或者由於達到 MAXSIZE 而需要新的檔案時，系統就會評估此參數。 評估 *MAX_ROLLOVER_FILES* 時，如果檔案的數目超過 *MAX_ROLLOVER_FILES* 設定，系統就會刪除最舊的檔案。 因此，如果 *MAX_ROLLOVER_FILES* 的設定為 0，每次評估 *MAX_ROLLOVER_FILES* 設定時，系統都會建立新的檔案。 評估 *MAX_ROLLOVER_FILES* 設定時，系統只會自動刪除一個檔案，所以當您降低 *MAX_ROLLOVER_FILES* 的值時，除非手動刪除舊的檔案，否則檔案的數目將不會縮減。 可以指定的檔案數量上限為 2,147,483,647。  
  
 MAX_FILES =*integer*  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定可建立的最大稽核檔案數目。 達到此限制時，不會換用第一個檔案。 達到 MAX_FILES 限制時，導致系統產生其他稽核事件的任何動作都會失敗並發生錯誤。  
  
 RESERVE_DISK_SPACE = { ON | OFF }  
 這個選項會在磁碟上將檔案預先配置為 MAXSIZE 值。 只有當 MAXSIZE 不等於 UNLIMITED 時，才會套用它。 預設值是 OFF。  
  
 QUEUE_DELAY =*integer*  
 判斷在強制處理稽核動作之前經過的時間長度 (以毫秒為單位)。 值為 0 表示同步傳遞。 可設定的最小查詢延遲值為 1000 (1 秒)，這是預設值。 最大值為 2,147,483,647 (2,147,483.647 秒鐘或是 24 天 20 小時 31 分鐘又 23.647 秒鐘)。 指定無效的數字會引發 MSG_INVALID_QUEUE_DELAY 錯誤。  
  
 ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }  
 指出如果目標無法寫入稽核記錄，則寫入目標的執行個體應該失敗、繼續還是停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 預設值為 CONTINUE。  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作業繼續進行。 系統不會保留稽核記錄。 稽核會繼續嘗試記錄事件，而且如果失敗狀況已解決，就會恢復稽核。 選取繼續選項會允許可能違反安全性原則的未稽核活動。 當繼續進行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 作業比維持完整稽核更重要時，請使用此選項。  
  
SHUTDOWN  
如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 因為任何原因無法將資料寫入稽核目標，則會強制關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 執行 `CREATE SERVER AUDIT` 陳述式的登入在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內必須擁有 `SHUTDOWN` 權限。 即使稍後已從執行中的登入撤銷 `SHUTDOWN` 權限，關閉的行為仍會持續。 如果使用者沒有此權限，則陳述式將會失敗，且將不會建立稽核。 當稽核失敗可能危害系統的安全性或完整性時，請使用此選項。 如需詳細資訊，請參閱 [SHUTDOWN](../../t-sql/language-elements/shutdown-transact-sql.md)。  
  
 FAIL_OPERATION  
 如果資料庫動作導致稽核的事件，這些動作就會失敗。 雖然不會導致稽核事件的動作可繼續進行，不過也無法發生稽核的事件。 稽核會繼續嘗試記錄事件，而且如果失敗狀況已解決，就會恢復稽核。 當維持完整稽核比 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的完整存取權更重要時，請使用此選項。  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。

 AUDIT_GUID =*uniqueidentifier*  
 若要支援類似資料庫鏡像等案例，稽核需要一個特定的 GUID，而且此 GUID 要符合鏡像資料庫中找到的 GUID。 當建立稽核之後，就無法再修改 GUID。  
  
 predicate_expression  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定用來判斷是否應該處理事件的述詞運算式。 述詞運算式限制為 3000 個字元，這會限制字串引數。  
  
 event_field_name  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 這是識別述詞來源之事件欄位的名稱。 稽核欄位會在 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) 中說明。 除了 `file_name`、`audit_file_offset` 和 `event_time` 以外的所有欄位都可進行稽核。  

> [!NOTE]  
>  雖然 `action_id` 和 `class_type` 欄位在 sys.fn_get_audit_file 中是 **varchar** 類型，但是當它們為可進行篩選的述詞來源時，僅可以搭配數字使用。 若要取得搭配 `class_type` 使用之值的清單，請執行下列查詢：  
> ```sql
> SELECT spt.[name], spt.[number]
> FROM   [master].[dbo].[spt_values] spt
> WHERE  spt.[type] = N'EOD'
> ORDER BY spt.[name];
> ```


 number  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 這是包含 **decimal** 的任何數值類型。 限制為缺少可用的實體記憶體，或是數字太大而不能表示為 64 位元整數。  
  
 ' string '  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 ANSI 或 Unicode 字串 (依述詞比較的需求而定)。 不會針對述詞比較函數執行隱含字串類型轉換。 傳遞錯誤的類型會產生錯誤。  
  
## <a name="remarks"></a>Remarks  
 當建立伺服器稽核之後，它就會處於停用狀態。  
  
 CREATE SERVER AUDIT 陳述式位於交易的範圍內。 如果回復交易，也會回復此陳述式。  
  
## <a name="permissions"></a>Permissions  
 若要建立、更改或卸除伺服器稽核，主體需要使用 ALTER ANY SERVER AUDIT 或 CONTROL SERVER 權限。  
  
 當您將稽核資訊儲存到檔案時，為了避免遭到篡改，您可以限制對檔案位置的存取：  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-server-audit-with-a-file-target"></a>A. 建立具有檔案目標的伺服器稽核  
 下列範例會建立稱為 `HIPPA_Audit` 的伺服器稽核，並將二進位檔案當做目標而且不指定任何選項。  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
```  
  
### <a name="b-creating-a-server-audit-with-a-windows-application-log-target-with-options"></a>B. 建立具有 Windows 應用程式記錄檔目標 (含選項) 的伺服器稽核  
 下列範例會建立稱為 `HIPPA_Audit` 的伺服器稽核，並包含針對 Windows 應用程式記錄檔所設定的目標。 每秒鐘都會寫入此佇列，並在失敗時關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 引擎。  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO APPLICATION_LOG  
    WITH ( QUEUE_DELAY = 1000,  ON_FAILURE = SHUTDOWN);  
```  
  
###  <a name="ExampleWhere"></a> C. 建立包含 WHERE 子句的伺服器稽核  
 下列範例會建立資料庫、結構描述和兩個範例資料表。 名為 `DataSchema.SensitiveData` 的資料表將包含機密資料，而且此資料表的存取權必須記錄在稽核中。 名為 `DataSchema.GeneralData` 的資料表則不包含機密資料。 資料庫稽核規格會稽核 `DataSchema` 結構描述中所有物件的存取權。 伺服器稽核是使用 WHERE 子句所建立，這個子句會將伺服器稽核限制為只有 `SensitiveData` 資料表。 伺服器稽核會假設稽核資料夾存在 `C:\SQLAudit` 中。  
  
```sql  
CREATE DATABASE TestDB;  
GO  
USE TestDB;  
GO  
CREATE SCHEMA DataSchema;  
GO  
CREATE TABLE DataSchema.GeneralData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
CREATE TABLE DataSchema.SensitiveData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
-- Create the server audit in the master database  
USE master;  
GO  
CREATE SERVER AUDIT AuditDataAccess  
    TO FILE ( FILEPATH ='C:\SQLAudit\' )  
    WHERE object_name = 'SensitiveData' ;  
GO  
ALTER SERVER AUDIT AuditDataAccess WITH (STATE = ON);  
GO  
-- Create the database audit specification in the TestDB database  
USE TestDB;  
GO  
CREATE DATABASE AUDIT SPECIFICATION [FilterForSensitiveData]  
FOR SERVER AUDIT [AuditDataAccess]   
ADD (SELECT ON SCHEMA::[DataSchema] BY [public])  
WITH (STATE = ON);  
GO  
-- Trigger the audit event by selecting from tables  
SELECT ID, DataField FROM DataSchema.GeneralData;  
SELECT ID, DataField FROM DataSchema.SensitiveData;  
GO  
-- Check the audit for the filtered content  
SELECT * FROM fn_get_audit_file('C:\SQLAudit\AuditDataAccess_*.sqlaudit',default,default);  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
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
  
  

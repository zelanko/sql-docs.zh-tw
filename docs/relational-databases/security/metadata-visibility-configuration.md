---
title: "中繼資料可見性組態 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subcomponents visibility [SQL Server]
- metadata [SQL Server], visibility
- permissions [SQL Server], metadata access
- viewing metadata
- objects [SQL Server], metadata
- displaying metadata
- database metadata [SQL Server]
- metadata [SQL Server], permissions
ms.assetid: 50d2e015-05ae-4014-a1cd-4de7866ad651
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9381b69a605ed7928851a18e64d7054d43fcb65c
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="metadata-visibility-configuration"></a>中繼資料可見性組態
  中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。 例如，如果授與使用者資料表 `myTable`的 SELECT 或 INSERT 權限，則下列查詢會傳回一個資料列。  
  
```  
SELECT name, object_id  
FROM sys.tables  
WHERE name = 'myTable';  
GO  
```  
  
 但是，如果使用者對 `myTable`沒有任何權限，則查詢會傳回空的結果集。  
  
## <a name="scope-and-impact-of-metadata-visibility-configuration"></a>中繼資料可見性組態的範圍和影響  
 中繼資料可見性組態僅適用於下列安全性實體。  
  
|||  
|-|-|  
|目錄檢視|[!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help** 預存程序|  
|公開內建函數的中繼資料|資訊結構描述檢視|  
|相容性檢視|擴充屬性|  
  
 中繼資料可見性組態不適用於下列安全性實體。  
  
|||  
|-|-|  
|「記錄傳送」系統資料表|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 系統資料表|  
|資料庫維護計畫系統資料表|「備份」系統資料表|  
|「複寫」系統資料表|複寫和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent **sp_help** 預存程序|  
  
 中繼資料存取範圍有限制的意義如下：  
  
-   假設以 **public** 來存取中繼資料的應用程式會中斷。  
  
-   對系統檢視查詢可能只會傳回資料列的子集，或有時候傳回空的結果集。  
  
-   發出中繼資料的內建函數 (例如 OBJECTPROPERTYEX) 可能傳回 NULL。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help** 預存程序可能只會傳回資料列的子集，或傳回 NULL。  
  
 SQL 模組 (例如預存程序和觸發程序) 會在呼叫者的安全性內容下執行，因此在中繼資料的存取上受到限制。 例如，在下列的程式碼中，當預存程序嘗試存取資料表 `myTable` 的中繼資料而呼叫者對此資料表沒有任何權限時，將會傳回空的結果集。 若在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則會傳回一個資料列。  
  
```  
CREATE PROCEDURE assumes_caller_can_access_metadata  
BEGIN  
SELECT name, id   
FROM sysobjects   
WHERE name = 'myTable';  
END;  
GO  
```  
  
 若要讓呼叫者能夠檢視中繼資料，您可以在適當範圍 (例如，物件層級、資料庫層級或伺服器層級) 授與呼叫者 VIEW DEFINITION 權限。 因此，在上個範例中，如果呼叫者具有 `myTable` 的 VIEW DEFINITION 權限，預存程序就會傳回一個資料列。 如需詳細資訊，請參閱 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md) 和[授與資料庫權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)。  
  
 您也可以修改預存程序，使其在擁有者的認證下執行。 若程序擁有者和資料表擁有者是相同的擁有者，就會套用擁有權鏈結，且程序擁有者的安全性內容就可以存取 `myTable`的中繼資料。 在這種狀況下，下列程式碼會將中繼資料的資料列傳回給呼叫者。  
  
> [!NOTE]  
>  下列範例使用 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 目錄檢視，而非 [sys.sysobjects](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md) 相容性檢視。  
  
```  
CREATE PROCEDURE does_not_assume_caller_can_access_metadata  
WITH EXECUTE AS OWNER  
AS  
BEGIN  
SELECT name, id  
FROM sys.objects   
WHERE name = 'myTable'   
END;  
GO  
```  
  
> [!NOTE]  
>  您可以使用 EXECUTE AS，暫時切換到呼叫者的安全性內容。 如需詳細資訊，請參閱 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)。  
  
## <a name="benefits-and-limits-of-metadata-visibility-configuration"></a>中繼資料可見性組態的優點和限制  
 中繼資料可見性組態在整體安全性計畫中扮演著重要的角色。 但在某些情況中，技術純熟又執意操作的使用者還是能夠強制洩漏某些中繼資料。 我們建議您將中繼資料權限部署為全面防禦中的一環。  
  
 強制發出錯誤訊息中的中繼資料，理論上是可行的，做法是在查詢中操縱述詞評估的順序。 這種「嘗試與錯誤攻擊」的可能性不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所特有。 它由關聯式代數所允許的關聯式和交換式轉換所暗示。 您可以限制錯誤訊息所傳回的資訊來減輕此風險。 若要以此方式進一步限制中繼資料的可見性，您可以用追蹤旗標 3625 來啟動伺服器。 此追蹤旗標限制錯誤訊息所顯示的資訊量。 而這有助於防止強制洩漏。 代價是錯誤訊息會簡單一些，用於偵錯時可能會比較困難。 如需詳細資訊，請參閱 [Database Engine 服務啟動選項](../../database-engine/configure-windows/database-engine-service-startup-options.md)和[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  
  
 下列的中繼資料不會被強制洩漏：  
  
-   **sys.servers** 的 **provider_string**資料行中儲存的值。 沒有 ALTER ANY LINKED SERVER 權限的使用者在資料行中只會看見 NULL 值。  
  
-   使用者自訂物件 (例如預存程序或觸發程序) 的來源定義。 只有下列任一狀況屬實時，才能看見原始程式碼：  
  
    -   使用者具有物件的 VIEW DEFINITION 權限。  
  
    -   使用者對該物件的 VIEW DEFINITION 權限尚未被拒絕，且使用者具有該物件的 CONTROL、ALTER 或 TAKE OWNERSHIP 權限。 其他所有使用者都只會看到 NULL。  
  
-   下列目錄檢視中的定義資料行：  
  
    |||  
    |-|-|  
    |**sys.all_sql_modules**|**sys.sql_modules**|  
    |**sys.server_sql_modules**|**sys.check_constraints**|  
    |**sys.default_constraints**|**sys.computed_columns**|  
    |**sys.numbered_procedures**||  
  
-   **syscomments** 相容性檢視中的 **ctext** 資料行。  
  
-   **sp_helptext** 程序的輸出。  
  
-   資訊結構描述檢視中的下列資料行：  
  
    |||  
    |-|-|  
    |INFORMATION_SCHEMA.CHECK_CONSTRAINTS.CHECK_CLAUSE|INFORMATION_SCHEMA.COLUMNS.COLUMN_DEFAULT|  
    |INFORMATION_SCHEMA.DOMAINS.DOMAIN_DEFAULT|INFORMATION_SCHEMA.ROUTINE_COLUMNS.COLUMN_DEFAULT|  
    |INFORMATION_SCHEMA.ROUTINES.ROUTINE_DEFINITION|INFORMATION_SCHEMA.VIEWS.VIEW_DEFINITION|  
  
-   OBJECT_DEFINITION() 函數  
  
-   **sys.sql_logins**的 password_hash 資料行中儲存的值。  沒有 CONTROL SERVER 權限的使用者將在此資料行中看到 NULL 值。  
  
> [!NOTE]  
>  內建系統程序和函數的 SQL 定義，可經由 **sys.system_sql_modules** 目錄檢視、 **sp_helptext** 預存程序和 OBJECT_DEFINITION() 函數公開檢視。  
  
## <a name="general-principles-of-metadata-visibility"></a>中繼資料可見性的一般原則  
 下列是幾個關於中繼資料可見性的一般考量原則：  
  
-   固定角色的隱含權限  
  
-   權限範圍  
  
-   DENY 的優先順序  
  
-   子元件中繼資料的可見性  
  
### <a name="fixed-roles-and-implicit-permissions"></a>固定角色和隱含權限  
 固定角色可以存取的中繼資料取決於其對應的隱含權限。  
  
### <a name="scope-of-permissions"></a>權限範圍  
 在某個範圍的權限意味著，查看該範圍及所有包含範圍之中繼資料的能力。 例如，結構描述的 SELECT 權限表示被授與者對該結構描述包含的所有安全性實體具有 SELECT 權限。 因此，授與結構描述的 SELECT 權限，可讓使用者查看結構描述的中繼資料，以及其中所有資料表、檢視、函數、程序、佇列、同義字、類型和 XML 結構描述集合。 如需範圍的詳細資訊，請參閱[權限階層 &#40;Database Engine&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)。  
  
### <a name="precedence-of-deny"></a>DENY 的優先順序  
 DENY 的優先順序通常高於其他權限。 例如，如果授與資料庫使用者結構描述的 EXECUTE 權限，但是對該結構描述中某個預存程序的 EXECUTE 權限遭到拒絕，則使用者就不能檢視該預存程序的中繼資料。  
  
 此外，如果某個使用者對結構描述的 EXECUTE 權限被拒，但是曾被授與該結構描述中某個預存程序的 EXECUTE 權限，則使用者還是不能檢視該預存程序的中繼資料。  
  
 以其他例子來說，如果授與使用者預存程序的 EXECUTE 權限而又被拒絕 (使用不同角色成員資格可能會造成這種情形)，則會優先執行 DENY，而使用者將不能檢視該預存程序的中繼資料。  
  
### <a name="visibility-of-subcomponent-metadata"></a>子元件中繼資料的可見性  
 子元件 (例如索引、檢查條件約束和觸發程序) 的可見性是由其父元件上的權限來決定。 這些子元件不具有可授與的權限。 例如，如果某個使用者被授與了某個資料表的部分權限，該使用者就能檢視資料表、資料行、索引、檢查條件約束、觸發程序和其他子元件的中繼資料。  
  
#### <a name="metadata-that-is-accessible-to-all-database-users"></a>所有資料庫使用者都可以存取的中繼資料  
 在特定資料庫中，某些中繼資料必須可由所有使用者存取。 例如，檔案群組不具可授與的權限，所以使用者無法被授與權限來檢視檔案群組的中繼資料。 但是，任何可以建立資料表的使用者，必定能夠存取檔案群組中繼資料，以使用 CREATE TABLE 陳述式中的 ON *filegroup* 或 TEXTIMAGE_ON *filegroup* 子句。  
  
 DB_ID() 和 DB_NAME() 函數傳回的中繼資料，所有使用者都可以看到。  
  
 下表列出 **public** 角色可以看見的目錄檢視。  
  
|||  
|-|-|  
|**sys.partition_functions**|**sys.partition_range_values**|  
|**sys.partition_schemes**|**sys.data_spaces**|  
|**sys.filegroups**|**sys.destination_data_spaces**|  
|**sys.database_files**|**sys.allocation_units**|  
|**sys.partitions**|**sys.messages**|  
|**sys.schemas**|**sys.configurations**|  
|**sys.sql_dependencies**|**sys.type_assembly_usages**|  
|**sys.parameter_type_usages**|**sys.column_type_usages**|  
  
## <a name="see-also"></a>另請參閱  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [EXECUTE AS 子句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  


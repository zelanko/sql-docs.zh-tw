---
title: 管理 FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], security
- FileTables [SQL Server], managing access
ms.assetid: 93af982c-b4fe-4be0-8268-11f86dae27e1
caps.latest.revision: 23
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b7bd860efcf71ec72e70fab40ef1efe60b1ecc13
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135402"
---
# <a name="manage-filetables"></a>管理 FileTable
  描述用於管理 FileTable 的常見管理工作。  
  
##  <a name="HowToEnumerate"></a> 如何：取得 FileTable 和相關物件的清單  
 若要取得 FileTable 的清單，請查詢下列其中一個目錄檢視：  
  
-   [sys.filetables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)  
  
-   [sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql) (檢查 **is_filetable** 資料行的值)。  
  
```tsql  
SELECT * FROM sys.filetables;  
GO  
  
SELECT * FROM sys.tables WHERE is_filetable = 1;  
GO  
```  
  
 若要取得建立相關聯之 FileTable 時所建立的系統定義物件清單，請查詢 [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql) 目錄檢視。  
  
```tsql  
SELECT object_id, OBJECT_NAME(object_id) AS 'Object Name'  
    FROM sys.filetable_system_defined_objects  
    WHERE object_id = filetable_object_id;  
GO  
```  
  
##  <a name="BasicsDisabling"></a> 停用並重新啟用資料庫層級的非交易式存取  
 若要取得特定管理工作所需的獨佔存取，您可能必須暫時停用非交易式存取。  
  
 **ALTER DATABASE 陳述式在變更非交易式存取層級時的行為**  
  
-   將非交易式存取設為 READ_ONLY 或 OFF 時，只要存在與所要求作業衝突的開啟檔案控制代碼，ALTER DATABASE 命令就不會將控制權傳回給使用者。 與此作業衝突的檔案控制代碼包括下列項目：  
  
    -   將存取權設為 **NONE**時，為所有開啟檔案控制代碼。  
  
    -   將存取權設為 **READ_ONLY**時，為所有針對寫入存取所開啟的檔案控制代碼。  
  
     如需有關終止開啟檔案控制代碼的詳細資訊，請參閱本主題中的＜ [終止與 FileTable 相關聯的開啟檔案控制代碼](#BasicsKilling) ＞。  
  
     如果 ALTER DATABASE 命令已取消或因逾時而結束，則交易式存取的層級不會變更。  
  
-   如果您使用 WITH \<終止> 子句 (ROLLBACK AFTER integer [ SECONDS ] | ROLLBACK IMMEDIATE | NO_WAIT) 來呼叫 ALTER DATABASE 陳述式，則系統會終止所有開啟的非交易式檔案控制代碼。  
  
> [!WARNING]  
>  終止開啟檔案控制代碼，可能會導致使用者遺失未儲存的資料。 此行為與檔案系統本身的行為一致。  
  
 **停用非交易式存取的影響**  
  
 變更資料庫層級的非交易式存取層級，會對資料庫層級目錄底下的 FileTable 目錄造成下列影響：  
  
-   將存取權設為 **NONE**時，就無法再存取或看到所有 FileTable 目錄及其內容。  
  
-   將存取權設為 **READ_ONLY**時，所有 FileTable 目錄和其內容也會是唯讀狀態。  
  
 停用執行個體層級的 FILESTREAM，會對該執行個體的資料庫層級目錄和其下的 FileTable 目錄造成下列影響：  
  
-   如果您在執行個體層級停用 FILESTREAM，就不會顯示執行個體上的資料庫層級目錄。  
  
###  <a name="HowToDisable"></a> 如何：停用並重新啟用資料庫層級的非交易式存取  
 如需詳細資訊，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
 **停用完整的非交易式存取**  
 您可以呼叫 **ALTER DATABASE** 陳述式並將 **NON_TRANSACTED_ACCESS** 的值設定為 **READ_ONLY** 或 **OFF**。  
  
```tsql  
-- Disable write access.  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = READ_ONLY );  
GO  
  
-- Disable non-transactional access.  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = OFF );  
GO  
```  
  
 **重新啟用完整的非交易式存取**  
 您可以呼叫 **ALTER DATABASE** 陳述式並將 **NON_TRANSACTED_ACCESS** 的值設定為 **FULL**。  
  
```tsql  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL );  
GO  
```  
  
###  <a name="visible"></a> 如何：確保資料庫中 FileTable 的可見性  
 如果下列所有條件都成立，就會顯示資料庫層級目錄和其下的 FileTable 目錄 (如果有的話)：  
  
1.  在執行個體層級啟用 FILESTREAM。  
  
2.  在資料庫層級啟用非交易式存取。  
  
3.  已在資料庫層級指定有效的目錄。  
  
##  <a name="BasicsEnabling"></a> 停用並重新啟用資料表層級的 FileTable 命名空間  
 停用 FileTable 命名空間，會停用所有使用 FileTable 所建立的系統定義條件約束和觸發程序。 如果您需要使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業來大規模重新組織 FileTable，但不想要產生 FileTable 語意強制執行的成本，這樣做就很有用。 不過，這些作業可能會讓 FileTable 處於不一致的狀態，而且可能會無法重新啟用 FileTable 命名空間。  
  
 停用 FileTable 命名空間會產生下列結果：  
  
-   系統不會實際從資料表中卸除 FileTable 資料行和資料。  
  
-   FileTable 目錄及其所含的檔案和目錄會從檔案系統中消失，而且不適用於進行檔案 I/O 存取。  
  
-   您無法卸除和重新建立系統定義的 FileTable 資料行，但就 DML 作業而言，它們的行為與一般資料行一樣。  
  
-   開啟檔案控制代碼會讓 FileTable 條件約束無法停用，因為此作業在資料表上需要有結構描述鎖定。  
  
-   停用 FileTable 命名空間之後，系統會停止強制執行所有 FileTable 語意 (包含系統定義的條件約束和觸發程序)。  
  
 重新啟用 FileTable 命名空間會產生下列結果：  
  
-   系統會檢查 FileTable 的一致性。 如果發現不一致，則會引發錯誤，而 FileTable 會保持停用狀態，否則會重新啟用 FileTable。  
  
-   系統會還原強制執行 FileTable 語意 (包含系統定義的條件約束和觸發程序)。  
  
-   FileTable 目錄及其所含的檔案及目錄會在檔案系統中顯示，而且可用於進行檔案 I/O 存取。  
  
###  <a name="HowToEnableNS"></a> 如何：停用並重新啟用資料表層級的 FileTable 命名空間  
 您可以使用 **{ ENABLE | DISABLE } FILETABLE_NAMESPACE** 選項來呼叫 ALTER TABLE 陳述式。  
  
 **停用 FileTable 命名空間**  
 ```tsql  
ALTER TABLE filetable_name  
    DISABLE FILETABLE_NAMESPACE;  
GO  
```  
  
 **重新啟用 FileTable 命名空間**  
 ```tsql  
ALTER TABLE filetable_name  
    ENABLE FILETABLE_NAMESPACE;  
GO  
```  
  
##  <a name="BasicsKilling"></a> 終止與 FileTable 相關聯的開啟檔案控制代碼  
 儲存在 FileTable 中之檔案的開啟控制代碼可能會防止特定管理工作所需的獨佔存取。 若要啟用緊急工作，您可能必須終止與一個或多個 FileTable 相關聯的開啟檔案控制代碼。  
  
> [!WARNING]  
>  終止開啟檔案控制代碼，可能會導致使用者遺失未儲存的資料。 此行為與檔案系統本身的行為一致。  
  
###  <a name="HowToListOpen"></a> 如何：取得與 FileTable 相關聯的開啟檔案控制代碼清單  
 查詢 [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql) 目錄檢視。  
  
```tsql  
SELECT * FROM sys.dm_filestream_non_transacted_handles;  
GO  
```  
  
###  <a name="HowToKill"></a> 如何：終止與 FileTable 相關聯的開啟檔案控制代碼  
 使用適當的引數來呼叫預存程序 [sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles)，可終止資料庫或 FileTable 中的所有開啟檔案控制代碼，或是終止特定控制代碼。  
  
```  
USE database_name;  
  
-- Kill all open handles in all the filetables in the database.  
EXEC sp_kill_filestream_non_transacted_handles;  
GO  
  
-- Kill all open handles in a single filetable.  
EXEC sp_kill_filestream_non_transacted_handles @table_name = 'filetable_name';  
GO  
  
-- Kill a single handle.  
EXEC sp_kill_filestream_non_transacted_handles @handle_id = integer_handle_id;  
GO  
```  
  
###  <a name="HowToIdentifyLocks"></a> 如何：識別 FileTable 所持有的鎖定  
 FileTable 所採用的大部分鎖定都會對應至應用程式所開啟的檔案。  
  
 **識別開啟的檔案和相關聯的鎖定**  
 您可以將 [sys.dm_tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql) 動態管理檢視中的 **request_owner_id** 欄位與 [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql) 中的 **fcb_id** 欄位聯結。 在某些情況下，鎖定不會對應至單一開啟檔案控制代碼。  
  
```tsql  
SELECT opened_file_name  
    FROM sys.dm_filestream_non_transacted_handles  
    WHERE fcb_id IN  
        ( SELECT request_owner_id FROM sys.dm_tran_locks );  
GO  
```  
  
##  <a name="BasicsSecurity"></a> FileTable 安全性  
 儲存在 FileTable 中的檔案和目錄都僅受 SQL Server 安全性保護。 會針對檔案系統存取和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取，強制執行以資料表和資料行為基礎的安全性。 但是，不支援 Windows 檔案系統安全性 API 和 ACL 設定。  
  
 適用於 FILESTREAM 檔案群組和容器的安全性及存取權限也適用於 FileTable，因為檔案資料會儲存成 FileTable 中的 FILESTREAM 資料行。  
  
 **FileTable 安全性和 Transact-SQL 存取**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] FileTable 中資料的存取是使用與任何其他資料表相同的方式進行保護。 系統會針對每個存取或變更資料的作業，進行適當的資料表和資料行層級安全性檢查。  
  
 **FileTable 安全性和檔案系統存取**  
 檔案系統 API 需要 FileTable 中整個資料列的適當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 權限 (即資料表層級權限)，才能開啟 FileTable 中所儲存之檔案或目錄的控制代碼。 如果使用者沒有 FileTable 中任何資料行的適當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 權限，則會拒絕檔案系統存取。  
  
##  <a name="OtherBackup"></a> 備份和 FileTable  
 當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來備份 FileTable 時，FILESTREAM 資料會與資料庫中的結構化資料一起備份。 如果您不想要將 FILESTREAM 資料與關聯式資料一起備份，您可以使用部分備份來排除 FILESTREAM 檔案群組。  
  
 **FileTable 備份的交易一致性**  
  
 許多管理工具和作業 (包括備份、記錄備份和異動複寫) 會透過讀取交易記錄來讀取交易上一致的資料。 此時，它們會讀取當做交易之一部分更新的任何 FILESTREAM 資料。 未在資料庫層級啟用非交易式存取時，這些工具和作業會以完整交易一致性的方式運作。  
  
 但是，當啟用完整的非交易式存取時，則 FileTable 包含的更新資料可以比工具或程序從交易記錄讀取的交易還要新 (透過非交易式更新)。 這表示，特定交易的「時間點」還原作業可能會包含比該交易還新的 FILESTREAM 資料。 當 FileTable 上允許非交易式更新時，這會是預期的行為。  
  
##  <a name="Monitor"></a> SQL Server Profiler 和 FileTable  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 可以在儲存於 FileTable 之檔案的追蹤輸出中，擷取「Windows 檔案開啟」和「檔案關閉」作業。  
  
##  <a name="OtherAuditing"></a> 稽核和 FileTable  
 您可以稽核 FileTable，就像其他任何資料表一樣。 但是，不會根據作業來設定 Win32 存取模式。 檔案系統中的單一動作會轉譯成多個 Transact-SQL DML 作業。 例如，在 Microsoft Word 中開啟檔案會轉譯成多個開啟/關閉/建立/重新命名/刪除作業及對應的 Transact-SQL DML 活動。 這會產生詳細稽核記錄，這種記錄很難將檔案系統動作與對應 Transact-SQL DML 稽核記錄之間的記錄產生關聯。  
  
##  <a name="OtherDBCC"></a> DBCC 和 FileTable  
 您可以使用 DBCC CHECKCONSTRAINTS 來驗證 FileTable 上的條件約束，包括系統定義的條件約束。  
  
## <a name="see-also"></a>另請參閱  
 [FileTable 與其他 SQL Server 功能的相容性](filetable-compatibility-with-other-sql-server-features.md)   
 [FileTable DDL、函數、預存程序及檢視](../views/views.md)  
  
  

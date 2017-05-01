---
title: "管理 suspect_pages 資料表 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- 824 (Database Engine error)
- restoring pages [SQL Server]
- pages [SQL Server], suspect
- pages [SQL Server], restoring
- suspect_pages system table
- suspect pages [SQL Server]
- restoring [SQL Server], pages
ms.assetid: f394d4bc-1518-4e61-97fc-bf184d972e2b
caps.latest.revision: 54
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f06acec180d12a9cabfff5e35b4f254883111838
ms.lasthandoff: 04/11/2017

---
# <a name="manage-the-suspectpages-table-sql-server"></a>管理 suspect_pages 資料表 (SQL Server)
  本主題描述如何使用 **或** 管理 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] suspect_pages [!INCLUDE[tsql](../../includes/tsql-md.md)]資料表。 **suspect_pages** 資料表用於維護可疑頁面的相關資訊，有助於決定是否有必要進行還原。 [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) 資料表位於 [msdb 資料庫](../../relational-databases/databases/msdb-database.md)中。  
  
 頁面視為「可疑」的條件如下：當 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 嘗試讀取資料頁時，遇到下列其中一個錯誤：  
  
-   作業系統發出之循環冗餘檢查 (CRC) 所造成的 823 錯誤 ，例如磁碟錯誤 (某些硬體錯誤)  
  
-   824 錯誤，例如損毀頁 (任何邏輯錯誤)  
  
 每一個可疑頁面的頁面識別碼都會記錄在 **suspect_pages** 資料表中。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會記錄正常處理期間 (例如下列時間) 發生的任何可疑頁面：  
  
-   查詢必須讀取頁面。  
  
-   在 DBCC CHECKDB 作業期間。  
  
-   在備份作業期間。  
  
 在還原作業、DBCC 修復作業或卸除資料庫作業期間，也會視需要更新 **suspect_pages** 資料表。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目管理 suspect_pages 資料表：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   **記錄在 suspect_pages 資料表的錯誤**  
  
     **suspect_pages** 資料表每頁都會包含一個因 824 錯誤而失敗的資料列 (上限是 1,000 個資料列)。 下表顯示在 **suspect_pages** 資料表的 **event_type** 資料行中所記錄的錯誤。  
  
    |錯誤描述|**event_type** 值|  
    |-----------------------|---------------------------|  
    |作業系統 CRC 錯誤所導致的 823 錯誤，或是總和檢查碼錯誤或頁面損毀以外之原因 (例如，頁面識別碼不正確) 所導致的 824 錯誤|1|  
    |錯誤的總和檢查碼|2|  
    |損毀頁面|3|  
    |已還原 (在將頁面標示為錯誤頁面之後，還原該頁面)|4|  
    |已修復 (DBCC 已修復頁面)|5|  
    |由 DBCC 取消配置|7|  
  
     **suspect_pages** 資料表也會記錄暫時性錯誤。  暫時性錯誤的來源包括 I/O 錯誤 (例如，纜線連接斷開)，或暫時在重複總和檢查碼測試中失敗的頁面。  
  
-   **Database Engine 更新 suspect_pages 資料表的方式**  
  
     [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會對 **suspect_pages** 資料表採取下列動作：  
  
    -   如果資料表未滿，則為每個 824 錯誤更新一次，以指出發生錯誤，並使錯誤計數器遞增。 如果經修復、還原或取消配置等方式修正錯誤後，頁面仍有錯誤，則其 **number_of_errors** 計數會遞增，而 **last_update** 資料行也會更新  
  
    -   經由還原或修復作業修正列出的頁面後，作業會更新 **suspect_pages** 資料列，指出該頁面已修復 (**event_type** = 5) 或還原 (**event_type** = 4) 該頁面。  
  
    -   如果執行 DBCC 檢查，則該檢查會將任何沒有錯誤的頁面標示為已修復 (**event_type** = 5) 或已取消配置 (**event_type** = 7)。  
  
-   **自動更新 suspect_pages 資料表**  
  
     資料庫鏡像夥伴或 AlwaysOn 可用性複本會在嘗試從資料檔案讀取頁面，但是因為以下其中一個原因而失敗之後，更新 **suspect_pages** 資料表。  
  
    -   作業系統 CRC 錯誤所造成的 823 錯誤。  
  
    -   824 錯誤 (邏輯損毀，例如損毀頁)。  
  
     下列動作也會自動更新 **suspect_pages** 資料表中的資料列。  
  
    -   DBCC CHECKDB REPAIR_ALLOW_DATA_LOSS 會更新 **suspect_pages** 資料表，以指出它所取消配置或修復的每個頁面。  
  
    -   完整、檔案或分頁 RESTORE 會將頁面項目標示為已還原。  
  
     下列動作會從 **suspect_pages** 資料表自動刪除資料列。  
  
    -   ALTER DATABASE REMOVE FILE  
  
    -   DROP DATABASE  
  
-   **資料庫管理員的維護角色**  
  
     資料庫管理員負責管理資料表，主要是刪除舊的資料列。 **suspect_pages** 資料表有大小限制，而且如果該資料表已滿，則不會記錄新的錯誤。 為了避免這個資料表被填滿，資料庫管理員或系統管理員必須手動刪除資料列，以清除這個資料表中的舊項目。 建議您定期刪除或封存包含還原或修復而來之 **event_type** 的資料列，或包含舊 **last_update** 值的資料列。  
  
     若要監視 suspect_pages 資料表上的活動，您可以使用 [Database Suspect Data Page 事件類別](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)。 資料列有時會因為暫時性錯誤而加入 **suspect_pages** 資料表中。 但是，如果有許多資料列加入此資料表，則可能意味著 I/O 子系統發生問題。 如果您注意到突然有許多資料列加入到此資料表，我們建議您最好調查 I/O 子系統是否有問題。  
  
     資料庫管理員也可以插入或更新記錄。 例如，如果資料庫管理員知道某個疑問頁面其實沒問題，但想要保留記錄一段時間，則更新資料列會很有用。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 任何可以存取 **msdb** 的人員，均能讀取 **suspect_pages** 資料表中的資料。 針對 suspect_pages 資料表擁有 UPDATE 權限的任何人都可以更新其記錄。 **msdb** 上 **db_owner** 固定資料庫角色的成員或 **系統管理員** 固定伺服器角色的成員皆可插入、更新及刪除記錄。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-manage-the-suspectpages-table"></a>若要管理 suspect_pages 資料表  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，展開該執行個體，然後展開 [資料庫] 。  
  
2.  依序展開 [系統資料庫] 、[msdb] 、[資料表] 和 [系統資料表] 。  
  
3.  展開 **dbo.suspect_pages** ，然後以滑鼠右鍵按一下 [編輯前 200 個資料列] 。  
  
4.  在查詢視窗中，編輯、更新或刪除所要的資料列。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-manage-the-suspectpages-table"></a>若要管理 suspect_pages 資料表  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 這個範例會刪除 `suspect_pages` 資料表中的部分資料列。  
  
```  
-- Delete restored, repaired, or deallocated pages.  
DELETE FROM msdb..suspect_pages  
   WHERE (event_type = 4 OR event_type = 5 OR event_type = 7);  
GO  
  
```  
  
 這個範例會傳回 `suspect_pages` 資料表中的錯誤頁面。  
  
```  
-- Select nonspecific 824, bad checksum, and torn page errors.  
SELECT * FROM msdb..suspect_pages  
   WHERE (event_type = 1 OR event_type = 2 OR event_type = 3);  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
 [還原頁面 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
    
   
  
  





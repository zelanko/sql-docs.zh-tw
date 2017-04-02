---
title: "檢視或變更資料庫的復原模式 (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "08/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "資料庫備份 [SQL Server], 復原模式"
  - "復原 [SQL Server], 復原模式"
  - "備份資料庫 [SQL Server], 復原模式"
  - "復原模式 [SQL Server], 切換"
  - "復原模式 (SQL Server), 檢視"
  - "資料庫還原 [SQL Server], 復原模式"
  - "修改資料庫復原模式"
ms.assetid: 94918d1d-7c10-4be7-bf9f-27e00b003a0f
caps.latest.revision: 40
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 40
---
# 檢視或變更資料庫的復原模式 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 檢視或變更資料庫。 
  
  「復原模式」是一項資料庫屬性，可控制交易的記錄方式、是否需要 (及允許) 備份交易記錄，以及可用的還原作業類型。 復原模式共有三種：簡單、完整和大量記錄。 一般而言，資料庫會使用完整復原模式或簡單復原模式。 資料庫可以隨時切換到另一個復原模式。 **model** 資料庫會設定新資料庫的預設復原模式。  
  
  如需[復原模式](https://msdn.microsoft.com/library/ms189275.aspx)的更深入說明，請參閱 [MSSQLTips!](https://www.mssqltips.com/) 人員提供的 [SQL Server Recovery Models](https://www.mssqltips.com/sqlservertutorial/2/sql-server-recovery-models/) (SQL Server 復原模式)。
  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  

-   從[完整復原模式或大量記錄復原模式](https://msdn.microsoft.com/library/ms189275.aspx)切換**之前**，請[備份交易記錄](https://msdn.microsoft.com/library/ms179478.aspx)。  
  
-   在大量記錄模式下無法使用時間點復原。 在需要交易記錄還原的大量記錄復原模式下執行交易，可能會有資料遺失的風險。 若要在災害復原的情況下獲得最佳資料復原能力，請只在下列情況下切換到大量記錄復原模式：  
  
    -   資料庫中目前不允許有使用者。  
  
    -   大量處理期間進行的所有修改都可復原，不必依賴建立記錄備份；例如，重新執行大量處理序。  
  
     如果您滿足這兩項條件，還原大量記錄復原模式下備份的交易記錄時，就不必擔心資料遺失。  
  
**注意！** 如果您在大量作業期間切換到完整復原模式，大量作業記錄將從最小記錄變成完整記錄，反之亦然。  
  
###  <a name="Security"></a> 必要權限  
   需要資料庫的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 檢視或變更復原模式  
  
1.  連接到適當的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，請在 [物件總管] 中按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]**，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，然後按一下 [屬性]，這會開啟 [資料庫屬性] 對話方塊。  
  
4.  在 **[選取頁面]** 窗格中，按一下 **[選項]**。  
  
5.  目前的復原模式會顯示在 **[復原模式]** 清單方塊中。  
  
6.  或者，您可以從不同的模式清單中選取來變更復原模式。 這些選擇包括 [完整]、[大量記錄] 或 [簡單]。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 檢視復原模式  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例示範如何查詢 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目錄檢視，以了解 **model** 資料庫的復原模式。  
  
```tsql  
SELECT name, recovery_model_desc  
   FROM sys.databases  
      WHERE name = 'model' ;  
GO  
  
```  
  
#### 變更復原模式  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例示範如何使用 `model` ALTER DATABASE `FULL` 陳述式的 `SET RECOVERY` 選項，將 [資料庫的復原模式變更為](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md) 。  
  
```tsql  
USE master ;  
ALTER DATABASE model SET RECOVERY FULL ;  
```  
  
##  <a name="FollowUp"></a> 建議：變更復原模式之後  
  
-   **在完整模式與大量記錄復原模式之間切換之後**  
  
    -   在完成大量作業之後，立即切換回完整復原模式。  
  
    -   從大量記錄復原模式切換回完整復原模式之後，請備份記錄檔。  
  
        >**注意：**您的備份策略維持不變：持續執行定期資料庫備份、記錄備份及差異備份。  
  
-   **從簡單復原模式切換之後**  
  
    -   在切換至完整復原模式或大量記錄復原模式的作業之後，立即建立完整或差異資料庫備份，以便啟動記錄鏈結。  
  
        >**注意：**只有在第一次資料備份之後，切換到完整或大量記錄復原模式才會生效。  
  
    -   排程定期記錄備份並據此更新還原計畫。  
  
        > **重要！！！！** 備份記錄檔！！ 如果您沒有經常備份記錄，交易記錄會一直擴充，直到磁碟空間用盡為止！  
  
-   **切換到簡單復原模式之後**  
  
    -   中止備份交易記錄的任何排程作業  
  
    -   確定已排程定期資料庫備份。 備份資料庫是必要的動作，才能保護資料及截斷交易記錄中非使用中的部分。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [建立作業](../../ssms/agent/create-a-job.md)  
  
-   [啟用或停用作業](../../ssms/agent/disable-or-enable-a-job.md)  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   [資料庫維護計畫](http://msdn.microsoft.com/library/ms187658.aspx) (在《[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 線上叢書》中)  
  
## 另請參閱  
 [復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
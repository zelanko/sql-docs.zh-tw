---
title: 檢視或變更資料庫的復原模式 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- recovery [SQL Server], recovery model
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], switching
- recovery models [SQL Server], viewing
- database restores [SQL Server], recovery models
- modifying database recovery models
ms.assetid: 94918d1d-7c10-4be7-bf9f-27e00b003a0f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 889080301109938f0514bd6b81265c100237ab60
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84956104"
---
# <a name="view-or-change-the-recovery-model-of-a-database-sql-server"></a>檢視或變更資料庫的復原模式 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視或變更資料庫的復原模式。 「復原模式」  是一項資料庫屬性，可控制交易的記錄方式、是否需要 (及允許) 備份交易記錄，以及可用的還原作業類型。 復原模式共有三種：簡單、完整和大量記錄。 一般而言，資料庫會使用完整復原模式或簡單復原模式。 資料庫可以隨時切換到另一個復原模式。 **model** 資料庫會設定新資料庫的預設復原模式。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目檢視或變更資料庫的復原模式：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作建議：**  [變更復原模式之後](#FollowUp)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   從完整復原模式或大量記錄復原模式切換之前，請備份交易記錄。  
  
-   在大量記錄模式下無法使用時間點復原。 因此，如果您在可能需要交易記錄還原的大量記錄復原模式下執行交易，則這些交易可能會有資料遺失的風險。 若要在災難復原的情況下獲得最佳資料復原能力，建議您只能在下列情況下切換到大量記錄復原模式，以避免資料遺失：  
  
    -   資料庫中目前不允許有使用者。  
  
    -   大量處理期間進行的所有修改都可復原，不必依賴建立記錄備份；例如，重新執行大量處理序。  
  
     如果您滿足這兩項條件，還原大量記錄復原模式下備份的交易記錄時，就不必擔心資料遺失。  
  
> [!NOTE]  
>  如果您在大量作業期間切換到完整復原模式，大量作業的記錄將從最小記錄變成完整記錄，反之亦然。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料庫的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-recovery-model"></a>檢視或變更復原模式  
  
1.  連接到適當的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，請在 [物件總管] 中按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]** ，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，然後按一下 [屬性]  ，這會開啟 [資料庫屬性]  對話方塊。  
  
4.  在 **[選取頁面]** 窗格中，按一下 **[選項]** 。  
  
5.  目前的復原模式會顯示在 **[復原模式]** 清單方塊中。  
  
6.  或者，您可以從不同的模式清單中選取來變更復原模式。 這些選擇包括 [完整]  、[大量記錄]  或 [簡單]  。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-recovery-model"></a>檢視復原模式  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例示範如何查詢 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目錄檢視，以了解 **model** 資料庫的復原模式。  
  
```sql  
SELECT name, recovery_model_desc  
   FROM sys.databases  
      WHERE name = 'model' ;  
GO  
  
```  
  
#### <a name="to-change-the-recovery-model"></a>變更復原模式  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例示範如何使用 `model` ALTER DATABASE `FULL` 陳述式的 `SET RECOVERY` 選項，將 [資料庫的復原模式變更為](/sql/t-sql/statements/alter-database-transact-sql-set-options) 。  
  
```sql  
USE master ;  
ALTER DATABASE model SET RECOVERY FULL ;  
```  
  
##  <a name="follow-up-recommendations-after-you-change-the-recovery-model"></a><a name="FollowUp"></a>後續操作建議：變更復原模式之後  
  
-   **在完整模式與大量記錄復原模式之間切換之後**  
  
    -   在完成大量作業之後，立即切換回完整復原模式。  
  
    -   從大量記錄復原模式切換回完整復原模式之後，請備份記錄檔。  
  
        > [!NOTE]  
        >  您的備份策略維持不變：持續執行定期資料庫備份、記錄備份及差異備份。  
  
-   **從簡單復原模式切換之後**  
  
    -   在切換至完整復原模式或大量記錄復原模式的作業之後，立即建立完整或差異資料庫備份，以便啟動記錄鏈結。  
  
        > [!NOTE]  
        >  只有在第一次資料備份之後，切換到完整或大量記錄復原模式才會生效。  
  
    -   排程定期記錄備份並據此更新還原計畫。  
  
        > [!IMPORTANT]  
        >  如果您沒有經常備份記錄，交易記錄會一直擴充，直到磁碟空間用盡為止。  
  
-   **切換到簡單復原模式之後**  
  
    -   中止備份交易記錄的任何排程作業  
  
    -   確定已排程定期資料庫備份。 備份資料庫是必要的動作，才能保護資料及截斷交易記錄中非使用中的部分。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [建立作業](../../ssms/agent/create-a-job.md)  
  
-   [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相關內容  
  
-   [資料庫維護計畫](../maintenance-plans/maintenance-plans.md) (在《 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 線上叢書》中)  
  
## <a name="see-also"></a>另請參閱  
 [復原模式 &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [交易記錄 &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [復原模式 &#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  

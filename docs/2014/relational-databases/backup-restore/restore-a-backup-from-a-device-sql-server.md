---
title: 從裝置還原備份 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring databases [SQL Server], device restores
- backup devices [SQL Server], restoring from
- database restores [SQL Server], device restores
- devices [SQL Server]
ms.assetid: 6e139de7-7de2-4d18-9df0-beac31ba7ff1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f5e272dde5ca7a3c0ff7246d42131f1e70331689
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921947"
---
# <a name="restore-a-backup-from-a-device-sql-server"></a>從裝置還原備份 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中從裝置還原備份。  
  
> [!NOTE]  
>  如需有關 SQL Server 備份至 Windows Azure Blob 儲存服務的詳細資訊，請參閱＜ [SQL Server 備份及還原與 Windows Azure Blob 儲存體服務](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目，從裝置還原備份：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在，RESTORE 權限預設為 **系統管理員 (sysadmin)** 和 **資料庫建立者 (dbcreator)** 固定伺服器角色的成員以及資料庫的擁有者 (**dbo**) (對 FROM DATABASE_SNAPSHOT 選項而言，資料庫一律存在)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此；因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-restore-a-backup-from-a-device"></a>若要從裝置還原備份  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在 [物件總管] 中按一下伺服器名稱展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]** ，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 [工作]  ，然後按一下 [還原]  。  
  
4.  按一下您想要的還原作業類型 ([資料庫]  、[檔案和檔案群組]  或 [交易記錄檔]  )。 這會開啟對應的還原對話方塊。  
  
5.  在 **[一般]** 頁面的 **[還原來源]** 區段中，按一下 **[來源裝置]** 。  
  
6.  按一下 **[來源裝置]** 文字方塊的瀏覽按鈕，這會開啟 **[指定備份]** 對話方塊。  
  
7.  在 **[備份媒體]** 文字方塊中，選取 **[備份裝置]** ，然後按一下 **[加入]** 按鈕，以開啟 **[選取備份裝置]** 對話方塊。  
  
8.  在 **[備份裝置]** 文字方塊中，選取您要用於還原作業的裝置。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-restore-a-backup-from-a-device"></a>若要從裝置還原備份  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  在 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 陳述式中，指定備份作業要用的邏輯或實體備份裝置。 這個範例會從實體名稱為 `Z:\SQLServerBackups\AdventureWorks2012.bak`的磁碟檔案還原。  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak' ;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)   
 [在簡單復原模式下還原資料庫備份 &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)   
 [還原資料庫備份&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)   
 [還原差異資料庫備份 &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)   
 [將資料庫還原到新位置 &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)   
 [備份檔案和檔案群組 &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [備份交易記錄 &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [建立差異資料庫備份 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
  

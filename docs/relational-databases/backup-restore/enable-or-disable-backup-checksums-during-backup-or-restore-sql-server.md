---
title: 啟用 | 停用備份總和檢查碼
description: 本文說明如何使用 SQL Server Management Studio 或 Transact-SQL，在 SQL Server 中啟用或停用資料庫的備份總和檢查碼。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup checksums [SQL Server]
- disabling checksums
- checksums [SQL Server]
ms.assetid: 6786bd1e-ad97-430a-8dfb-d4ba952d6c4d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3675b4557bae7a394ef5b1b3ac47d2d1da9b2af3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718146"
---
# <a name="enable-or-disable-backup-checksums-during-backup-or-restore-sql-server"></a>在備份或還原期間啟用或停用備份總和檢查碼 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中備份或還原資料庫時啟用或停用備份總和檢查碼。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目啟用或停用備份總和檢查碼：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 備份  
 BACKUP DATABASE 和 BACKUP LOG 權限預設為 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。  
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶必須具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)並不會檢查檔案存取權限。 當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。  
  
 RESTORE  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在，RESTORE 權限預設為 **系統管理員 (sysadmin)** 和 **資料庫建立者 (dbcreator)** 固定伺服器角色的成員以及資料庫的擁有者 (**dbo**) (對 FROM DATABASE_SNAPSHOT 選項而言，資料庫一律存在)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此；因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-enable-or-disable-checksums-during-a-backup-operation"></a>若要在備份作業期間啟用或停用總和檢查碼  
  
1.  請依照＜ [建立資料庫備份](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)＞的步驟執行。  
  
2.  在 **[選項]** 頁面的 **[可靠性]** 區段中，按一下 **[寫入媒體之前執行總和檢查碼]** 。  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-enable-or-disable-backup-checksum-for-a-backup-operation"></a>若要為備份作業啟用或停用備份總和檢查碼  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  若要在 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 陳述式中啟用備份總和檢查碼，請指定 WITH CHECKSUM 選項。 若要停用備份總和檢查碼，請指定 WITH NO_CHECKSUM 選項。 這是預設行為，但是壓縮備份除外。 下列範例指定應執行總和檢查碼。  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM;  
GO  
```  
  
#### <a name="to-enable-or-disable-backup-checksum-for-a-restore-operation"></a>若要為還原作業啟用或停用備份總和檢查碼  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  若要在 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式中啟用備份總和檢查碼，請指定 WITH CHECKSUM 選項。 這是壓縮備份的預設行為。 若要停用備份總和檢查碼，請指定 WITH NO_CHECKSUM 選項。 這是預設行為，但是壓縮備份除外。 下列範例指定應執行備份總和檢查碼。  
  
```sql  
RESTORE DATABASE AdventureWorks2012   
 FROM DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM;  
GO  
```  
  
> [!WARNING]  
>  如果您明確地在還原作業中要求 CHECKSUM，而且備份包含備份總和檢查碼，就會和預設情況一樣，備份總和檢查碼及分頁總和檢查碼都會加以驗證。 然而，如果備份組沒有備份總和檢查碼，則還原作業就會失敗，並且會產生訊息指出總和檢查碼不存在。  
  
## <a name="see-also"></a>另請參閱  
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [備份和還原期間可能發生的媒體錯誤 &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)   
 [指定在發生錯誤後備份或還原作業應該繼續還是停止 &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
  

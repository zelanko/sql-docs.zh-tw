---
title: 指定備份或還原作業應該繼續還是停止後發生錯誤 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], backups
- backing up databases [SQL Server], errors
- backups [SQL Server], errors
- database backups [SQL Server], errors
ms.assetid: 042be17a-b9b0-4629-b6bb-b87a8bc6c316
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 79ab28861fb4ad1eb3fb166e0cccb6b30ff89f86
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537380"
---
# <a name="specify-whether-a-backup-or-restore-operation-continues-or-stops-after-encountering-an-error-sql-server"></a>指定在發生錯誤後備份或還原作業應該繼續還是停止 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，指定在 [!INCLUDE[tsql](../../includes/tsql-md.md)]發生錯誤後，備份或還原作業應該繼續還是停止。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目，指定在發生錯誤後備份或還原作業應該繼續還是停止：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 BACKUP  
 BACKUP DATABASE 和 BACKUP LOG 權限預設為 **系統管理員** 固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。  
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶必須具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)並不會檢查檔案存取權限。 當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。  
  
 RESTORE  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在，RESTORE 權限預設為 **系統管理員 (sysadmin)** 和 **資料庫建立者 (dbcreator)** 固定伺服器角色的成員以及資料庫的擁有者 (**dbo**) (對 FROM DATABASE_SNAPSHOT 選項而言，資料庫一律存在)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此；因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-specify-whether-backup-continues-or-stops-after-an-error-is-encountered"></a>若要指定在發生錯誤後備份應該繼續還是停止  
  
1.  請依照＜ [建立資料庫備份](create-a-full-database-backup-sql-server.md)＞的步驟執行。  
  
2.  在 **[選項]** 頁面的 **[可靠性]** 區段中，按一下 **[寫入媒體之前執行總和檢查碼]** 和 **[發生錯誤時繼續]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-specify-whether-a-backup-operation-continues-or-stops-after-encountering-an-error"></a>若要指定在發生錯誤後備份作業應該繼續還是停止  
  
1.  連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  在 [BACKUP](/sql/t-sql/statements/backup-transact-sql) 陳述式中，指定 CONTINUE_AFTER_ERROR 選項以繼續，或指定 STOP_ON_ERROR 選項以停止。 預設行為是在發生錯誤後停止。 此範例指示備份作業儘管發生錯誤時仍繼續進行。  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM, CONTINUE_AFTER_ERROR;  
GO  
```  
  
#### <a name="to-specify-whether-a-restore-operation-continues-or-stops-after-encountering-an-error"></a>若要指定在發生錯誤後還原作業應該繼續還是停止  
  
1.  連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  在 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 陳述式中，指定 CONTINUE_AFTER_ERROR 選項以繼續，或指定 STOP_ON_ERROR 選項以停止。 預設行為是在發生錯誤後停止。 此範例指示還原作業儘管發生錯誤時仍繼續進行。  
  
```sql  
RESTORE DATABASE AdventureWorks2012   
 FROM DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'   
   WITH CHECKSUM, CONTINUE_AFTER_ERROR;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [RESTORE 引數 &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)   
 [備份和還原期間可能發生的媒體錯誤 &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)   
 [在備份或還原期間啟用或停用備份總和檢查碼 &#40;SQL Server&#41;](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
  

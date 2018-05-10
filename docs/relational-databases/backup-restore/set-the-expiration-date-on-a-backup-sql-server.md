---
title: 設定備份的到期日 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], expiration dates
- expiration [SQL Server]
- database backups [SQL Server], expiration dates
ms.assetid: 76e814df-6487-4893-9f09-7759f1863a5c
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 400ddef2411b5f5933c3ba1841c5e3606233a2c0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="set-the-expiration-date-on-a-backup-sql-server"></a>設定備份的到期日 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中設定備份的到期日。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目，在備份上設定到期日：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 BACKUP DATABASE 和 BACKUP LOG 權限預設為 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。  
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶必須具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)並不會檢查檔案存取權限。 當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-the-expiration-date-on-a-backup"></a>若要在備份上設定到期日  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在 [物件總管] 中按一下伺服器名稱展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]**，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 **[工作]**，然後按一下 **[備份]**。 會出現 **[備份資料庫]** 對話方塊。  
  
4.  在 **[一般]** 頁面上的 **[備份組逾期時間]**，指定到期日以表示備份組可由其他備份覆寫的時間：  
  
    -   若要讓備份組在特定的天數後過期，請按一下 [之後] (預設選項)，然後輸入備份組建立之後將會過期的天數。 這個值可以介於 0 到 99999 日之間；值為 0 日意指備份組永遠不會過期。  
  
         預設值會在 **[伺服器屬性]** 對話方塊 ( **[資料庫設定]** 頁面) 的 **[預設備份媒體保留 (以天為單位)]** 選項中設定。 若要存取，請以滑鼠右鍵按一下物件總管中的伺服器名稱並選取 [屬性]，然後選取 [資料庫設定] 頁面。  
  
    -   若要讓備份組在特定日期過期，請按一下 **[於]**，然後輸入備份組將過期的日期。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-set-the-expiration-date-on-a-backup"></a>若要在備份上設定到期日  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  在 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 陳述式中，指定 EXPIREDATE 或 RETAINDAYS 選項，以決定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 何時可覆寫備份。 如果沒有指定任何選項，便會由 [media retention](../../database-engine/configure-windows/configure-the-media-retention-server-configuration-option.md) 伺服器組態設定來決定到期日。 此範例使用 `EXPIREDATE` 選項，指定到期日為 2015 年 6 月 30 日 (`6/30/2015`)。  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
 TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH EXPIREDATE = '6/30/2015' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)   
 [備份檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
  

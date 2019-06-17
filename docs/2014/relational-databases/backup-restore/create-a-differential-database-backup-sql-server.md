---
title: 建立差異資料庫備份 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full differential backups [SQL Server]
- database backups [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
- backups [SQL Server], creating
ms.assetid: 70f49794-b217-4519-9f2a-76ed61fa9f99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4be1c196adbe21635c1339da3d5ec7ca519001fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876596"
---
# <a name="create-a-differential-database-backup-sql-server"></a>建立差異資料庫備份 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立差異資料庫備份。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [必要條件](#Prerequisites)  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要使用下列項目建立差異資料庫備份：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   在明確或隱含的交易中，並不允許使用 BACKUP 陳述式。  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   建立差異資料庫備份時，需要有先前的完整資料庫備份存在。 如果從未備份過所選取的資料庫，在建立任何差異備份之前，請先執行完整資料庫備份。 如需詳細資訊，請參閱 [建立完整資料庫備份 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)中建立差異資料庫備份。  
  
###  <a name="Recommendations"></a> 建議  
  
-   隨著差異備份大小增加，還原差異備份會大幅增加還原資料庫所需的時間。 因此，建議您定期進行新的完整備份，為資料建立新的差異基底。 例如，您可能每週進行整個資料庫的完整備份 (亦即，完整資料庫備份)，然後在該週定期進行一連串的差異資料庫備份。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 BACKUP DATABASE 和 BACKUP LOG 權限預設為 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_backupoperator** 固定資料庫角色的成員。  
  
 備份裝置實體檔案的擁有權和權限問題可能會干擾備份作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須能夠讀取和寫入裝置；執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶必須具備寫入權限。 不過，在系統資料表中加入備份裝置項目的 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)並不會檢查檔案存取權限。 當您嘗試備份或還原時，存取實體資源之前不一定會出現備份裝置實體檔案的這些問題。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-differential-database-backup"></a>建立差異資料庫備份  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在 [物件總管] 中按一下伺服器名稱展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]** ，根據資料庫選取使用者資料庫或展開 **[系統資料庫]** ，然後選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 [工作]  ，然後按一下 [備份]  。 會出現 **[備份資料庫]** 對話方塊。  
  
4.  在 **[資料庫]** 清單方塊中確認資料庫名稱。 您可以選擇性從清單中選取不同的資料庫。  
  
     您可以為任何復原模式 (完整、大量記錄或簡單) 執行差異備份。  
  
5.  在 **[備份類型]** 清單方塊中，選取 **[差異]** 。  
  
    > [!IMPORTANT]  
    >  當**差異**已選取，請確認**只複製備份**核取方塊。  
  
6.  針對 **[備份元件]** ，按一下 **[資料庫]** 。  
  
7.  接受 **[名稱]** 文字方塊中建議的預設備份組名稱，或者輸入不同的備份組名稱。  
  
8.  (選擇性) 在 **[描述]** 文字方塊中輸入備份組的描述。  
  
9. 指定備份組會在何時過期：  
  
    -   若要讓備份組在特定的天數後過期，請按一下 **[之後]** (預設選項)，然後輸入備份組建立之後將會過期的天數。 這個值可以介於 0 到 99999 日之間；值為 0 日意指備份組永遠不會過期。  
  
         預設值會在 **[伺服器屬性]** 對話方塊 ( **[資料庫設定]** 頁面) 的 **[預設備份媒體保留 (以天為單位)]** 選項中設定。 若要存取，請以滑鼠右鍵按一下物件總管中的伺服器名稱並選取 [屬性]，然後選取 [資料庫設定]  頁面。  
  
    -   若要讓備份組在特定日期過期，請按一下 **[於]** ，然後輸入備份組將過期的日期。  
  
10. 按一下 **[磁碟]** 或 **[磁帶]** ，以選擇備份目的地的類型。 若要選取包含單一媒體集的磁碟或磁帶機 (最多 64 個) 的路徑，請按一下 **[加入]** 。 選取的路徑會在 **[備份至]** 清單方塊中顯示。  
  
     若要移除備份目的地，請選取目的地，然後按一下 **[移除]** 。 若要檢視備份目的地的內容，請選取目的地，然後按一下 **[內容]** 。  
  
11. 若要檢視或選取進階選項，請按一下 **[選取頁面]** 窗格中的 **[選項]** 。  
  
12. 按下列項目之一，以選取 **[覆寫媒體]** 選項：  
  
    -   **備份至現有的媒體集**  
  
         針對這個選項，按一下 **[附加至現有的備份組]** 或 **[覆寫所有現有的備份組]** 。 (選擇性) 選取 **[檢查媒體集名稱及備份組是否逾期]** 核取方塊，然後在 **[媒體集名稱]** 文字方塊中輸入名稱。 如果未指定名稱，就會建立一個空白名稱的媒體集。 如果您指定媒體集名稱，就會檢查媒體 (磁帶或磁碟)，以查看實際名稱是否與您在此處輸入的名稱相符。  
  
         如果您讓媒體名稱保持空白，並核取方塊以針對媒體進行檢查，成功也會使媒體上的媒體名稱保持空白。  
  
    -   **備份至新的媒體集，並清除所有現有的備份組**  
  
         針對這個選項，在 **[新媒體集名稱]** 文字方塊中輸入名稱，然後選擇性在 **[新媒體集描述]** 文字方塊中描述媒體集。  
  
13. (選擇性) 在 **[可靠性]** 區段中選取：  
  
    -   **[完成後驗證備份]** 。  
  
    -   **[寫入媒體之前執行總和檢查碼]** 及/或 **[發生總和檢查碼錯誤時繼續]** 。 如需總和檢查碼的詳細資訊，請參閱[在備份和還原期間可能的媒體錯誤 &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)。  
  
14. 如果是備份至磁帶機 (在 [一般]  頁面的 [目的地]  區段中指定)，[備份後卸載磁帶]  選項會啟用供選擇。 按一下這個選項會啟動 **[卸載之前倒轉磁帶]** 選項。  
  
    > [!NOTE]  
    >  除非您備份的是交易記錄檔 (依 [一般]  頁面的 [備份類型]  區段中的指定)，否則 [交易記錄檔]  區段中的選項為非使用中。  
  
15. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 和更新的版本支援 [備份壓縮](backup-compression-sql-server.md)。 依預設，備份壓縮與否取決於 **備份壓縮預設** 伺服器組態選項的值。 不過，不論目前的伺服器層級預設值為何，您都可以透過核取 **[壓縮備份]** 壓縮備份，而且可以透過核取 **[不要壓縮備份]** 防止壓縮。  
  
     **檢視目前的 backup compression default**  
  
    -   [檢視或設定 backup compression default 伺服器組態選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
    > [!NOTE]  
    >  或者，您可以使用「維護計畫精靈」來建立差異資料庫備份。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-differential-database-backup"></a>建立差異資料庫備份  
  
1.  執行 BACKUP DATABASE 陳述式以建立差異資料庫備份，請指定：  
  
    -   欲備份的資料庫名稱。  
  
    -   寫入完整資料庫備份的備份裝置。  
  
    -   DIFFERENTIAL 子句，指定只備份資料庫自上次進行完整資料庫備份後的變更部分。  
  
     必要的語法如下：  
  
     BACKUP DATABASE <資料庫名稱>  TO <備份裝置> WITH DIFFERENTIAL  
  
###  <a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 這個範例會建立 `MyAdvWorks` 資料庫的完整和差異資料庫備份。  
  
```sql  
-- Create a full database backup first.  
BACKUP DATABASE MyAdvWorks   
   TO MyAdvWorks_1   
   WITH INIT;  
GO  
-- Time elapses.  
-- Create a differential database backup, appending the backup  
-- to the backup device containing the full database backup.  
BACKUP DATABASE MyAdvWorks  
   TO MyAdvWorks_1  
   WITH DIFFERENTIAL;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [差異備份 &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [建立完整資料庫備份 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)   
 [備份檔案和檔案群組 &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [還原差異資料庫備份 &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)   
 [還原交易記錄備份 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [維護計畫](../maintenance-plans/maintenance-plans.md)   
 [完整檔案備份 &#40;SQL Server&#41;](full-file-backups-sql-server.md)  
  
  

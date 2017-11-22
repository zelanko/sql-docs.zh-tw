---
title: "以覆蓋現有檔案的方式還原檔案與檔案群組 (SQL Server) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- restoring files [SQL Server], how-to topics
- restoring files [SQL Server], steps
- file restores [SQL Server], how-to topics
- filegroups [SQL Server], restoring
- restoring filegroups [SQL Server]
- overwriting filegroups
- overwriting files
ms.assetid: 517e07eb-9685-4b06-90af-b1cc496700b7
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 072a1ce53f58de81e6cc212438525f340ba61bf4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="restore-files-and-filegroups-over-existing-files-sql-server"></a>以覆蓋現有檔案的方式還原檔案與檔案群組 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中以覆蓋現有檔案的方式還原檔案與檔案群組。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目，以覆蓋現有檔案的方式還原檔案與檔案群組：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   進行檔案與檔案群組還原的系統管理員，必須是目前唯一正在使用即將還原之資料庫的人。  
  
-   在明確或隱含的交易中，不允許使用 RESTORE。  
  
-   在完整或大量記錄復原模式下，您必須先備份使用中的交易記錄 (也稱為記錄的結尾)，才能還原檔案。 如需詳細資訊，請參閱 [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)中還原檔案與檔案群組。  
  
-   若要還原加密的資料庫，您必須能夠存取之前用來加密資料庫的憑證或非對稱金鑰。 如果沒有該憑證或非對稱金鑰，就無法還原資料庫。 因此，只要需要備份，就必須保留用來加密資料庫加密金鑰的憑證。 如需詳細資訊，請參閱 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 如果還原的資料庫不存在，使用者必須有 CREATE DATABASE 權限，才能執行 RESTORE。 如果資料庫存在，RESTORE 權限預設為 **系統管理員 (sysadmin)** 和 **資料庫建立者 (dbcreator)** 固定伺服器角色的成員以及資料庫的擁有者 (**dbo**) (對 FROM DATABASE_SNAPSHOT 選項而言，資料庫一律存在)。  
  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此，因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-restore-files-and-filegroups-over-existing-files"></a>若要以覆蓋現有檔案的方式還原檔案與檔案群組  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，展開該執行個體，然後展開 [資料庫] 。  
  
2.  以滑鼠右鍵按一下所要的資料庫，依序指向 [工作] 與 [還原]，然後按一下 [檔案與檔案群組]。  
  
3.  在 **[一般]** 頁面上的 **[目的地資料庫]** 清單方塊，輸入要還原的資料庫。 您可以輸入新的資料庫，或者從下拉式清單中選擇現有的資料庫。 清單包含伺服器上的所有資料庫，排除系統資料庫 **master** 和 **tempdb**。  
  
4.  若要指定要還原之備份組的來源與位置，請按一下下列任一個選項：  
  
    -   **來源資料庫**  
  
         在清單方塊中輸入資料庫名稱。 此清單僅包含已根據 **msdb** 備份記錄而備份的資料庫。  
  
    -   **來源裝置**  
  
         按一下 [瀏覽] 按鈕。 在 **[指定備份裝置]** 對話方塊中，選取 **[備份媒體類型]** 清單方塊上列出的其中一個裝置類型。 若要選取 **[備份媒體]** 清單方塊的一個或多個裝置，請按一下 **[加入]**。  
  
         將您要的裝置加入 **[備份媒體]** 清單方塊後，按一下 **[確定]** 即可回到 **[一般]** 頁面。  
  
5.  在 **[選取要還原的備份組]** 方格中，選取要還原的備份。 這個方格會顯示指定位置可用的備份。 依預設，會建議一個復原計畫。 若要覆寫建議的復原計畫，您可以變更方格中的選取項目。 任何相依於已取消選取備份的備份，會自動被取消選取。  
  
    |資料行標頭|值|  
    |-----------------|------------|  
    |**Restore**|選取的核取方塊會指出要還原的備份組。|  
    |**名稱**|備份組的名稱。|  
    |**檔案類型**|指定備份中的資料類型： **[資料]**、 **[記錄檔]**或 **[檔案資料流資料]**。 資料表中所包含的資料位於 **[資料]** 檔案中。 交易記錄資料位於 **[記錄檔]** 中。 儲存在檔案系統上的二進位大型物件 (BLOB) 資料位於 [Filestream 資料] 檔案中。|  
    |**型別**|執行的備份類型： **[完整]**、 **[差異]**或 **[交易記錄]**。|  
    |**Server**|執行備份作業的 Database Engine 執行個體名稱。|  
    |**檔案邏輯名稱**|檔案的邏輯名稱。|  
    |**資料庫**|備份作業中所含的資料庫名稱。|  
    |**開始日期**|備份作業開始時的日期和時間，會出現在用戶端的地區設定中。|  
    |**完成日期**|備份作業完成時的日期和時間，會出現在用戶端的地區設定中。|  
    |**大小**|備份組的大小 (以位元組為單位)。|  
    |**使用者名稱**|執行備份作業的使用者名稱。|  
  
6.  在 **[選取頁面]** 窗格中，按一下 **[選項]** 頁面。  
  
7.  在 [還原選項] 面板中，選取 [覆寫現有的資料庫 (WITH REPLACE)]。 還原作業會覆寫任何現有的資料庫及其相關檔案，即使已經有另一個資料庫或檔案具有相同名稱也一樣。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-restore-files-and-filegroups-over-existing-files"></a>若要以覆蓋現有檔案的方式還原檔案與檔案群組  
  
1.  執行 RESTORE DATABASE 陳述式以還原檔案及檔案群組備份，並指定以下項目：  
  
    -   所要還原的資料庫名稱。  
  
    -   將要還原完整資料庫備份的來源備份裝置。  
  
    -   替要還原的每個檔案指定 FILE 子句。  
  
    -   替要還原的每個檔案群組指定 FILEGROUP 子句。  
  
    -   REPLACE 選項，以指明可以用覆蓋相同名稱、相同位置之現有檔案的方式來還原每一個檔案。  
  
        > [!CAUTION]  
        >  請小心使用 REPLACE 選項。 若需相關資訊，請參閱 。  
  
    -   NORECOVERY 選項。 如果檔案在備份建立之後沒有做過任何修改，請指定 RECOVERY 子句。  
  
2.  如果檔案在備份建立之後做過修改，則請執行 RESTORE LOG 陳述式以套用交易記錄備份，並指定下列項目：  
  
    -   交易記錄檔要套用的資料庫名稱。  
  
    -   用於還原交易記錄備份的備份裝置。  
  
    -   倘若在目前的交易記錄備份之後還有另一個交易記錄備份要套用，請指定 NORECOVERY 子句，否則請指定 RECOVERY 子句。  
  
         您所套用的交易記錄備份必須涵蓋檔案和檔案群組備份的時間。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例還原 `MyNwind` 資料庫的檔案和檔案群組，並取代任何相同名稱的現有檔案。 同時還套用了兩份交易記錄，以便將資料庫還原到目前的時間。  
  
```tsql  
USE master;  
GO  
-- Restore the files and filesgroups for MyNwind.  
RESTORE DATABASE MyNwind  
   FILE = 'MyNwind_data_1',  
   FILEGROUP = 'new_customers',  
   FILE = 'MyNwind_data_2',  
   FILEGROUP = 'first_qtr_sales'  
   FROM MyNwind_1  
   WITH NORECOVERY,  
   REPLACE;  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [還原檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)   
 [使用備份與還原複製資料庫](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)  
  
  

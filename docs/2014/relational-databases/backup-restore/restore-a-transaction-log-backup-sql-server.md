---
title: 還原交易記錄備份 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoretlog.options.f1
- sql12.swb.restoretlog.general.f1
helpviewer_keywords:
- restore log
- backing up transaction logs [SQL Server], restoring
- transaction log backups [SQL Server], restoring
- restoring transaction logs [SQL Server], restoring backups
- transaction log restores [SQL Server], SQL Server Management Studio
ms.assetid: 1de2b888-78a6-4fb2-a647-ba4bf097caf3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a0cfc68f78ae9ca4022abfb59a33d756e82a6f2f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62875676"
---
# <a name="restore-a-transaction-log-backup-sql-server"></a>還原交易記錄備份 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中還原交易記錄備份。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [先決條件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要還原交易記錄備份，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   備份必須依照它們建立的順序還原。 在還原特定交易記錄備份之前，您必須先還原下列先前的備份，而不必回復未認可的交易，即 WITH NORECOVERY：  
  
    -   在特定交易記錄備份之前產生的完整資料庫備份與前次差異備份 (如果有的話)。 在建立完整或差異資料庫備份之前，資料庫必須已在使用完整復原模式或大量記錄復原模式。  
  
    -   在完整資料庫備份或差異備份 (如果您有還原其中一個) 之後及特定交易記錄備份之前產生的所有交易記錄備份。 必須依建立記錄備份的順序來套用記錄備份，且記錄鏈中沒有任何間距。  
  
         如需交易記錄備份的詳細資訊，請參閱[交易記錄備份 &#40;SQL Server &#41;](transaction-log-backups-sql-server.md) 和[套用交易記錄備份 &#40;SQL Server &#41;](apply-transaction-log-backups-sql-server.md)。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 RESTORE 權限提供給伺服器隨時可以取得其成員資格資訊的角色。 由於資料庫必須是可存取且未損毀，才能夠檢查固定資料庫角色成員資格，但執行 RESTORE 時未必如此；因此， **db_owner** 固定資料庫角色的成員並沒有 RESTORE 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
> [!WARNING]  
>  還原的一般程序是在 [還原資料庫]  對話方塊中選取記錄備份，還有資料與差異備份。  
  
#### <a name="to-restore-a-transaction-log-backup"></a>還原交易記錄備份  
  
1.  連線至適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在 [物件總管] 中按一下伺服器名稱，以展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]** ，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 [工作]  ，再指向 [還原]  ，然後按一下 [交易記錄]  ，這樣會開啟 [還原交易記錄]  對話方塊。  
  
    > [!NOTE]  
    >  如果 **[交易記錄]** 呈灰色，您可能需要先還原完整備份或差異備份。 使用 **[資料庫備份]** 對話方塊。  
  
4.  在 **[一般]** 頁面的 **[資料庫]** 清單方塊中，選取資料庫名稱。 只會列出處於正在還原狀態的資料庫。  
  
5.  若要指定要還原之備份組的來源與位置，請按一下下列任一個選項：  
  
    -   **從先前的資料庫備份**  
  
         從下拉式清單中選取要還原的資料庫。 此清單僅包含已根據 **msdb** 備份記錄而備份的資料庫。  
  
    -   **從檔案或磁帶**  
  
         按一下瀏覽 ( **...** ) 按鈕，開啟 [選取備份裝置]  對話方塊。 在 **[備份媒體類型]** 方塊中，選取列出的其中一種裝置類型。 若要選取 **[備份媒體]** 方塊中的一個或多個裝置，請按一下 **[加入]** 。  
  
         將您要的裝置加入 **[備份媒體]** 清單方塊後，按一下 **[確定]** 即可回到 **[一般]** 頁面。  
  
6.  在 **[選取要還原的交易記錄備份]** 方格中，選取要還原的備份。 此方格會列出選取的資料庫可用的交易記錄備份。 只有當資料庫的 **[第一個 LSN]** 大於 **[最後一個 LSN]** 時，才能使用記錄備份。 記錄備份會依它們所含的記錄序號 (LSN) 順序列出，而且必須按這個順序還原。  
  
     下表列出方格的各資料行標頭，並描述各標頭的值。  
  
    |頁首|值|  
    |------------|-----------|  
    |**Restore**|選取的核取方塊表示要還原的備份組。|  
    |**名稱**|備份組的名稱。|  
    |**元件**|備份的元件：**資料庫** **檔案**，或 \<空白> (適用於交易記錄)。|  
    |**Database**|執行備份所涉及的資料庫名稱。|  
    |**開始日期**|備份作業開始的日期和時間，以用戶端的區域設定表示。|  
    |**完成日期**|備份作業完成的日期和時間，以用戶端的區域設定表示。|  
    |**第一個 LSN**|備份組內第一筆交易的記錄序號。 針對檔案備份為空白。|  
    |**最後一個 LSN**|備份組內最後一個交易的記錄序號。 針對檔案備份為空白。|  
    |**檢查點 LSN**|在建立備份時，最近的檢查點之記錄序號。|  
    |**完整 LSN**|最近的完整資料庫備份之記錄序號。|  
    |**Server**|執行備份作業之 Database Engine 執行個體的名稱。|  
    |**使用者名稱**|執行備份作業之使用者的名稱。|  
    |**大小**|備份組的大小，以位元組為單位。|  
    |**位置**|備份組在磁碟區中的位置。|  
    |**到期**|備份組到期的日期和時間。|  
  
7.  選取下列其中一個：  
  
    -   **時間點**  
  
         保留預設值 ([最近可能的]  )，或按一下瀏覽按鈕，開啟 [還原時間點]  對話方塊，選取特定的日期和時間。  
  
    -   **標示的交易**  
  
         還原資料庫至先前標示的交易。 選取此選項會啟動 **[選取標示的交易]** 對話方塊，顯示一個方格，列出所選交易記錄備份中可用的已標示交易。  
  
         依預設，會還原到標示的交易，但是不含該交易。 若也要還原標示的交易，請選取 **[包含標示的交易]** 。  
  
         下表列出方格的各資料行標頭，並描述各標頭的值。  
  
        |頁首|值|  
        |------------|-----------|  
        |\<空白>|顯示選取標示的核取方塊。|  
        |**交易標示**|在認可交易時，由使用者所指定之標示交易的名稱。|  
        |**日期**|認可交易的日期和時間。 交易日期和時間是依照 **msdbgmarkhistory** 資料表中記錄的顯示，而非依照用戶端電腦的日期和時間。|  
        |**說明**|在認可交易時，由使用者所指定之標示交易的描述 (如果有的話)。|  
        |**LSN**|標示之交易的記錄序號。|  
        |**Database**|認可標示的交易之資料庫的名稱。|  
        |**使用者名稱**|認可標示的交易之資料庫使用者的名稱。|  
  
8.  若要檢視或選取進階選項，請按一下 **[選取頁面]** 窗格中的 **[選項]** 。  
  
9. 在 **[還原選項]** 區段中，選項如下：  
  
    -   **保留複寫設定 (WITH KEEP_REPLICATION)**  
  
         將發行資料庫還原至並非建立該資料庫的伺服器時，就會保留複寫設定。  
  
         這個選項只能搭配 [**回復未認可的交易，讓資料庫保持備**妥可用 ...] 選項使用（稍後會說明），這相當於使用`RECOVERY`選項還原備份。  
  
         核取此選項相當於在`KEEP_REPLICATION` [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE`語句中使用選項。  
  
    -   **還原每個備份之前先提示**  
  
         還原每個備份組之前 (第一個之後)，這個選項會帶出 [繼續還原]  對話方塊，其中會要求您指出是否要繼續還原順序。 這個對話方塊會顯示下一個媒體集名稱 (如果有)、備份組名稱，以及備份組描述。  
  
         您必須為不同的媒體集交換磁帶時，這個選項特別有用。 例如，您可以在伺服器只有一個磁帶裝置時使用。 等到您準備好繼續後，才能按一下 **[確定]** 。  
  
         按一下 **[否]** 會讓資料庫保持在還原狀態。 在上次的還原完成之後，您可以隨時繼續還原順序。 如果下一個備份是資料或差異備份，請再次使用 **[還原資料庫]** 工作。 如果下一個備份是記錄檔備份，請使用 **[還原交易記錄檔]** 工作。  
  
    -   **限制對還原資料庫的存取 (WITH RESTRICTED_USER)**  
  
         僅有 **db_owner**、 **dbcreator**或 **系統管理員**的成員可以使用還原資料庫。  
  
         核取此選項相當於在`RESTRICTED_USER` [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE`語句中使用選項。  
  
10. 針對 **[復原狀態]** 選項，指定資料庫在還原作業之後的狀態。  
  
    -   **回復未認可的交易，讓資料庫保持備妥可用。無法還原其他交易記錄。(RESTORE WITH RECOVERY)**  
  
         復原資料庫。 此選項相當於`RECOVERY` [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE`語句中的選項。  
  
         只有當您沒有任何要還原的記錄檔時，才選擇這個選項。  
  
    -   **讓資料庫保持不運作，且不回復未認可的交易。可以還原其他交易記錄。(RESTORE WITH NORECOVERY)**  
  
         讓資料庫處於無法復原狀態，也就是 `RESTORING` 的狀態。 此選項相當於在`NORECOVERY` [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE`語句中使用選項。  
  
         選擇這個選項時，將無法使用 **[保留複寫設定]** 選項。  
  
        > [!IMPORTANT]  
        >  若為鏡像或次要資料庫，請一律選取這個選項。  
  
    -   **讓資料庫保持唯讀模式。恢復未認可的交易，但是將恢復動作儲存在檔案中，以便能夠反轉復原結果。(RESTORE WITH STANDBY)**  
  
         讓資料庫處於待命狀態。 此選項相當於在`STANDBY` [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE`語句中使用選項。  
  
         您必須指定待命資料庫檔案，才能選擇此選項。  
  
11. 在 **[待命資料庫檔案]** 文字方塊中指定待命資料庫檔案 (選擇性)。 如果您讓資料庫處於唯讀模式，就需要指定此選項。 您可以瀏覽待命資料庫檔案，或者在文字方塊中輸入其路徑名稱。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
> [!IMPORTANT]  
>  我們建議您在每一個 RESTORE 陳述式中永遠明確指定 WITH NORECOVERY 或 WITH RECOVERY，以避免模稜兩可。 這在撰寫指令碼時尤其重要。  
  
#### <a name="to-restore-a-transaction-log-backup"></a>還原交易記錄備份  
  
1.  執行 RESTORE LOG 陳述式以套用交易記錄備份，請指定：  
  
    -   交易記錄檔要套用的資料庫名稱。  
  
    -   用於還原交易記錄備份的備份裝置。  
  
    -   NORECOVERY 子句。  
  
     此陳述式的基本語法如下：  
  
     RESTORE LOG *資料庫名稱* FROM <備份裝置> WITH NORECOVERY。  
  
     其中，*資料庫名稱* 為資料庫名稱，而 <備份裝置> 為裝置名稱 (內含要還原的記錄備份)。  
  
2.  對於需要套用的每個交易記錄備份，請重複步驟 1。  
  
3.  依還原順序還原最後一個備份之後，若要復原資料庫，請使用下列其中一個陳述式：  
  
    -   在最後一個 RESTORE LOG 陳述式之中復原資料庫：  
  
        ```  
        RESTORE LOG <database_name> FROM <backup_device> WITH RECOVERY;  
        GO  
        ```  
  
    -   使用不同的 RESTORE DATABASE 陳述式來等待復原資料庫：  
  
        ```  
        RESTORE LOG <database_name> FROM <backup_device> WITH NORECOVERY;   
        RESTORE DATABASE <database_name> WITH RECOVERY;  
        GO  
        ```  
  
         等待復原資料庫，可讓您有機會確認是否已經還原所有必要的記錄備份。 在執行時間點還原時，這個方法是較明智的。  
  
    > [!IMPORTANT]  
    >  如果您建立鏡像資料庫，請省略復原步驟。 鏡像資料庫必須保留 RESTORING 狀態。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 根據預設， [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫使用簡單復原模式。 此範例需要修改資料庫以使用完整復原模式，如下所示：  
  
```sql  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
```  
  
#### <a name="a-applying-a-single-transaction-log-backup"></a>A. 套用單一交易記錄備份  
 下列範例一開始會使用名為 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 備份裝置上的完整資料庫備份來還原 `AdventureWorks2012_1`資料庫。 此範例接著套用名為 `AdventureWorks2012_log`備份裝置上的第一個交易記錄備份。 最後，此範例復原了資料庫。  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorks2012_1  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 1,  
   WITH NORECOVERY;  
GO  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
#### <a name="b-applying-multiple-transaction-log-backups"></a>B. 套用多個交易記錄備份  
 下列範例一開始會使用名為 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 備份裝置上的完整資料庫備份來還原 `AdventureWorks2012_1`資料庫。 此範例接著逐一套用名為 `AdventureWorks2012_log`備份裝置上的前三個交易記錄備份。 最後，此範例復原了資料庫。  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorks2012_1  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 1,  
   NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 2,  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 3,  
   WITH NORECOVERY;  
GO  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [備份交易記錄 &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [還原資料庫備份 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [在完整復原模式下將資料庫還原至失敗點 &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   [還原資料庫至標示的交易 &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另請參閱  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [套用交易記錄備份 &#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md)  
  
  

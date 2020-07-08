---
title: 使用 SSMS 還原資料庫備份 | Microsoft 文件
description: 本文說明如何使用 SQL Server Management Studio 還原完整 SQL Server 資料庫備份。
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.locatebackupfileazure.f1
- sql13.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2e23cceab272e11eedb1fa99250dce5520ada073
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718014"
---
# <a name="restore-a-database-backup-using-ssms"></a>Restore a Database Backup Using SSMS
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  本主題說明如何使用 SQL Server Management Studio 還原完整資料庫備份。    
       
### <a name="important"></a>重要！    
您可能必須先備份使用中的交易記錄 (也稱為 [記錄結尾](tail-log-backups-sql-server.md))，才能在完整或大量記錄復原模式下還原資料庫。 如需詳細資訊，請參閱 [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)資料庫還原至新位置，並選擇性地重新命名資料庫。  

從另一個執行個體還原資料庫時，請考慮 [在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)中的資訊。   
    
若要還原加密的資料庫，您必須能夠存取用來加密該資料庫的憑證或非對稱金鑰。 如果沒有此憑證或非對稱金鑰，您就無法還原該資料庫。 只要您需要儲存備份，就必須保留用來加密資料庫加密金鑰的憑證。 如需詳細資訊，請參閱 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。    
    
如果您將舊版資料庫還原至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，該資料庫會自動升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 這可防止搭配 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 的較舊版本使用資料庫。 但是，這與中繼資料狀態相關，且不會影響[資料庫相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)。 如果使用者資料庫的相容性層級在升級前為 100 或更高層級，則在升級後仍會保持相同。 如果升級前的相容性層級為 90，則在升級後的資料庫中，相容性層級會設定為 100 (這是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]所支援的最低相容性層級)。 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
通常，資料庫立即變為可用。 不過，如果 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫具有全文檢索索引，升級程序就會根據 [全文檢索升級選項]  伺服器屬性的設定，匯入、重設或重建這些索引。 如果您將升級選項設定為 [匯入]  或 [重建]  ，則全文檢索索引在升級期間將無法使用。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建將需要十倍以上的時間。     
    
當您將升級選項設定為 [匯入]  時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。 如需有關檢視或變更 **全文檢索目錄升級選項** 屬性設定的詳細資訊，請參閱＜ [管理及監視伺服器執行個體的全文檢索搜尋](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)＞。    

如需從 Microsoft Azure Blob 儲存體服務還原 SQL Server 的資訊，請參閱[使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。

## <a name="examples"></a>範例
    
### <a name="a-restore-a-full-database-backup"></a>A. 還原完整資料庫備份   
    
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
    
2.  以滑鼠右鍵按一下 [資料庫]  ，然後選取 [還原資料庫...]     
    
3.  在 **[一般]** 頁面上，使用 **[來源]** 區段指定要還原之備份組的來源和位置。 選取下列其中一個選項：    
    
    -   **Database**    
    
         從下拉式清單中選取要還原的資料庫。 此清單僅包含已根據 **msdb** 備份記錄而備份的資料庫。    
    
        > [!NOTE]
        > 如果備份是根據不同的伺服器建立的，目的地伺服器就沒有指定之資料庫的備份記錄資訊。 在此情況下，請選取 **[裝置]** ，以便手動指定要還原的檔案或裝置。 
    
    -   **裝置**    
    
         按一下瀏覽 ( **...** ) 按鈕，開啟 [選取備份裝置]  對話方塊。 
         
        -   [選取備份裝置]  對話方塊  
        
            **備份媒體類型**  
         從 [備份媒體類型]  下拉式清單中選取媒體類型。  注意:只有在電腦上有掛載磁帶機時才會出現 **[磁帶]** 選項，而只有在至少有一個備份裝置時才會出現 **[備份裝置]** 選項。

            **加入**  
            依據您從 [備份媒體類型]  下拉式清單中選取的媒體類型，按一下 [加入]  就會開啟下列其中一個對話方塊。 (如果 [備份媒體]  清單方塊中的清單已滿，[加入]  按鈕便無法使用。)

            |媒體類型|對話方塊|描述|    
            |----------------|----------------|-----------------|    
            |**檔案**|**尋找備份檔案**|在這個對話方塊中，您可以從樹狀目錄中選取本機檔案，或是使用完整的通用命名慣例 (UNC) 名稱指定遠端檔案。 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。|    
            |**裝置**|**選取備份裝置**|在這個對話方塊中，您可以從伺服器執行個體上所定義的邏輯備份裝置清單中選取裝置。|    
            |**磁帶**|**選取備份磁帶**|在這個對話方塊中，您可以從實際連接到執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之電腦的磁帶機清單中選取磁帶。|    
            |**URL**|**選取備份檔案位置**|在此對話方塊中，您可以選取現有的 SQL Server 認證/Azure 儲存體容器、使用共用存取簽章新增 Azure 儲存體容器，或為現有的儲存體容器產生共用存取簽章和 SQL Server 認證。  另請參閱 [連接到 Microsoft Azure 訂用帳戶](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)|  
         
             **移除**    
             移除一個或多個選取的檔案、磁帶或邏輯備份裝置。    
                 
             **目錄**    
            顯示選取之檔案、磁帶或邏輯備份裝置的媒體內容。  如果媒體類型為 [URL]  ，此按鈕可能沒有作用。  

             **備份媒體**   
             列出選取的媒體。
    
             將您要的裝置加入 **[備份媒體]** 清單方塊後，按一下 **[確定]** 即可回到 **[一般]** 頁面。    
    
         在 **[來源：裝置：資料庫]** 清單方塊中，選取應該還原的資料庫名稱。    
    
         > [!NOTE]
         > 這份清單只能在選取 **[裝置]** 時使用。 只有在所選取裝置上有備份的資料庫才可供使用。    
     
4.  在 **[目的地]** 區段中，會將要還原之資料庫的名稱自動填入 **[資料庫]** 方塊。 若要變更資料庫的名稱，請在 **[資料庫]** 方塊中輸入新名稱。    
    
5.  在 **[還原至]** 方塊中，保留 **[到上次建立的備份]** 預設值，或按一下 **[時間表]** 存取 **[備份時間表]** 對話方塊，手動選取停止復原動作的時間點。 如需有關指定特定時間點的詳細資訊，請參閱＜ [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md)＞。    
    
6.  在 **[要還原的備份組]** 方格中，選取要還原的備份。 這個方格會顯示指定位置可用的備份。 依預設，會建議一個復原計畫。 若要覆寫建議的復原計畫，您可以變更方格中的選取項目。 取消選取先前的備份時，會自動取消選取相依於先前備份還原的備份。 如需 [要還原的備份組]  方格中各資料行的相關資訊，請參閱[還原資料庫 &#40;一般頁面&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)。    
    
7.  (選擇性) 按一下 **[選取頁面]** 窗格中的 **[檔案]** 存取 **[檔案]** 對話方塊。 如此，您就可以在 **[將資料庫檔案還原為]** 方格中，為每個檔案指定新的還原目的地，藉以將資料庫還原到新的位置。 如需這個方格的詳細資訊，請參閱[還原資料庫 &#40;檔案頁面&#41;](../../relational-databases/backup-restore/restore-database-files-page.md)。    
    
8. 若要檢視或選取進階選項，在 **[選項]** 頁面的 **[還原選項]** 面板中，您可以選取下列任何選項 (如果情況適用)：    

   1. **WITH** 選項 (非必要)：    
    
     - **覆寫現有的資料庫 (WITH REPLACE)**    
    
     - **保留複寫設定 (WITH KEEP_REPLICATION)**    
    
     - **限制對還原資料庫的存取 (WITH RESTRICTED_USER)**    
    
   2. 針對 **[還原狀態]** 方塊，選取選項。 此方塊決定資料庫在還原作業之後的狀態。    
    
     - **RESTORE WITH RECOVERY** 是預設行為，透過回復未認可的交易，讓資料庫保持備妥可用。 無法還原其他交易記錄。 若您要立即還原所有必要的備份，請選取這個選項。    
    
     - **RESTORE WITH NORECOVERY** ，讓資料庫保持不運作，且不回復未認可的交易。 可以還原其他交易記錄。 資料庫在復原之前都無法使用。    
    
     - **RESTORE WITH STANDBY** ，讓資料庫處於唯讀模式。 它會復原未認可的交易，但會將復原動作儲存在待命資料庫檔案中，以還原復原影響。    
    
   3. **還原前先進行結尾記錄備份。** 並不是所有的還原實例都需要結尾記錄備份。  如需詳細資訊，請參閱[結尾記錄備份 (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) 中的＜需要結尾記錄備份的實例＞  。
  
   4. 若資料庫有使用中的連接，還原作業可能會失敗。 核取 **[關閉現有的連接選項]** ，確定已關閉 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 與資料庫之間的所有使用中連接。 這個核取方塊會在執行還原作業之前將資料庫設定為單一使用者模式，並在完成後將資料庫設定為多使用者模式。    
  
   5. 如果想要系統在每個還原作業之間提示您，請選取 **[還原每個備份之前先提示]** 。 除非資料庫夠大，而且您想要監視還原作業的狀態，否則這通常不需要。    
    
如需這些還原選項的詳細資訊，請參閱 [還原資料庫 &#40;選項頁面&#41;](../../relational-databases/backup-restore/restore-database-options-page.md))，才能在完整或大量記錄復原模式下還原資料庫。    
    
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="b-restore-an-earlier-disk-backup-over-an-existing-database"></a>B. 以覆蓋現有資料庫的方式還原先前的磁碟備份
下列範例會還原先前對 `Sales` 執行的磁碟備份，並覆寫現有的 `Sales` 資料庫。

1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
2.  以滑鼠右鍵按一下 [資料庫]  ，然後選取 [還原資料庫...]   
3.  在 [一般]  頁面上，選取 [來源]  區段下的 [裝置]  。
4.  按一下瀏覽 ( **...** ) 按鈕，開啟 [選取備份裝置]  對話方塊。 按一下 [加入]  並巡覽至您的備份。 選取您的磁碟備份檔案，然後按一下 [確定]  。
5.  按一下 [確定]  回到 [一般]  頁面。
6.  在 [選取頁面]  窗格中，按一下 [選項]  。
7.  在 [還原選項]  區段下，核取 [覆寫現有的資料庫 (WITH REPLACE)]  。

    > [!NOTE]
    > 未選取此選項可能會導致下列錯誤訊息："System.Data.SqlClient.SqlError：備份組包含現有的 '`Sales`' 資料庫以外的資料庫備份。 (Microsoft.SqlServer.SmoExtended)」

8.  在 [結尾記錄備份]  區段下，取消核取 [還原前先進行結尾記錄備份]  。

    > [!NOTE]
    > 並不是所有的還原實例都需要結尾記錄備份。 如果復原點是包含在較早的記錄備份中，則不需要結尾記錄備份。 而且，如果您要移動或取代 (覆寫) 資料庫，而且不需要將它還原至最近備份之後的某個時間點，就不需要有結尾記錄備份。 如需詳細資訊，請參閱 [結尾記錄備份 (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。

    簡單復原模式下的資料庫無法使用此選項。

9.  在 [伺服器連接]  區段下，核取 [關閉目的地資料庫的現有連接]  。

    > [!NOTE]
    > 未選取此選項可能會導致下列錯誤訊息："System.Data.SqlClient.SqlError：無法獲得獨佔存取權，因為資料庫正在使用中。 (Microsoft.SqlServer.SmoExtended)」
    
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="c--restore-an-earlier-disk-backup-with-a-new-database-name-where-the-original-database-still-exists"></a>C.  在原始資料庫仍存在的情況下，使用新的資料庫名稱還原先前的磁碟備份
下列範例會還原先前對 `Sales` 執行的磁碟備份，並建立新的資料庫 `SalesTest`。  原始的資料庫 `Sales`仍存在於伺服器上。

1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
2.  以滑鼠右鍵按一下 [資料庫]  ，然後選取 [還原資料庫...]   
3.  在 [一般]  頁面上，選取 [來源]  區段下的 [裝置]  。
4.  按一下瀏覽 ( **...** ) 按鈕，開啟 [選取備份裝置]  對話方塊。 按一下 [加入]  並巡覽至您的備份。 選取您的磁碟備份檔案，然後按一下 [確定]  。
5.  按一下 [確定]  回到 [一般]  頁面。
6.  在 **[目的地]** 區段中，會將要還原之資料庫的名稱自動填入 **[資料庫]** 方塊。 若要變更資料庫的名稱，請在 **[資料庫]** 方塊中輸入新名稱。
7.  在 [選取頁面]  窗格中，按一下 [選項]  。
8.  在 [結尾記錄備份]  區段下，取消核取 [還原前先進行結尾記錄備份]  。

    > [!IMPORTANT]
    > 無法取消核取此選項將會導致現有的資料庫 `Sales`變更為正在還原狀態。

9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

    > [!NOTE]
    > 若您收到下列錯誤訊息：      
    > "System.Data.SqlClient.SqlError：資料庫 "`Sales`" 的記錄結尾尚未備份。 若其中包含您不想遺失的內容，請使用 `BACKUP LOG WITH NORECOVERY` 備份記錄。 亦可使用 `RESTORE` 陳述式的 `WITH REPLACE` 或 `WITH STOPAT` 子句來覆寫記錄的內容。 (Microsoft.SqlServer.SmoExtended)」。      
    > 則您可能未在上述步驟 6 中輸入新的資料庫名稱。 還原通常可以防止意外將資料庫覆寫成不同資料庫。 如果 `RESTORE` 陳述式中指定的資料庫已經存在於目前伺服器，而且所指定資料庫系列 GUID 與備份組中記錄的資料庫系列 GUID 不同，便不會還原資料庫。 這是重要的防護措施。

### <a name="d--restore-earlier-disk-backups-to-a-point-in-time"></a>D.  將先前的磁碟備份還原至某個時間點
下列範例會將資料庫還原至 `1:23:17 PM``May 30, 2016` 時的狀態，並顯示含有多個記錄備份的還原作業。 資料庫目前不在伺服器上。

1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
2.  以滑鼠右鍵按一下 [資料庫]  ，然後選取 [還原資料庫...]   
3.  在 [一般]  頁面上，選取 [來源]  區段下的 [裝置]  。
4.  按一下瀏覽 ( **...** ) 按鈕，開啟 [選取備份裝置]  對話方塊。 按一下 [加入]  並巡覽至您的完整備份及所有相關交易記錄備份。  選取您的磁碟備份檔案，然後按一下 [確定]  。
5.  按一下 [確定]  回到 [一般]  頁面。
6.  在 [目的地]  區段中，按一下 [時間表]  存取 [備份時間表]  對話方塊，手動選取停止復原動作的時間點。
7.  選取 [特定的日期與時間]  。  
8.  將 [時間表間隔]  變更為下拉式方塊中的 [小時] \(選擇性)。   
9.  將滑桿移至想要的時間。
10. 按一下 [確定]  回到 [一般] 頁面。
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="e--restore-a-backup-from-the-microsoft-azure-storage-service"></a>E.  從 Microsoft Azure 儲存體服務還原備份

#### <a name="common-steps"></a>通用步驟
下列兩個範例會從 Microsoft Azure 儲存體服務中的備份執行 `Sales` 的還原。  儲存體帳戶名稱為 `mystorageaccount`。  容器名稱為 `myfirstcontainer`。  為求簡潔，前六個步驟只會在此列出一次，所有範例將從**步驟 7** 開始進行。
1.  在物件總管  中，連接到 SQL Server Database Engine 的執行個體，然後展開該執行個體。
2.  以滑鼠右鍵按一下 [資料庫]  ，然後選取 [還原資料庫...]  。
3.  在 [一般]  頁面上，選取 [來源]  區段下的 [裝置]  。
4.  按一下瀏覽 (...) 按鈕，開啟 [選取備份裝置]  對話方塊。    
5.  從 [備份媒體類型:]  下拉式清單中選取 [URL]  。
6.  按一下 [加入]  ，[選取備份檔案位置]  對話方塊隨即開啟。

#### <a name="e1---restore-a-striped-backup-over-an-existing-database-and-a-shared-access-signature-exists"></a>E1.   以覆蓋現有資料庫的方式還原等量備份，而且存在共用存取簽章。
已建立具有讀取、寫入、刪除和列出權限的預存存取原則。  為容器 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`建立了與此預存存取原則相關聯的共用存取簽章。  如果 SQL Server 認證已經存在，則步驟大致相同。  資料庫 `Sales` 目前不在伺服器上。  備份檔案為 `Sales_stripe1of2_20160601.bak` 和 `Sales_stripe2of2_20160601.bak`。  

1.  如果 SQL Server 認證已經存在，請從 [Azure 儲存體容器:]  下拉式清單中選取 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`；否則請手動輸入容器 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` 的名稱。 
1. 在 [共用存取簽章:]  RTF 方塊中，輸入共用存取簽章。
1. 按一下 [確定]  ，[在 Microsoft Azure 中尋找備份檔案]  對話方塊隨即開啟。
1. 展開 [容器]  並巡覽至 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`。
1. 按住 Ctrl，然後選取檔案 `Sales_stripe1of2_20160601.bak` 和 `Sales_stripe2of2_20160601.bak`。
1. 按一下 [確定]  。
1. 按一下 [確定]  回到 [一般]  頁面。
1. 在 [選取頁面]  窗格中，按一下 [選項]  。
1. 在 [還原選項]  區段下，核取 [覆寫現有的資料庫 (WITH REPLACE)]  。
1. 在 [結尾記錄備份]  區段下，取消核取 [還原前先進行結尾記錄備份]  。
1. 在 [伺服器連接]  區段下，核取 [關閉目的地資料庫的現有連接]  。
1. 按一下 [確定]  。

#### <a name="e2---a-shared-access-signature-does-not-exist"></a>E2.   共用存取簽章不存在
在此範例中， `Sales` 資料庫目前不在伺服器上。
1. 按一下 [加入]  ，[連接至 Microsoft 訂用帳戶]  對話方塊隨即開啟。  
1. 完成 [連接至 Microsoft 訂用帳戶]  對話方塊，然後按一下 [確定]  回到 [選取備份檔案位置]  對話方塊。  如需其他資訊，請參閱[連接到 Microsoft Azure 訂用帳戶](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)。
1. 在 [選取備份檔案位置]  對話方塊中按一下 [確定]  ，[在 Microsoft Azure 中尋找備份檔案]  對話方塊隨即開啟。
1. 展開 [容器]  並巡覽至 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`。
1. 選取備份檔案，然後按一下 [確定]  。
1. 按一下 [確定]  回到 [一般]  頁面。
1. 按一下 [確定]  。

#### <a name="f-restore-local-backup-to-microsoft-azure-storage-url"></a>F. 將本機備份還原至 Microsoft Azure 儲存體 (URL)
`Sales` 資料庫將從 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` 中的備份還原至 Microsoft Azure 儲存體容器 `E:\MSSQL\BAK`。  已建立 Azure 容器的 SQL Server 認證。  目的地容器的 SQL Server 認證必須已經存在，因為您無法透過 **還原** 工作建立此認證。  `Sales` 資料庫目前不在伺服器上。
1.  在物件總管  中，連接到 SQL Server Database Engine 的執行個體，然後展開該執行個體。
2.  以滑鼠右鍵按一下 [資料庫]  ，然後選取 [還原資料庫...]  。
3.  在 [一般]  頁面上，選取 [來源]  區段下的 [裝置]  。
4.  按一下瀏覽 (...) 按鈕，開啟 [選取備份裝置]  對話方塊。  
5.  從 [備份媒體類型:]  下拉式清單中選取 [檔案]  。
6.  按一下 [加入]  ，[尋找備份檔案]  對話方塊隨即開啟。
7.  巡覽至 `E:\MSSQL\BAK` 並選取備份檔案，然後按一下 [確定]  。
8.  按一下 [確定]  回到 [一般]  頁面。
9.  在 [選取頁面]  窗格中，按一下 [檔案]  。
10. 核取 [將所有檔案重新放置到資料夾]  方塊。
11. 在 [資料檔案資料夾:]  和 [記錄檔資料夾:]  的文字方塊中，輸入容器 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`。
12. 按一下 [確定]  。

## <a name="see-also"></a>另請參閱    
 [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)     
 [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)     
 [將資料庫還原到新位置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)     
 [還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)     
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [還原資料庫 &#40;選項頁面&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)     
 [還原資料庫 &#40;一般頁面&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)    
    
  

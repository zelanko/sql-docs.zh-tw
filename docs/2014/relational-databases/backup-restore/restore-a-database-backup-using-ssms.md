---
title: 還原資料庫備份 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.locatebackupfileazure.f1
- sql12.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 521fc35b8ada4b1eb6c62e75fed4e1d9f99d21c4
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154783"
---
# <a name="restore-a-database-backup-sql-server-management-studio"></a>還原資料庫備份 (SQL Server Management Studio)
  本主題說明如何還原完整資料庫備份。  
  
> [!IMPORTANT]  
>  在完整或大量記錄復原模式下，您必須先備份使用中的交易記錄檔 (也稱為記錄檔的結尾)，才能在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中還原資料庫。 如需詳細資訊，請參閱 [備份交易記錄 &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)資料庫還原至新位置，並選擇性地重新命名資料庫。 若要還原加密的資料庫，您必須能夠存取之前用來加密資料庫的憑證或非對稱金鑰。 如果沒有該憑證或非對稱金鑰，就無法還原資料庫。 因此，只要需要備份，就必須保留用來加密資料庫加密金鑰的憑證。 如需詳細資訊，請參閱 [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md)。  
  
 請注意，如果您將 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本的資料庫還原成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，資料庫會自動升級。 通常，資料庫立即變為可用。 不過，如果 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫具有全文檢索索引，升級程序就會根據 [全文檢索升級選項] 伺服器屬性的設定，匯入、重設或重建這些索引。 如果升級選項設定為 [匯入] 或 [重建]，則全文檢索索引在升級期間將無法使用。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建可能需要十倍以上的時間。 此外，請注意，當升級選項設定為 [匯入] 時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。 如需有關檢視或變更 **全文檢索目錄升級選項** 屬性設定的詳細資訊，請參閱＜ [管理及監視伺服器執行個體的全文檢索搜尋](../search/manage-and-monitor-full-text-search-for-a-server-instance.md)＞。  
  
### <a name="to-restore-a-full-database-backup"></a>還原完整資料庫備份  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，請在 [物件總管] 中按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  展開 [資料庫]。 視資料庫而定，選取使用者資料庫，或者展開 [系統資料庫]，再選取系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫, 指向 [工作], 再指向 [**還原**], 然後按一下 [**資料庫**], 這會開啟 [**還原資料庫**] 對話方塊。  
  
4.  在 **[一般]** 頁面上，使用 **[來源]** 區段指定要還原之備份組的來源和位置。 選取下列其中一個選項：  
  
    -   **[資料庫備份]**  
  
         從下拉式清單中選取要還原的資料庫。 此清單僅包含已根據 **msdb** 備份記錄而備份的資料庫。  
  
    > [!NOTE]  
    >  如果備份是根據不同的伺服器建立的，目的地伺服器就沒有指定之資料庫的備份記錄資訊。 在此情況下，請選取 **[裝置]** ，以便手動指定要還原的檔案或裝置。  
  
    -   **[裝置]**  
  
         按一下瀏覽 ( **...** ) 按鈕，開啟 [選取備份裝置] 對話方塊。 在 **[備份媒體類型]** 方塊中，選取列出的其中一種裝置類型。 若要選取 **[備份媒體]** 方塊中的一個或多個裝置，請按一下 **[加入]** 。  
  
         將您要的裝置加入 **[備份媒體]** 清單方塊後，按一下 **[確定]** 即可回到 **[一般]** 頁面。  
  
         在 **[來源：裝置：資料庫]** 清單方塊中，選取應該還原的資料庫名稱。  
  
        > [!NOTE]  
        >  這份清單只能在選取 **[裝置]** 時使用。 只有在所選取裝置上有備份的資料庫才可供使用。  
  
         **備份媒體**  
         選取還原作業的媒體:檔案、**磁帶**、 **URL**或**備份裝置**。 只有在電腦上有掛載磁帶機時才會出現 **[磁帶]** 選項，而只有在至少有一個備份裝置時才會出現 **[備份裝置]** 選項。  
  
         **備份位置**  
         檢視、加入或移除還原作業的媒體。 清單最多可以包含 64 個檔案、磁帶或備份裝置。  
  
         **[加入]**  
         將備份裝置的位置新增至 [**備份位置**] 清單。 依據您在 **[備份媒體]** 欄位中選取的媒體類型，按一下 **[加入]** 就會開啟下列其中一個對話方塊。  
  
        |媒體類型|對話方塊|描述|  
        |----------------|----------------|-----------------|  
        |**檔案**|**尋找備份檔案**|在這個對話方塊中，您可以從樹狀目錄中選取本機檔案，或是使用完整的通用命名慣例 (UNC) 名稱指定遠端檔案。 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。|  
        |**裝置**|**選取備份裝置**|在這個對話方塊中，您可以從伺服器執行個體上所定義的邏輯備份裝置清單中選取裝置。|  
        |**Tape**|**選取備份磁帶**|在這個對話方塊中，您可以從實際連接到執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之電腦的磁帶機清單中選取磁帶。|  
        |**URL**|這會依下列順序啟動兩個對話方塊：<br /><br /> 1)**連接到 Azure 儲存體**<br /><br /> 2)**在 Azure 中尋找備份檔案**|在 [**連接到 Azure 儲存體**] 對話方塊中, 選取儲存 Azure 儲存體帳戶名稱和存取金鑰資訊的現有 sql 認證, 或指定儲存體帳戶名稱和儲存體存取金鑰資訊, 以建立新的 sql 認證。 如需詳細資訊, 請參閱[連接&#40;到&#41;Azure 儲存體還原](connect-to-microsoft-azure-storage-restore.md)。<br /><br /> 在 **[尋找備份檔案]** 對話方塊中，您可以從左框架所顯示的容器清單中選取檔案。|  
  
         如果清單已滿， **[加入]** 按鈕就無法使用。  
  
         **移除**  
         移除一個或多個選取的檔案、磁帶或邏輯備份裝置。  
  
         **目錄**  
         顯示選取之檔案、磁帶或邏輯備份裝置的媒體內容。  
  
5.  在 **[目的地]** 區段中，會將要還原之資料庫的名稱自動填入 **[資料庫]** 方塊。 若要變更資料庫的名稱，請在 **[資料庫]** 方塊中輸入新名稱。  
  
6.  在 **[還原至]** 方塊中，保留 **[到上次建立的備份]** 預設值，或按一下 **[時間表]** 存取 **[備份時間表]** 對話方塊，手動選取停止復原動作的時間點。 如需有關指定特定時間點的詳細資訊，請參閱＜ [Backup Timeline](backup-timeline.md)＞。  
  
7.  在 **[要還原的備份組]** 方格中，選取要還原的備份。 這個方格會顯示指定位置可用的備份。 依預設，會建議一個復原計畫。 若要覆寫建議的復原計畫，您可以變更方格中的選取項目。 取消選取先前的備份時，會自動取消選取相依於先前備份還原的備份。 如需 [要還原的備份組] 方格中各資料行的資訊，請參閱[還原資料庫 &#40;一般頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)。  
  
8.  (選擇性) 按一下 **[選取頁面]** 窗格中的 **[檔案]** 存取 **[檔案]** 對話方塊。 如此，您就可以在 **[將資料庫檔案還原為]** 方格中，為每個檔案指定新的還原目的地，藉以將資料庫還原到新的位置。 如需這個方格的詳細資訊，請參閱[還原資料庫 &#40;檔案頁面&#41;](restore-database-files-page.md)。  
  
9. 若要檢視或選取進階選項，在 **[選項]** 頁面的 **[還原選項]** 面板中，您可以選取下列任何選項 (如果情況適用)：  
  
    1.  `WITH` 選項 (非必要)：  
  
        -   **覆寫現有的資料庫 (WITH REPLACE)**  
  
        -   **保留複寫設定 (WITH KEEP_REPLICATION)**  
  
        -   **限制對還原資料庫的存取 (WITH RESTRICTED_USER)**  
  
    2.  針對 **[還原狀態]** 方塊，選取選項。 此方塊決定資料庫在還原作業之後的狀態。  
  
        -   **RESTORE WITH RECOVERY** 是預設行為，透過回復未認可的交易，讓資料庫保持備妥可用。 無法還原其他交易記錄。 若您要立即還原所有必要的備份，請選取這個選項。  
  
        -   **RESTORE WITH NORECOVERY** ，讓資料庫保持不運作，且不回復未認可的交易。 可以還原其他交易記錄。 資料庫在復原之前都無法使用。  
  
        -   **RESTORE WITH STANDBY** ，讓資料庫處於唯讀模式。 它會復原未認可的交易，但會將復原動作儲存在待命資料庫檔案中，以還原復原影響。  
  
    3.  如果選取的時間點需要 [還原前先進行結尾記錄備份]，則會予以選取。 您不需要修改這個設定，但是即使不需要，還是可以選擇備份記錄結尾。 在這裡的檔案名稱？ 如果 [**一般**] 頁面中的第一個備份組是在 Azure 中, 則結尾記錄也會備份至相同的儲存體容器。  
  
    4.  若資料庫有使用中的連接，還原作業可能會失敗。 核取 **[關閉現有的連接選項]** ，確定已關閉 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 與資料庫之間的所有使用中連接。 這個核取方塊會在執行還原作業之前將資料庫設定為單一使用者模式，並在完成後將資料庫設定為多使用者模式。  
  
    5.  如果想要系統在每個還原作業之間提示您，請選取 **[還原每個備份之前先提示]** 。 除非資料庫夠大，而且您想要監視還原作業的狀態，否則這通常不需要。  
  
     如需這些還原選項的詳細資訊，請參閱 [還原資料庫 &#40;選項頁面&#41;](restore-database-options-page.md))，才能在完整或大量記錄復原模式下還原資料庫。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [備份交易記錄 &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [建立完整資料庫備份 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)   
 [將資料庫還原到新位置 &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)   
 [還原交易記錄備份 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [還原資料庫 &#40;選項頁面&#41;](restore-database-options-page.md)   
 [還原資料庫 &#40;一般頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  

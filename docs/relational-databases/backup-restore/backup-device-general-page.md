---
title: 備份裝置 (一般頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backupdevice.general.f1
ms.assetid: c557e37d-319e-4adb-a0c1-94189b15d2ac
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2ba0a8ac8f1e008c4adc2e8206b900e53689ea9e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618926"
---
# <a name="backup-device-general-page"></a>備份裝置 (一般頁面)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 **[一般]** 頁面，可指定或檢視邏輯備份裝置的一般屬性。  
  
 **若要使用 SQL Server Management Studio 檢視備份裝置的內容**  
  
-   [檢視備份磁帶或檔案的內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>選項。  
 **裝置名稱**  
 檢視現有邏輯備份裝置的名稱，或是指定新邏輯備份裝置的名稱。  
  
 **磁帶**  
 在 [磁帶] 清單中檢視或選取目的地磁帶裝置。 只有當磁帶機已連接到執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]之執行個體的電腦上時，此選項才可以使用。  
  
> [!NOTE]  
>  遠端電腦上的磁帶備份裝置並不是有效的備份目的地。  
  
 **檔案**  
 檢視現有邏輯備份裝置的目的地檔案，或是指定新邏輯備份裝置的目的地檔案。  
  
-   如果是現有的邏輯備份裝置，則會顯示備份檔案的路徑。 **[檔案]** 欄位無法編輯，而且 [瀏覽] 按鈕無法使用。  
  
-   如果是新的邏輯備份裝置，您必須提供要定義邏輯備份裝置之備份檔案的路徑。 這個檔案目前尚不存在。  
  
     若要指定邏輯備份檔案，可以按一下 **[檔案]** 文字方塊右邊的 [瀏覽] 按鈕。 接著，您可以在 **[尋找資料庫檔案]** 對話方塊中，導覽至執行伺服器執行個體之電腦中任何固定磁碟機上的任何位置。 如果備份檔案尚不存在，則您必須在該對話方塊的 **[檔案名稱]** 欄位中輸入您要使用的檔名。  
  
     或者，您可以用手動方式編輯 **[檔案]** 欄位，以覆寫預設的路徑、檔案名稱和副檔名。 若要指定遠端檔案做為備份目的地，請輸入其完整的通用命名慣例 (UNC) 名稱。 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)之執行個體的電腦上時，此選項才可以使用。  
  
    > [!IMPORTANT]  
    >  透過網路備份資料可能會受到網路錯誤的影響，因此，建議您在備份作業完成之後要進行確認。 如需詳細資訊，請參閱 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks  
 單一媒體集是由一組一個或多個備份裝置上的備份所組成。 *「媒體集」* 是按順序排列的備份媒體集合 (磁帶或磁碟檔案)，由一個或多個的備份作業使用固定的備份裝置類型與數量寫入。 如需媒體集的一般資訊，請參閱 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)之執行個體的電腦上時，此選項才可以使用。  
  
 將媒體集中的第一個備份寫入邏輯備份裝置時，會初始化對應於邏輯備份裝置的實體備份裝置。 如果實體備份裝置是目前尚不存在的檔案，在初始化時便會建立該檔案。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [定義磁碟檔案的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [指定磁碟或磁帶作為備份目的地 &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [刪除備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [設定備份的到期日 &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [檢視備份磁帶或檔案的內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [檢視備份組中的資料和記錄檔 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [從裝置還原備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  

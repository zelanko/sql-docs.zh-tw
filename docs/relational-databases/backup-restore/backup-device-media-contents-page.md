---
title: "備份裝置 (媒體內容頁面) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.backupdevice.contents.f1
ms.assetid: 5fc7bd22-b6d8-4af1-8a58-2e7d0b994d08
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4bfa385cab6527c16e62e2e631b9ffa1b96e0d10
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="backup-device-media-contents-page"></a>備份裝置 (媒體內容頁面)
  使用 **[備份裝置]** 對話方塊來檢視備份資訊。 這個資訊描述裝置、媒體、媒體集，以及備份組。  
  
 **若要使用 SQL Server Management Studio 檢視備份裝置的內容**  
  
-   [檢視備份磁帶或檔案的內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>選項  
 檢視有關個別媒體、媒體集和備份組的資訊。  
  
 **媒體**  
 儲存備份資訊的磁碟或磁帶集。  
  
 **媒體順序**  
 列出媒體序號、家族序號，以及鏡像識別碼 (如果有的話)。 各個實體備份媒體都標記有媒體序號，指出媒體使用時的順序。 初始備份媒體會標記為 1，第二個 (第一個接續磁帶) 則會標記為 2，依此類推。 在還原備份組時，媒體序號可確保還原備份的操作員以正確的順序掛載正確的媒體。  
  
 **建立於**  
 顯示媒體集的建立日期和時間。  
  
 **媒體集**  
 媒體集是備份媒體的已排序集合，在其中使用固定數目的備份裝置寫入一個或多個備份作業。  
  
 **名稱**  
 顯示媒體集的名稱 (如果有的話)。  
  
 **說明**  
 顯示媒體集的描述 (如果有的話)。  
  
 **媒體家族計數**  
 顯示媒體集內的家族數目。 各個媒體集皆是一個或多個媒體家族的集合。 所有輸出到給定的單一備份裝置 (或鏡像的備份裝置群組)，即形成一個單一媒體家族。 每一個媒體集都會針對個別的裝置 (或鏡像裝置的群組) 組成一個媒體家族；例如，如果媒體集使用兩個非鏡像的備份裝置，媒體集就會包含兩個媒體家族。  
  
 **備份組**  
 顯示有關媒體上包含的備份組的資訊。 備份組是成功備份作業的結果，其內容會散發在備份裝置集的媒體上。  
  
|標頭|值|  
|------------|------------|  
|**名稱**|備份組的名稱。|  
|**型別**|已備份的物件：資料庫、檔案或 \<空白> (適用於交易記錄)。|  
|**元件**|執行的備份類型：完整、差異或交易記錄。|  
|**Server**|執行備份作業之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的名稱。|  
|**資料庫**|已備份資料庫的名稱。|  
|**位置**|備份組在磁碟區中的位置。|  
|**日期**|備份作業完成時的日期和時間，會出現在用戶端的地區設定中。|  
|**大小**|備份組的大小 (以位元組為單位)。|  
|**使用者名稱**|執行備份作業的使用者名稱。|  
|**到期**|備份組過期的日期和時間。|  
  
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
  
  

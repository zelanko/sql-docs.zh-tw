---
title: "選取備份目的地 | Microsoft Docs"
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
f1_keywords: sql13.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
caps.latest.revision: "33"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 08a629ac319f874312d6bb3878c721d783a5fe12
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="select-backup-destination"></a>選取備份目的地
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 [選取備份目的地] 對話方塊，即可選取裝置作為備份目的地。 備份目的地可以是磁碟或是邏輯備份裝置。  
  
 **若要使用 SQL Server Management Studio 備份資料庫**  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [備份檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>選項。  
 此對話方塊的選項，會視您選取的目的地是磁碟還是磁帶而定。  
  
 **磁碟上的目的地**  
 若要指定備份目的地，請選擇下列其中一個選項：  
  
|||  
|-|-|  
|**檔案名稱**|選擇這個選項，即可在文字方塊中輸入本機或遠端檔案做為備份目的地，以便：<br /><br /> 指定本機檔案，請按一下文字方塊右邊的瀏覽按鈕，並導覽至執行伺服器的電腦之固定磁碟機上的檔案，或是直接輸入完整路徑和檔案名稱；例如， `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`。<br /><br /> 指定遠端檔案做為備份目的地，請輸入其完整的通用命名慣例 (UNC) 名稱。 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)。<br /><br /> <br /><br /> **\*\* 重要 \*\*** 透過網路備份資料可能會受到網路錯誤的影響，因此，建議您在備份作業完成之後要進行驗證。 如需詳細資訊，請參閱 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。|  
|**備份裝置**|選擇這個選項，即可選取邏輯備份裝置。<br /><br /> 注意︰如需如何建立磁碟備份裝置的資訊，請參閱[定義磁碟檔案的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)。|  
  
 **磁帶上的目的地**  
 在磁帶機上指定備份目的地，此磁帶機實際連接到執行伺服器的電腦 (亦即 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體)。 請選擇下列其中一個選項：  
  
|||  
|-|-|  
|**磁帶機**|選擇這個選項，即可從實際連接到執行伺服器執行個體之電腦的磁帶機清單中選取磁帶機，做為備份目的地。<br /><br /> 注意：遠端電腦上的磁帶備份裝置並不是有效的備份目的地。|  
|**備份裝置**|選擇這個選項，即可選取現有的邏輯備份裝置。 這些邏輯備份裝置會對應至實際連接到執行伺服器執行個體之電腦的磁帶機。<br /><br /> 注意︰如需如何建立磁帶備份裝置的資訊，請參閱[定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  

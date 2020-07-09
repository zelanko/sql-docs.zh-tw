---
title: 選取備份目的地 | Microsoft Docs
description: 針對 SQL Server 還原，請使用 [選取備份目的地] 對話方塊，以選取磁碟或邏輯備份裝置作為備份目的地。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a7590bab8546dbc43e07cd88f6892d6cae6d4eda
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759090"
---
# <a name="select-backup-destination"></a>選取備份目的地
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  使用 [選取備份目的地]  對話方塊，即可選取裝置作為備份目的地。 備份目的地可以是磁碟或是邏輯備份裝置。  
  
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
|**檔案名稱**|選擇這個選項，即可在文字方塊中輸入本機或遠端檔案做為備份目的地，以便：<br /><br /> 指定本機檔案，請按一下文字方塊右邊的瀏覽按鈕，並導覽至執行伺服器的電腦之固定磁碟機上的檔案，或是直接輸入完整路徑和檔案名稱；例如， `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`。<br /><br /> 指定遠端檔案做為備份目的地，請輸入其完整的通用命名慣例 (UNC) 名稱。 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。<br /><br /> <br /><br /> **\*\* 重要 \*\*** 透過網路備份資料可能會受到網路錯誤的影響，因此，建議您在備份作業完成之後要進行驗證。 如需詳細資訊，請參閱 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)。|  
|**備份裝置**|選擇這個選項，即可選取邏輯備份裝置。<br /><br /> 注意:如需如何建立磁碟備份裝置的資訊，請參閱[定義磁碟檔案的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)。|  
  
 **磁帶上的目的地**  
 在磁帶機上指定備份目的地，此磁帶機實際連接到執行伺服器的電腦 (亦即 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體)。 請選擇下列其中一個選項：  
  
|||  
|-|-|  
|**磁帶機**|選擇這個選項，即可從實際連接到執行伺服器執行個體之電腦的磁帶機清單中選取磁帶機，做為備份目的地。<br /><br /> 注意:遠端電腦上的磁帶備份裝置並不是有效的備份目的地。|  
|**備份裝置**|選擇這個選項，即可選取現有的邏輯備份裝置。 這些邏輯備份裝置會對應至實際連接到執行伺服器執行個體之電腦的磁帶機。<br /><br /> 注意:如需如何建立磁帶備份裝置的資訊，請參閱[定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  

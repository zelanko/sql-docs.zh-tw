---
title: 選取備份目的地 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d9b4a0e07f32e074ff7e8875c263615bcebc12d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874873"
---
# <a name="select-backup-destination"></a>選取備份目的地
  使用 [選取備份目的地] 對話方塊，即可選取裝置作為備份目的地。 備份目的地可以是磁碟或是邏輯備份裝置。  
  
 **若要使用 SQL Server Management Studio 備份資料庫**  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [建立差異資料庫備份 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [備份檔案和檔案群組 &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>選項。  
 此對話方塊的選項，會視您選取的目的地是磁碟還是磁帶而定。  
  
 **磁碟上的目的地**  
 若要指定備份目的地，請選擇下列其中一個選項：  
  
|||  
|-|-|  
|**檔案名稱**|選擇這個選項，即可在文字方塊中輸入本機或遠端檔案，做為備份目的地。<br /><br /> 若要指定本機檔案，按一下 [瀏覽] 按鈕右邊的文字方塊中，瀏覽至執行伺服器之電腦的固定式磁碟機上的檔案或完整路徑和檔案名稱直接輸入;比方說， `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`。<br /><br /> 若要指定遠端檔案做為備份目的地，請輸入其完整的通用命名慣例 (UNC) 名稱。 如需詳細資訊，請參閱 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)執行個體上建立資料庫備份，就需要這個選項。<br /><br /> **\*\* 重要 \*\*** 透過網路備份資料可能會受到網路錯誤的影響，因此，建議您在備份作業完成之後要進行驗證。 如需詳細資訊，請參閱 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)。|  
|**備份裝置**|選擇這個選項，即可選取邏輯備份裝置。<br /><br /> 注意:如需有關如何建立磁碟備份裝置的資訊，請參閱 <<c0> [ 定義磁碟檔案的邏輯備份裝置&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)。</c0>|  
  
 **磁帶上的目的地**  
 在磁帶機上指定備份目的地，此磁帶機實際連接到執行伺服器的電腦 (亦即 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體)。 請選擇下列其中一個選項：  
  
|||  
|-|-|  
|**磁帶機**|選擇這個選項，即可從實際連接到執行伺服器執行個體之電腦的磁帶機清單中選取磁帶機，做為備份目的地。<br /><br /> 注意:遠端電腦上的磁帶備份裝置並不是有效的備份目的地。|  
|**備份裝置**|選擇這個選項，即可選取現有的邏輯備份裝置。 這些邏輯備份裝置會對應至實際連接到執行伺服器執行個體之電腦的磁帶機。<br /><br /> 注意:如需有關如何建立磁帶備份裝置的資訊，請參閱 <<c0> [ 定義磁帶機的邏輯備份裝置&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)。</c0>|  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [媒體集、媒體家族與備份組 &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  

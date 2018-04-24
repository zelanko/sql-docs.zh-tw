---
title: 使用備份與還原複製資料庫 | Microsoft 文件
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], back up and restore
- restoring databases [SQL Server], previous SQL Server versions
- database restores [SQL Server], copying databases
- restoring databases [SQL Server], onto another server instance
- restoring [SQL Server], onto another server instance
- backing up databases [SQL Server], copying databases
- database backups [SQL Server], copying databases
ms.assetid: b93e9701-72a0-408e-958c-dc196872c040
caps.latest.revision: 61
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: feccd83196b055f2f129164d609f8d976cc9f80b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="copy-databases-with-backup-and-restore"></a>使用備份與還原複製資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，您可以藉由還原使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本所建立的使用者資料庫備份，建立新的資料庫。 但是， **無法還原使用舊版**所建立的 **master** 、 **model** 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]備份。 此外，任何舊版 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 都無法還原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]備份。  
  
>**重要！** SQL Server 2016 使用與之前版本不同的預設路徑。 因此，若要還原舊版預設位置中建立的資料庫備份，您就必須使用 MOVE 選項。 如需有關新預設路徑的詳細資訊，請參閱 [SQL Server 的預設和具名執行個體的檔案位置](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)。 如需移動資料庫檔案的詳細資訊，請參閱本主題稍後的「移動資料庫檔案」。  
  
## <a name="general-steps-for-using-backup-and-restore-to-copy-a-database"></a>使用備份與還原來複製資料庫的一般步驟  
 當您使用備份與還原將資料庫複製到 SQL Server 的另一個執行個體時，來源和目的地電腦可為執行 SQL Server 的任何平台。  
  
 一般步驟如下：  
  
1.  備份來源資料庫，它可能在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本的執行個體上。 執行這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦稱為 **來源電腦**。  
  
2.  在要複製資料庫的目標電腦上 (即 **目的地電腦**)，請連接到您打算還原資料庫的 SQL Server 執行個體。 如有需要，請在 **目的地** 伺服器執行個體上建立與 **來源** 資料庫備份所用的相同備份裝置。  
  
3.  在 **目的地** 電腦上還原 **來源** 資料庫的備份。 還原資料庫會自動建立所有的資料庫檔案。  
  
某些可能會影響此處理序的其他注意事項：
  
## <a name="before-you-restore-database-files"></a>在還原資料庫檔案之前  
 還原資料庫會自動建立還原資料庫所需的資料庫檔案。 依預設，SQL Server 在還原處理期間所建立的檔案會使用與來源電腦上的原始資料庫中的備份檔案相同的名稱和路徑。  
  
 (選擇性) 在還原資料庫時，您可以指定還原資料庫的裝置對應、檔案名稱或路徑。 
 
 在下列狀況中，這可能是必要的步驟：  
  
-   原始電腦之資料庫所使用的目錄結構或磁碟機對應不存在其他電腦上。 例如，備份可能包含預設還原至 E 磁碟機的檔案，但目的地電腦沒有 E 磁碟機。  
  
-   目標位置可能空間不夠。  
  
-   您要重複使用存在還原目的地上的資料庫名稱，而且其任何檔案的名稱都與備份組中的資料庫檔案名稱相同，此時將發生下列其中一種情況：  
  
    -   如果可覆寫現有的資料庫檔案，系統就會覆寫此檔案 (這就不會影響屬於不同資料庫名稱的檔案)。  
  
    -   如果無法覆寫現有的檔案，就會發生還原錯誤。  
  
 為了避免錯誤和不愉快的結果，您可以在還原作業之前，使用 [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) 記錄資料表，在您計畫還原的備份中找出資料庫和記錄檔。  
  
## <a name="moving-the-database-files"></a>移動資料庫檔案  
 如果資料庫備份內的檔案無法還原至目的地電腦，則在還原檔案時必須將檔案移到新位置。 例如：  
  
-   您想要從建立於舊版預設位置的備份中還原資料庫。  
  
-   由於容量的因素，可能有必要將備份中的部分資料庫檔案還原至其他磁碟機。 這種情況很常見，因為組織內的大部分電腦不會擁有個數與大小一樣的磁碟機，以及完全一樣的軟體組態。  
  
-   可能有必要在同一部電腦上建立現有資料庫的副本，以供測試之用。 在這種情況下，原始資料庫的資料庫檔已存在，所以在還原過程中建立資料庫副本時必須指定不同的檔案名稱。  
  
 如需詳細資訊，請參閱本主題稍後的「將檔案與檔案群組還原至新的位置」。  
  
## <a name="changing-the-database-name"></a>變更資料庫名稱  
 將資料庫還原至目的電腦時可以變更資料庫的名稱，而不必先還原資料庫，然後手動變更名稱。 例如，可能必須將資料庫名稱從 **Sales** 改成 **SalesCopy** ，以指出這是資料庫的副本。  
  
 會自動使用您還原資料庫時明確提供的資料庫名稱做為新的資料庫名稱。 因為資料庫名稱尚未存在，所以會使用備份中的檔案建立新名稱。  
  
## <a name="when-upgrading-a-database-by-using-restore"></a>使用還原來升級資料庫時  
 從舊版還原備份時，事先知道備份中的每個全文檢索目錄路徑 (磁碟機和目錄) 是否存在於目的地電腦上會很有協助。 若要列出備份中每個檔案 (包括目錄檔案) 的邏輯名稱和實體名稱 (路徑和檔案名稱)，請使用 RESTORE FILELISTONLY FROM *<備份裝置>* 陳述式。 如需詳細資訊，請參閱 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)。  
  
 如果目的地電腦上並無相同路徑存在，則您有兩個替代方案：  
  
-   在目的地電腦上建立同等的磁碟機/目錄對應。  
  
-   在還原作業期間，在 RESTORE DATABASE 陳述式中使用 WITH MOVE 子句，將目錄檔案移到新位置。 如需詳細資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)備份。  
  
 如需升級全文檢索索引之替代選項的相關資訊，請參閱 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
  
## <a name="database-ownership"></a>資料庫擁有權  
 當資料庫在另一部電腦上還原時，初始還原作業的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者會自動變成新資料庫的擁有者。 還原資料庫時，系統管理員或新的資料庫擁有者可以變更資料庫擁有權。 若要防止未經授權的資料庫還原，請使用媒體或備份組密碼。  
  
## <a name="managing-metadata-when-restoring-to-another-server-instance"></a>還原至另一個伺服器執行個體時管理中繼資料  
 當您在另一個伺服器執行個體還原資料庫時，為了提供一致的經驗給使用者和應用程式，您可能需要在其他伺服器執行個體上為資料庫重新建立部分或全部的中繼資料，例如登入和作業。 如需詳細資訊，請參閱 [在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
 **檢視備份組中的資料與記錄檔**  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
 **將檔案與檔案群組還原至新的位置**  
  
-   [將檔案還原到新位置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **以覆蓋現有檔案的方式還原檔案與檔案群組**  
  
-   [以覆蓋現有檔案的方式還原檔案與檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
 **使用新名稱還原資料庫**  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **重新啟動中斷的還原作業**  
  
-   [重新啟動中斷的還原作業 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
 **變更資料庫擁有者**  
  
-   [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)  
  
 **使用 SQL Server 管理物件 (SMO) 複製資料庫**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadFileList%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.RelocateFiles%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReplaceDatabase%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
## <a name="see-also"></a>另請參閱  
 [複製資料庫至其他伺服器](../../relational-databases/databases/copy-databases-to-other-servers.md)   
 [SQL Server 的預設和具名執行個體的檔案位置](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  

---
title: 將報表伺服器資料庫移至其他電腦 (SSRS 原生模式) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 44a9854d-e333-44f6-bdc7-8837b9f34416
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 94cdbe6358bd0361addd70d682a3d0d41e70bbba
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50100219"
---
# <a name="moving-the-report-server-databases-to-another-computer-ssrs-native-mode"></a>將報表伺服器資料庫移至其他電腦 (SSRS 原生模式)

  您可以將安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所使用的報表伺服器資料庫，移至不同電腦上的執行個體。 但是，您必須一起移動或複製 reportserver 和 reportservertempdb 資料庫。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝需要這兩個資料庫。reportservertempdb 資料庫的名稱必須與所移動的主要 reportserver 資料庫相關。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式  
  
 移動資料庫不會影響目前已針對報表伺服器項目所定義的排程作業。  
  
-   當您第一次重新啟動報表伺服器服務時，便會重新建立排程。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。 雖然您不需要將這些作業移至新的電腦，但是可能會想要刪除電腦上不再使用的作業。  
  
-   移動的資料庫會保留訂閱、快取報表以及快照集。 如果快照集並未在移動資料庫之後收取重新整理過的資料，請在報表管理員中清除快照集選項，然後按一下 [套用] 儲存變更、重新建立排程，再按一下 [套用] 儲存變更。  
  
-   當您移動 reportservertempdb 資料庫時，系統會保留儲存在該資料庫中的暫存報表和使用者工作階段。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供數種移動資料庫的方法，包括備份與還原、附加與卸離，以及複製。 並不是所有方法都適合用來將現有資料庫重新放置到新的伺服器執行個體上， 移動報表伺服器資料庫的最佳方法會因您的系統可用性需求而有所差異。 移動報表伺服器資料庫最簡單的方式就是附加與卸離， 但是，如果要採用這種方法，您必須在卸離資料庫時將報表伺服器設定為離線狀態。 如果您希望能將服務中斷的情況降到最少，備份與還原就是比較好的選擇，但是您必須執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令來執行這些作業。 我們不建議利用複製資料庫來移動報表伺服器 (特別是使用「複製資料庫精靈」)，因為複製資料庫不會保留資料庫中的權限設定。  
  
> [!IMPORTANT]  
>  如果您對現有安裝所做的唯一變更是重新放置報表伺服器資料庫，就適用本主題中所提供的這些步驟。 移轉整個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝 (亦即，移動資料庫，並變更使用資料庫之報表伺服器 Windows 服務的識別) 需要重新設定連接和重設加密金鑰。  
  
## <a name="detaching-and-attaching-the-report-server-databases"></a>卸離及附加報表伺服器資料庫  
 如果您可以將報表伺服器設定為離線狀態，就可以卸離資料庫，並將資料庫移動到您要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 這種方式可以保留資料庫中的權限。 如果您要使用 SQL Server 資料庫，就必須將它移至另一個 SQL Server 執行個體。 移動資料庫之後，您必須重新設定報表伺服器與報表伺服器資料庫間的連接。 如果執行的是向外延伸部署，您必須重新設定部署中每個報表伺服器的報表伺服器資料庫連接。  
  
 請使用下列步驟來移動資料庫：  
  
1.  備份您想要移動之報表伺服器資料庫的加密金鑰。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來備份這些金鑰。  
  
2.  停止報表伺服器服務。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來停止這項服務。  
  
3.  啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 並開啟主控報表伺服器資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連接。  
  
4.  以滑鼠右鍵按一下報表伺服器資料庫，指向 [工作]，並按一下 [卸離]。 針對報表伺服器暫存資料庫重複此步驟。  
  
5.  複製或移動 .mdf 和 .ldf 檔案到您要使用之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 Data 資料夾。 因為移動的資料庫共有兩個，因此請確定您總共移動或複製四個檔案。  
  
6.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，開啟即將主控報表伺服器資料庫之新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連接。  
  
7.  以滑鼠右鍵按一下 [資料庫] 節點，然後按一下 [附加]。  
  
8.  按一下 **[加入]** ，選取您要附加之報表伺服器資料庫的 .mdf 和 .ldf 檔案。 針對報表伺服器暫存資料庫重複此步驟。  
  
9. 附加資料庫之後，請確認報表伺服器資料庫和暫存資料庫中具有 **RSExecRole** 資料庫角色， 而且**RSExecRole** 必須具有選取、插入、更新、刪除和參考報表伺服器資料庫資料表的權限，以及執行預存程序的權限。 如需詳細資訊，請參閱 [建立 RSExecRole](../../reporting-services/security/create-the-rsexecrole.md)。  
  
10. 啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並開啟報表伺服器的連接。  
  
11. 在 [資料庫] 頁面上，選取新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，然後按一下 **[連接]**。  
  
12. 選取您剛才移動的報表伺服器資料庫，然後按一下 **[套用]**。  
  
13. 在 [加密金鑰] 頁面上，按一下 [還原]。 指定包含金鑰備份副本的檔案以及解除鎖定此檔案的密碼。  
  
14. 重新啟動報表伺服器服務。  
  
## <a name="backing-up-and-restoring-the-report-server-databases"></a>備份及還原報表伺服器資料庫  
 如果無法將報表伺服器設定為離線狀態，您可以使用備份和還原來重新放置報表伺服器資料庫。 您必須使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式來進行備份和還原。 還原資料庫之後，您必須將報表伺服器設定為使用新伺服器執行個體上的資料庫。 如需詳細資訊，請參閱此主題結尾的指示。  
  
### <a name="using-backup-and-copyonly-to-backup-the-report-server-databases"></a>使用 BACKUP 和 COPY_ONLY 備份報表伺服器資料庫  
 備份資料庫時，請設定 COPY_ONLY 引數。 請務必同時備份資料庫以及記錄檔。  
  
```  
-- To permit log backups, before the full database backup, alter the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE ReportServer  
   SET RECOVERY FULL  
  
-- If the ReportServerData device does not exist yet, create it.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerData',   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\BACKUP\ReportServerData.bak'  
  
-- Create a logical backup device, ReportServerLog.  
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerLog',   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\BACKUP\ReportServerLog.bak'  
  
-- Back up the full ReportServer database.  
BACKUP DATABASE ReportServer  
   TO ReportServerData  
   WITH COPY_ONLY  
  
-- Back up the ReportServer log.  
BACKUP LOG ReportServer  
   TO ReportServerLog  
   WITH COPY_ONLY  
  
-- To permit log backups, before the full database backup, alter the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE ReportServerTempdb  
   SET RECOVERY FULL  
  
-- If the ReportServerTempDBData device does not exist yet, create it.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerTempDBData',   
'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\BACKUP\ReportServerTempDBData.bak'  
  
-- Create a logical backup device, ReportServerTempDBLog.  
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerTempDBLog',   
'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\BACKUP\ReportServerTempDBLog.bak'  
  
-- Back up the full ReportServerTempDB database.  
BACKUP DATABASE ReportServerTempDB  
   TO ReportServerTempDBData  
   WITH COPY_ONLY  
  
-- Back up the ReportServerTempDB log.  
BACKUP LOG ReportServerTempDB  
   TO ReportServerTempDBLog  
   WITH COPY_ONLY  
```  
  
### <a name="using-restore-and-move-to-relocate-the-report-server-databases"></a>使用 RESTORE 和 MOVE 重新放置報表伺服器資料庫  
 還原資料庫時，請務必包含 MOVE 引數，如此才能指定路徑。 使用 NORECOVERY 引數來執行初始還原；這樣子資料庫可以保持在還原狀態，讓您有時間可以預覽記錄備份，判斷要還原哪一個資料庫。 最後一個步驟會使用 RECOVERY 引數重複執行 RESTORE 作業。  
  
 MOVE 引數會使用資料檔案的邏輯名稱。 若要找出該邏輯名稱，請執行下列陳述式： `RESTORE FILELISTONLY FROM DISK='C:\ReportServerData.bak';`  
  
 下列範例中包含 FILE 引數，因此您可以指定要還原之記錄檔的檔案位置。 若要找出該檔案的位置，請執行下列陳述式： `RESTORE HEADERONLY FROM DISK='C:\ReportServerData.bak';`  
  
 還原資料庫和記錄檔時，您應該個別執行每個 RESTORE 作業。  
  
```  
-- Restore the report server database and move to new instance folder   
RESTORE DATABASE ReportServer  
   FROM DISK='C:\ReportServerData.bak'  
   WITH NORECOVERY,   
      MOVE 'ReportServer' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer.mdf',   
      MOVE 'ReportServer_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer_Log.ldf';  
GO  
  
-- Restore the report server log file to new instance folder   
RESTORE LOG ReportServer  
   FROM DISK='C:\ReportServerData.bak'  
   WITH NORECOVERY, FILE=2  
      MOVE 'ReportServer' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer.mdf',   
      MOVE 'ReportServer_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer_Log.ldf';  
GO  
  
-- Restore and move the report server temporary database  
RESTORE DATABASE ReportServerTempdb  
   FROM DISK='C:\ReportServerTempDBData.bak'  
   WITH NORECOVERY,   
      MOVE 'ReportServerTempDB' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServerTempDB.mdf',   
      MOVE 'ReportServerTempDB_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\REportServerTempDB_Log.ldf';  
GO  
  
-- Restore the temporary database log file to new instance folder   
RESTORE LOG ReportServerTempdb  
   FROM DISK='C:\ReportServerTempDBData.bak'  
   WITH NORECOVERY, FILE=2  
      MOVE 'ReportServerTempDB' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServerTempDB.mdf',   
      MOVE 'ReportServerTempDB_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\REportServerTempDB_Log.ldf';  
GO  
  
-- Perform final restore  
RESTORE DATABASE ReportServer  
   WITH RECOVERY  
GO  
  
-- Perform final restore  
RESTORE DATABASE ReportServerTempDB  
   WITH RECOVERY  
GO  
```  
  
### <a name="how-to-configure-the-report-server-database-connection"></a>如何設定報表伺服器資料庫連接  
  
1.  啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，並開啟報表伺服器的連接。  
  
2.  在 [資料庫] 頁面上，按一下 **[變更資料庫]**。 按 [下一步] 。  
  
3.  按一下 **[選擇現有報表伺服器資料庫]**。 按 [下一步] 。  
  
4.  選取現在主控報表伺服器資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然後按一下 **[測試連接]**。 按 [下一步] 。  
  
5.  在 [資料庫名稱] 中，選取您想要使用的報表伺服器資料庫。 按 [下一步] 。  
  
6.  在 [認證] 中，指定報表伺服器將用來連接至報表伺服器資料庫的認證。 按 [下一步] 。  
  
7.  按 **[下一步]** ，然後按一下 **[完成]**。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝會要求 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體必須包含 **RSExecRole** 角色。 當您透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具設定報表伺服器資料庫連接時，會產生角色建立、登入註冊以及角色指派等動作。 如果您使用其他方法 (尤其是使用 rsconfig.exe 命令提示字元公用程式) 來設定連接，報表伺服器將不會處於工作狀態。 您可能必須撰寫 WMI 程式碼，才能讓報表伺服器可供使用。 如需詳細資訊，請參閱 [存取 Reporting Services WMI 提供者](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)。  

## <a name="next-steps"></a>後續步驟

[建立 RSExecRole](../../reporting-services/security/create-the-rsexecrole.md)   
[啟動與停止 Report Server 服務](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
[設定報表伺服器資料庫連線](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[設定自動執行帳戶](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
[Reporting Services 組態管理員](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
[rsconfig 公用程式](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
[設定和管理加密金鑰](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
[報表伺服器資料庫](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)

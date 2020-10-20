---
description: 移動系統資料庫
title: 移動系統資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- moving system databases
- disaster recovery [SQL Server], moving database files
- database files [SQL Server], moving
- data files [SQL Server], moving
- tempdb database [SQL Server], moving
- system databases [SQL Server], moving
- scheduled disk maintenace [SQL Server]
- moving databases
- msdb database [SQL Server], moving
- moving database files
- relocating database files
- planned database relocations [SQL Server]
- master database [SQL Server], moving
- model database [SQL Server], moving
- Resource database [SQL Server]
- databases [SQL Server], moving
ms.assetid: 72bb62ee-9602-4f71-be51-c466c1670878
author: stevestein
ms.author: sstein
ms.openlocfilehash: c9edfd5b460a6a6b80900e1beced674b80bfce93
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195001"
---
# <a name="move-system-databases"></a>移動系統資料庫
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  本主題將描述如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中移動系統資料庫。 在下列狀況下移動系統資料庫可能非常有用：  
  
-   失敗復原。 例如，資料庫因硬體失敗而進入質疑模式或被關閉。  
  
-   計畫的重新放置。  
  
-   排程的磁碟維護重新放置。  
  
 下列程序適用於在相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體內移動資料庫檔案。 若要將資料庫移至另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體或移至另一部伺服器，請使用 [備份和還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) 作業。  

 本主題中的程序需要資料庫檔案的邏輯名稱。 若要取得該名稱，請查詢 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) 目錄檢視中的 name 資料行。  
  
> [!IMPORTANT]  
>  如果您移動了系統資料庫，接著重建 master 資料庫，就必須再次移動系統資料庫，因為重建作業會將所有系統資料庫安裝到預設的位置。  

> [!IMPORTANT]  
>  移動檔案之後， [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 服務帳戶必須具有權限來存取新檔案資料夾位置中的檔案。
    
  
##  <a name="planned-relocation-and-scheduled-disk-maintenance-procedure"></a><a name="Planned"></a> 計畫的重新放置與排程的磁碟維謢程序  
 若要以計畫的重新放置或排程的維護作業來移動系統資料庫資料或記錄檔，請遵照下列步驟執行。 此程序適用於 master 和 Resource 資料庫以外的所有系統資料庫。  
  
1.  對於要移動的每個檔案執行下列陳述式。  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name , FILENAME = 'new_path\os_file_name' )  
    ```  
  
2.  停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體或關閉系統以執行維護。 如需詳細資訊，請參閱 [启动、停止、暂停、继续、重启 SQL Server 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
3.  將一個或多個檔案移到新位置。  

4.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體或伺服器。 如需詳細資訊，請參閱 [启动、停止、暂停、继续、重启 SQL Server 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
5.  執行下列查詢以驗證檔案變更。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
 如果移動 msdb 資料庫，並針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Mail [設定了](../../relational-databases/database-mail/database-mail.md)的執行個體，請完成下列額外步驟。  
  
1.  透過執行下列查詢，確認已為 msdb 資料庫啟用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 。  
  
    ```  
    SELECT is_broker_enabled   
    FROM sys.databases  
    WHERE name = N'msdb';  
    ```  
  
     如需啟用 [!INCLUDE[ssSB](../../includes/sssb-md.md)]的詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)中移動系統資料庫。  
  
2.  透過傳送測試郵件，確認 Database Mail 是否可正常運作。  
  
##  <a name="failure-recovery-procedure"></a><a name="Failure"></a> 失敗復原程序  
 如果因為硬體失敗必須移動檔案，請遵照下列步驟將檔案重新放置到新位置。 此程序適用於 master 和 Resource 資料庫以外的所有系統資料庫。  
  
> [!IMPORTANT]  
>  如果無法啟動資料庫，也就是資料庫在質疑模式下或在無法復原的狀態下，只有 sysadmin 固定角色的成員可以移動檔案。  
  
1.  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體已經啟動，請將它停止。  
  
2.  在命令提示字元下輸入下列其中一個命令，以僅限 master 的復原模式啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 在這些命令中指定的參數要區分大小寫。 如果未依照所示指定參數，命令將會失敗。  
  
    -   如果是預設 (MSSQLSERVER) 執行個體，請執行下列命令：  
  
        ```  
        NET START MSSQLSERVER /f /T3608
        ```  
  
    -   如果是具名執行個體，請執行下列命令：  
  
        ```  
        NET START MSSQL$instancename /f /T3608
        ```  
  
     如需詳細資訊，請參閱 [启动、停止、暂停、继续、重启 SQL Server 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
3.  對於要移動的每個檔案，使用 **sqlcmd** 命令或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來執行下列陳述式。  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE( NAME = logical_name , FILENAME = 'new_path\os_file_name' )  
    ```  
  
     如需使用 **sqlcmd** 公用程式的詳細資訊，請參閱 [使用 sqlcmd 公用程式](../../ssms/scripting/sqlcmd-use-the-utility.md)。  
  
4.  結束 **sqlcmd** 公用程式或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
5.  停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 例如，請執行 `NET STOP MSSQLSERVER`。  
  
6.  將一個或多個檔案移到新位置。  
  
7.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 例如，請執行 `NET START MSSQLSERVER`。  
  
8.  執行下列查詢以驗證檔案變更。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
##  <a name="moving-the-master-database"></a><a name="master"></a> 移動 master 資料庫  
 若要移動 master 資料庫，請遵循下列步驟。  
  
1.  從 **[開始]** 功能表上，依序指向 **[程式集]** 、 **[Microsoft SQL Server]** 和 **[組態工具]** ，再按一下 **[SQL Server 組態管理員]** 。  
  
2.  在 **[SQL Server 服務]** 節點中，以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體 (例如 **[SQL Server (MSSQLSERVER)]** )，然後選擇 **[屬性]** 。  
  
3.  在 [SQL Server () 屬性] 對話方塊中，按一下 [啟動參數] 索引標籤。  
  
4.  在 [現有參數] 方塊中，選取 -d 參數來移動 master 資料檔案。 按一下 **[更新]** 來儲存變更。  
  
     在 [指定啟動參數] 方塊中，將參數變更為 master 資料庫的新路徑。  
  
5.  在 [現有參數] 方塊中，選取 -l 參數來移動 master 記錄檔。 按一下 **[更新]** 來儲存變更。  
  
     在 [指定啟動參數] 方塊中，將參數變更為 master 資料庫的新路徑。  
  
     資料檔案的參數值必須遵照 `-d` 參數，而記錄檔的值則必須遵照 `-l` 參數。 下列範例顯示 master 資料檔案的預設位置參數值。  
  
     `-dC:\Program Files\Microsoft SQL Server\MSSQL<version>.MSSQLSERVER\MSSQL\DATA\master.mdf`  
  
     `-lC:\Program Files\Microsoft SQL Server\MSSQL<version>.MSSQLSERVER\MSSQL\DATA\mastlog.ldf`  
  
     如果 master 資料檔案計畫的重新放置為 `E:\SQLData`，則必須將參數值變更如下：  
  
     `-dE:\SQLData\master.mdf`  
  
     `-lE:\SQLData\mastlog.ldf`  
  
6.  以滑鼠右鍵按一下執行個體名稱並選擇 [停止]，即可停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
7.  將 master.mdf 和 mastlog.ldf 檔移至新位置。  
  
8.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  
  
9. 執行下列查詢，驗證 master 資料庫的檔案變更。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID('master');  
    GO  
    ```  

10. SQL Server 目前應該會正常執行。 不過，Microsoft 也建議調整 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\instance_ID\Setup`的登錄項目，其中 *instance_ID* 就像 `MSSQL13.MSSQLSERVER`。 在該登錄區中，將 `SQLDataRoot` 值變更為新路徑。 更新登錄失敗可能會導致無法修補和升級。

  
##  <a name="moving-the-resource-database"></a><a name="Resource"></a> 移動 Resource 資料庫  
 Resource 資料庫的位置是 \<*drive*>:\Program Files\Microsoft SQL Server\MSSQL\<version>.\<*instance_name*>\MSSQL\Binn\\。 此資料庫無法移動。  
  
##  <a name="follow-up-after-moving-all-system-databases"></a><a name="Follow"></a> 後續操作：移動所有系統資料庫之後  
 如果您將所有系統資料庫移動至新的磁碟機或磁碟區，或是移動至使用不同磁碟機代號的另一部伺服器，請進行下列更新。  
  
-   變更 SQL Server Agent 記錄路徑。 如果您未更新此路徑，SQL Server Agent 將無法啟動。  
  
-   變更資料庫預設位置。 如果指定為預設位置的磁碟機代號和路徑不存在，則建立新資料庫可能會失敗。  
  
#### <a name="change-the-sql-server-agent-log-path"></a>變更 SQL Server Agent 記錄路徑  
  
1.  從 SQL Server Management Studio，在 [物件總管] 中展開 **[SQL Server Agent]** 。  
  
2.  以滑鼠右鍵按一下 **[錯誤記錄檔]** ，然後按一下 **[設定]** 。  
  
3.  在 **[設定 SQL Server Agent 錯誤記錄檔]** 對話方塊中，指定 SQLAGENT.OUT 檔的新位置。 預設位置是 C:\Program Files\Microsoft SQL Server\MSSQL\<version>.<執行個體名稱>\MSSQL\Log\\。  
  
#### <a name="change-the-database-default-location"></a>變更資料庫預設位置  
  
1.  從 SQL Server Management Studio，在 [物件總管] 中以滑鼠右鍵按一下 SQL Server 伺服器，然後按一下 **[屬性]** 。  
  
2.  在 **[伺服器屬性]** 對話方塊中，選取 **[資料庫設定]** 。  
  
3.  在 **[資料庫預設位置]** 底下，瀏覽至資料和記錄檔的新位置。  
  
4.  停止 SQL Server 服務然後啟動它來完成變更。  
  
##  <a name="examples"></a><a name="Examples"></a> 範例  
  
### <a name="a-moving-the-tempdb-database"></a>A. 移動 tempdb 資料庫  
 下列範例會以計畫的重新放置，將 `tempdb` 資料和記錄檔移到新位置。  
  
> [!NOTE]  
>  由於在每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時都會重新建立 tempdb，因此您不需要實際移動資料和記錄檔。 在步驟 3 重新啟動此服務時，將會在新位置建立檔案。 在重新啟動服務之前，tempdb 將繼續使用現有位置中的資料和記錄檔。  
  
1.  判斷 `tempdb` 資料庫的邏輯檔案名稱以及它們目前的磁碟位置。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'tempdb');  
    GO  
    ```  
  
2.  請利用 `ALTER DATABASE`來變更每個檔案的位置。  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = templog, FILENAME = 'F:\SQLLog\templog.ldf');  
    GO  
    ```  
  
3.  停止和重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。  
  
4.  確認檔案變更。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'tempdb');  
    ```  
  
5.  從原始位置刪除 `tempdb.mdf` 和 `templog.ldf` 檔案。  
  
## <a name="see-also"></a>另請參閱  
 [Resource 資料庫](../../relational-databases/databases/resource-database.md)   
 [tempdb 資料庫](../../relational-databases/databases/tempdb-database.md)   
 [master 資料庫](../../relational-databases/databases/master-database.md)   
 [msdb 資料庫](../../relational-databases/databases/msdb-database.md)   
 [Model 資料庫](../../relational-databases/databases/model-database.md)   
 [移動使用者資料庫](../../relational-databases/databases/move-user-databases.md)   
 [移動資料庫檔案](../../relational-databases/databases/move-database-files.md)   
 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [重建系統資料庫](../../relational-databases/databases/rebuild-system-databases.md)  
  

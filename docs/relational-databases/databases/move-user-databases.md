---
description: 移動使用者資料庫
title: 移動使用者資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- database files [SQL Server], moving
- data files [SQL Server], moving
- editions [SQL Server], moving databases between
- moving full-text catalogs
- scheduled disk maintenace [SQL Server]
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- moving user databases
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: ad9a4e92-13fb-457d-996a-66ffc2d55b79
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0892e0a2a6db25e6a82f56177544572b8a5af388
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471210"
---
# <a name="move-user-databases"></a>移動使用者資料庫
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您可以在 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式的 FILENAME 子句中指定新的檔案位置，以便將使用者資料庫的資料、記錄和全文檢索目錄檔案移到新位置。 這種方法適用於在相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體內移動資料庫檔案。 若要將資料庫移到另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體或移到另一個伺服器，請使用 [備份和還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) 或 [卸離和附加作業](../../relational-databases/databases/move-a-database-using-detach-and-attach-transact-sql.md)。  
  
## <a name="considerations"></a>考量  
 將資料庫移動到其他伺服器執行個體，以提供一致的經驗給使用者和應用程式時，您可能必須為資料庫重新建立部分或全部的中繼資料。 如需詳細資訊，請參閱 [在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的某些功能會變更 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將資訊儲存在資料庫檔案中的方式， 這些功能受限為特定版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 包含這些功能的資料庫無法移至不支援它們的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 您可以使用 sys.dm_db_persisted_sku_features 動態管理檢視來列出目前資料庫中啟用的所有版本特有功能。  
  
 本主題中的程序需要資料庫檔案的邏輯名稱。 若要取得該名稱，請查詢 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) 目錄檢視中的 name 資料行。  
  
 從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]開始，全文檢索目錄會整合到儲存於檔案系統中的資料庫。 現在當您移動資料庫時，全文檢索目錄會自動移動。  
  
## <a name="planned-relocation-procedure"></a>計畫的重新放置程序  
 若要依照計畫的重新放置來移動資料或記錄檔，請遵循下列步驟：  
  
1.  執行下列陳述式。  
  
    ```  
    ALTER DATABASE database_name SET OFFLINE;  
    ```  
  
2.  將一個或多個檔案移到新位置。  
  
3.  對於移動的每個檔案，執行下列陳述式。  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name, FILENAME = 'new_path\os_file_name' );  
    ```  
  
4.  執行下列陳述式。  
  
    ```  
    ALTER DATABASE database_name SET ONLINE;  
    ```  
  
5.  執行下列查詢以驗證檔案變更。  

    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="relocation-for-scheduled-disk-maintenance"></a>排程的磁碟維謢重新放置  
 若要在排程的磁碟維護程序中重新放置檔案，請遵循下列步驟：  
  
1.  對於要移動的每個檔案執行下列陳述式。  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name , FILENAME = 'new_path\os_file_name' );  
    ```  
  
2.  停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體或關閉系統以執行維護。 如需詳細資訊，請參閱 [启动、停止、暂停、继续、重启 SQL Server 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
3.  將一個或多個檔案移到新位置。  
  
4.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體或伺服器。 如需詳細資訊，請參閱 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
5.  執行下列查詢以驗證檔案變更。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="failure-recovery-procedure"></a>失敗復原程序  
 如果因為硬體失敗必須移動檔案，請遵循下列步驟將檔案重新放置到新位置。  
  
> [!IMPORTANT]  
>  如果無法啟動資料庫，也就是資料庫在質疑模式下或在無法復原的狀態下，只有 sysadmin 固定角色的成員可以移動檔案。  
  
1.  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體已經啟動，請將它停止。  
  
2.  在命令提示字元下輸入下列其中一個命令，以僅限 master 的復原模式啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
    -   如果是預設 (MSSQLSERVER) 執行個體，請執行下列命令。  
  
        ```  
        NET START MSSQLSERVER /f /T3608  
        ```  
  
    -   如果是具名執行個體，請執行下列命令。  
  
        ```  
        NET START MSSQL$instancename /f /T3608  
        ```  
  
     如需詳細資訊，請參閱 [启动、停止、暂停、继续、重启 SQL Server 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
3.  對於要移動的每個檔案，使用 **sqlcmd** 命令或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來執行下列陳述式。  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE( NAME = logical_name , FILENAME = 'new_path\os_file_name' );  
    ```  
  
     如需如何使用 **sqlcmd** 公用程式的詳細資訊，請參閱 [使用 sqlcmd 公用程式](../../relational-databases/scripting/sqlcmd-use-the-utility.md)。  
  
4.  結束 **sqlcmd** 公用程式或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
5.  停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  
  
6.  將一個或多個檔案移到新位置。  
  
7.  啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 例如，請執行： `NET START MSSQLSERVER`。  
  
8.  執行下列查詢以驗證檔案變更。  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="examples"></a>範例  
 下列範例會以計畫的重新放置，將 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 記錄檔移到新位置。  
  
```  
USE master;  
GO  
-- Return the logical file name.  
SELECT name, physical_name AS CurrentLocation, state_desc  
FROM sys.master_files  
WHERE database_id = DB_ID(N'AdventureWorks2012')  
    AND type_desc = N'LOG';  
GO  
ALTER DATABASE AdventureWorks2012 SET OFFLINE;  
GO  
-- Physically move the file to a new location.  
-- In the following statement, modify the path specified in FILENAME to  
-- the new location of the file on your server.  
ALTER DATABASE AdventureWorks2012   
    MODIFY FILE ( NAME = AdventureWorks2012_Log,   
                  FILENAME = 'C:\NewLoc\AdventureWorks2012_Log.ldf');  
GO  
ALTER DATABASE AdventureWorks2012 SET ONLINE;  
GO  
--Verify the new location.  
SELECT name, physical_name AS CurrentLocation, state_desc  
FROM sys.master_files  
WHERE database_id = DB_ID(N'AdventureWorks2012')  
    AND type_desc = N'LOG';  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [移動系統資料庫](../../relational-databases/databases/move-system-databases.md)   
 [移動資料庫檔案](../../relational-databases/databases/move-database-files.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  

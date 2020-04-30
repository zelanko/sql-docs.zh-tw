---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: b885504d8431be2df9ab0c841b47fe0eb7019932
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728635"
---
# <a name="mssqlserver_17207"></a>MSSQLSERVER_17207
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|17207|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBLKIO_OS2DISKERROR|  
|訊息文字|%ls:建立或開啟檔案 '%ls' 時發生作業系統錯誤 %ls。 請診斷並更正作業系統錯誤，然後重試此作業。|  


## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法開啟指定的檔案，因為發生指定的 OS 錯誤。  

當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法開啟資料庫和/或交易記錄檔時，您可能會在 Windows 應用程式事件或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中看見錯誤 17207。 此錯誤的外觀範例如下所示：

``` 
Error: 17207, Severity: 16, State: 1.
FileMgr::StartSecondaryDataFiles: Operating system error 2(The system cannot find the file specified.) occurred while creating or opening file 'F:\MSSQL\DATA\MyDB_FG1_1.ndf'. Diagnose and correct the operating system error, and retry the operation.
```

您可能會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的啟動程序期間，或是嘗試啟動資料庫的任何 Database 作業 (例如 ALTER DATABASE) 期間看見這些錯誤。 在某些情況下，您可能會同時看見 17207 和 17204 錯誤，而在其他情況下則只看見其中一個錯誤。

如果使用者資料庫遇到這些錯誤，該資料庫將會處於 RECOVERY_PENDING 狀態，且應用程式將無法存取該資料庫。 如果系統資料庫遇到這些錯誤，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體將無法啟動，且您將無法連線到這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 這也可能會導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集資源離線。

如果問題與您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FileStream 檔案群組相關，您將會注意到系統只會列出完整目錄路徑，而非檔案名稱。 範例如下所示： 
```
Error: 17207, Severity: 16, State: 1.
STREAMFCB::Startup: Operating system error 2(The system cannot find the file specified.) occurred while creating or opening file 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\bpa_files_test_fs_1\bpa_files_test_fs_1'. Diagnose and correct the operating system error, and retry the operation.
```

## <a name="cause"></a>原因
在可以使用任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫之前，該資料庫必須先啟動。 資料庫啟動程序會涉及初始化代表資料庫和資料庫檔案的各種資料結構，開啟屬於資料庫的所有檔案，最後再於資料庫上執行復原。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 [CreateFile](https://docs.microsoft.com/windows/win32/api/fileapi/nf-fileapi-createfilea) \(英文\) Windows API 函式來開啟屬於某個資料庫的檔案。
 
訊息 17207 (和 17204) 指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在啟動程序期間嘗試開啟資料庫檔案時發生錯誤。
 
這些錯誤訊息包含下列資訊：
1. 嘗試開啟檔案之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 函式的名稱。 您通常會在這些錯誤訊息中觀察到下列其中之一的函式名稱：
   - FCB::Open                              - 檔案在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 嘗試加以開啟時發生錯誤
   - FileMgr::StartPrimaryDataFiles         - 屬於主要檔案群組的主要資料檔案或檔案
   - FileMgr::StartSecondaryDataFiles       - 屬於次要檔案群組的檔案
   - FileMgr::StartLogFiles                 - 交易記錄檔
   - STREAMFCB::Startup                     - SQL FileStream 容器
   - FCB::RemoveAlternateStreams
  
      
1. 狀態資訊能區分出函式內可能產生此錯誤訊息的多個位置
1. 檔案的完整實體路徑
1. 對應至檔案的檔案識別碼
1. 作業系統錯誤碼和錯誤描述。 在某些情況下，您只會看見錯誤碼。
 
列印在這些錯誤訊息中的作業系統錯誤資訊，是導致錯誤 17204 的根本原因。 導致這些錯誤訊息的常見原因為權限問題或不正確的檔案路徑。


## <a name="user-action"></a>使用者動作  
1. 解決錯誤 17207 須涉及了解相關聯的作業系統錯誤碼並診斷該錯誤。 在解決作業系統錯誤條件之後，您便可以嘗試重新啟動資料庫 (例如使用 ALTER DATABASE SET ONLINE) 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來使受影響的資料庫上線。 在某些情況下，您可能會無法解決作業系統錯誤。 在那種情況下，您必須採取特定的矯正措施。 我們將在此節中討論這些動作。
1. 如果 17207 錯誤訊息僅包含錯誤碼，而沒有錯誤描述，您可以嘗試從作業系統殼層使用命令來解決錯誤碼：net helpmsg <error code>。 如果您接收到 8 位數的狀態碼作為錯誤碼，您可以參考[我要如何將 HRESULT 轉換為 Win32 錯誤碼？](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133) \(英文\) 之類的資訊來源，來將這些狀態碼解碼為 OS 錯誤。
1. 如果您接收到 ```Access is Denied``` 作業系統錯誤 = 5，請考慮這些方法：
   -  透過在 Windows 檔案總管中查看檔案的內容，來檢查針對檔案所設定的權限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 Windows 群組來佈建各種檔案資源上的存取控制。 確定適當的群組 [具有如 SQLServerMSSQLUser$ComputerName$MSSQLSERVER 或 SQLServerMSSQLUser$ComputerName$InstanceName 的名稱] 針對錯誤訊息中所述的資料庫檔案具有必要的權限。 如需詳細資料，請檢閱[設定資料庫引擎對檔案系統的存取權限](../../2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md)。 確定 Windows 群組確實包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶或服務 SID。
   -  檢閱正在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的使用者帳戶。 您可以使用 Windows 工作管理員來取得此資訊。 尋找可執行檔 "sqlservr.exe" 的 [使用者名稱]。 此外，如果您最近已變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶，請記住執行此作業的支援方式是使用 SQL Server 組態管理員公用程式。 此功能的詳細資訊已於 [SQL Server 組態管理員](../sql-server-configuration-manager.md)提供。 
   -  取決於作業的類型 (在伺服器啟動時開啟資料庫、附加資料庫、資料庫還原等)，用來進行模擬和存取資料庫檔案的帳戶可能會有所不同。 請檢閱[保護資料和記錄檔](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN)主題，以了解哪個作業會設定哪一種權限，以及會針對哪些帳戶設定。 使用如 Windows SysInternals [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) \(英文\) 之類的工具，來了解檔案存取是否正在 SQL Server 執行個體服務啟動帳戶 [或服務 SID] 或模擬帳戶的資訊安全內容底下發生。

      如果 SQL Server 正在模擬執行 ALTER DATABASE 或 CREATE DATABASE 作業之登入的使用者認證，您將會在 Process Monitor 工具 (作為範例) 中注意到下列資訊：
        ```Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName```
  
1. If you are getting ```The system cannot find the file specified``` OS error = 3:
   - Review the complete path from the error message
   - Ensure the disk drive and the folder path is visible and accessible from Windows Explorer
   - Review the Windows Event log to find out if any problems exist with this disk drive
   - If the path is incorrect and if this database already exists in the system, you can change the database file paths using the methods explained in the topic [Move Database Files](../databases/move-database-files.md). You may have to use this procedure, especially for system database files which encounter 17204 or 17207 and you are working through a disaster recovery scenario where the specified disk drives are unavailable. This topic also explains how you can identify the current location of the various system databases [master, model, tempdb, msdb and mssqlsystemresource].
   - If you see this error because the database files are missing, you have to restore the database from a valid backup.
     - If the database file associated with the error belongs to a secondary filegroup, then you can optionally mark that filegroup offline, bring the database online and then perform a restore of that filegroup alone. For more information, refer to the OFFLINE section of the topic [ALTER DATABASE File and Filegroup Options (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).
     - If the file that produced the error is a transaction log file, review the information under the sections "FOR ATTACH" and "FOR ATTACH_REBUILD_LOG" of the topic [CREATE DATABASE (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) to understand how you can recreate the missing transaction log files.
   - Ensure that any disk or network location [like iSCSI drive] is available before [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attempts to access the database files on these locations. If needed create the required dependencies in Cluster Administrator or Service Control Manager.
1. If you're getting the ```The process cannot access the file because it is being used by another process``` operating system error = 32:
   - Use a tool like [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer) or [Handle](https://docs.microsoft.com/sysinternals/downloads/handle) from Windows Sysinternals to find out if another process or service has acquired exclusive lock on this database file
   - Stop that process from accessing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database files. Common examples include anti-virus programs (see guidance for file exclusions in the following [KB article](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server) )
   - In a cluster environment, make sure that the sqlservr.exe process from the previous owning node has actually released the handles to the database files. Normally, this doesn't occur, but misconfigurations of the cluster or I/O paths can lead to such issues.
  

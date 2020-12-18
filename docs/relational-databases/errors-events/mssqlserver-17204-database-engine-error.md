---
description: MSSQLSERVER_17204
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 996650e8552f435240663d61bf3734f875e2210a
ms.sourcegitcommit: 28fecbf61ae7b53405ca378e2f5f90badb1a296a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2020
ms.locfileid: "96595162"
---
# <a name="mssqlserver_17204"></a>MSSQLSERVER_17204
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |
| :-------- | :---- |
|產品名稱|SQL Server|  
|事件識別碼|17204|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBLKIO_DEVOPENFAILED|  
|訊息文字|%ls:無法開啟檔案 %ls，檔案編號為 %d。  作業系統錯誤: %ls。|  
  
## <a name="explanation"></a>說明  
SQL Server 無法開啟指定的檔案，因為發生指定的 OS 錯誤。  

當 SQL Server 無法開啟資料庫和/或交易記錄檔時，您可能會在 Windows 應用程式事件或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中看見錯誤 17204。 此錯誤的外觀範例如下所示：

``` 
Error: 17204, Severity: 16, State: 1.
FCB::Open failed: Could not open file c:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\data\MyDB_Prm.mdf for file number 1.  OS error: 5(Access is denied.).
```

您可能會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的啟動程序期間，或是嘗試啟動資料庫的任何 Database 作業 (例如 ALTER DATABASE) 期間看見這些錯誤。 在某些情況下，您可能會同時看見 17204 和 17207 錯誤，而在其他情況下則只看見其中一個錯誤。

如果使用者資料庫遇到這些錯誤，該資料庫將會處於 RECOVERY_PENDING 狀態，且應用程式將無法存取該資料庫。 如果系統資料庫遇到這些錯誤，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體將無法啟動，且您將無法連線到這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 系統資料庫發生失敗時，也可能會導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集資源離線。

## <a name="cause"></a>原因
在可以使用任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫之前，該資料庫必須先啟動。 資料庫啟動程序會涉及： 
1. 初始化代表資料庫及資料庫檔案的各種資料結構
1. 開啟屬於資料庫的所有檔案
1. 在資料庫上執行復原 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 [CreateFile](/windows/win32/api/fileapi/nf-fileapi-createfilea) \(英文\) Windows API 函式來開啟屬於某個資料庫的檔案。
 
訊息 17204 (和 17207) 指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在啟動程序期間嘗試開啟資料庫檔案時發生錯誤。
 
這些錯誤訊息包含下列資訊：
1. 嘗試開啟檔案之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 函式的名稱。 您通常會在這些錯誤訊息中觀察到下列其中之一的函式名稱：
   - FCB::Open - 檔案在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 嘗試加以開啟時發生錯誤
   - FileMgr::StartPrimaryDataFiles - 屬於主要檔案群組的主要資料檔案或檔案
   - FileMgr::StartSecondaryDataFiles - 屬於次要檔案群組的檔案
   - FileMgr::StartLogFiles - 交易記錄檔
   - STREAMFCB::Startup - SQL FileStream 容器
   - FCB::RemoveAlternateStreams
  
      
1. 狀態資訊能區分出函式內可能產生此錯誤訊息的多個位置
1. 檔案的完整實體路徑
1. 對應至檔案的檔案識別碼
1. 作業系統錯誤碼和錯誤描述。 在某些情況下，您只會看見錯誤碼。
 
列印在這些錯誤訊息中的作業系統錯誤資訊，是導致錯誤 17204 的根本原因。 導致這些錯誤訊息的常見原因為權限問題或不正確的檔案路徑。


## <a name="user-action"></a>使用者動作  
1. 解決錯誤 17204 須涉及了解相關聯的作業系統錯誤碼並診斷該錯誤。 在解決作業系統錯誤條件之後，您便可以嘗試重新啟動資料庫 (例如使用 ALTER DATABASE SET ONLINE) 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來使受影響的資料庫上線。 在某些情況下，您可能會無法解決作業系統錯誤。 在那種情況下，您必須採取特定的矯正措施。 我們將在此節中討論這些動作。
1. 如果 17204 錯誤訊息僅包含錯誤碼，而沒有錯誤描述，您可以嘗試從作業系統殼層使用命令來解決錯誤碼：net helpmsg <error code>。 如果您接收到 8 位數的狀態碼作為錯誤碼，您可以參考[我要如何將 HRESULT 轉換為 Win32 錯誤碼？](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133) \(英文\) 之類的資訊來源，來將這些狀態碼解碼為 OS 錯誤。
1. 如果您接收到 `Access is Denied` 作業系統錯誤 = 5，請考慮這些方法：
   -  透過在 Windows 檔案總管中查看檔案的內容，來檢查針對檔案所設定的權限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 Windows 群組來佈建各種檔案資源上的存取控制。 確定適當的群組 [具有如 SQLServerMSSQLUser$ComputerName$MSSQLSERVER 或 SQLServerMSSQLUser$ComputerName$InstanceName 的名稱] 針對錯誤訊息中所述的資料庫檔案具有必要的權限。 如需詳細資料，請檢閱[設定資料庫引擎對檔案系統的存取權限](/previous-versions/sql/2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access)。 確定 Windows 群組確實包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶或服務 SID。
   -  檢閱正在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的使用者帳戶。 您可以使用 Windows 工作管理員來取得此資訊。 尋找可執行檔 "sqlservr.exe" 的 [使用者名稱]。 此外，如果您最近已變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶，請記住執行此作業的支援方式是透過 SQL Server 組態管理員公用程式。 此功能的詳細資訊已於 [SQL Server 組態管理員](../sql-server-configuration-manager.md)提供。 
   -  取決於作業的類型 (在伺服器啟動時開啟資料庫、附加資料庫、資料庫還原等)，用來進行模擬和存取資料庫檔案的帳戶可能會有所不同。 請檢閱[保護資料和記錄檔](/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105))主題，以了解哪個作業會設定哪一種權限，以及會針對哪些帳戶設定。 使用如 Windows SysInternals [Process Monitor](/sysinternals/downloads/procmon) \(英文\) 之類的工具，來了解檔案存取是否正在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體服務啟動帳戶 [或服務 SID] 或模擬帳戶的資訊安全內容底下發生。

      如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在模擬執行 ALTER DATABASE 或 CREATE DATABASE 作業之使用者的認證，您將會在 Process Monitor 工具 (作為範例) 中注意到下列資訊：
        
        ```output
        Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName
        ```
  
1. 如果您收到 `The system cannot find the file specified` OS 錯誤 = 3：
   - 檢閱錯誤訊息中的完整路徑
   - 確定可從 Windows 檔案總管看見及存取磁碟機與資料夾路徑。
   - 檢閱 Windows 事件記錄檔，以找出此磁碟機是否有任何現有問題
   - 如果路徑不正確，且此資料庫已經存在於系統中，您便可以使用[移動資料庫檔案](../databases/move-database-files.md)主題中所述的方法變更資料庫檔案路徑。 您可能必須使用此程序，特別是針對遇到 17204 或 17207 且您正在處理無法使用指定磁碟機之災害復原案例之情況下的系統資料庫檔案。 此主題也會說明如何識別各種系統資料庫 [master、model、tempdb、msdb 及 mssqlsystemresource] 的目前位置。
   - 如果您看見此錯誤的原因是因為資料庫檔案遺失，便必須從有效的備份還原資料庫。
     - 如果與錯誤相關聯的資料庫檔案屬於次要檔案群組，您可以選擇性地將該檔案群組標示為離線，使資料庫上線，然後單獨對該檔案群組執行還原。 如需詳細資訊，請參閱 [ALTER DATABASE 檔案及檔案群組選項 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 的＜OFFLINE＞小節。
     - 如果產生錯誤的檔案是交易記錄檔，請檢閱 [CREATE DATABASE (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) 主題的＜FOR ATTACH＞和＜FOR ATTACH_REBUILD_LOG＞小節底下的資訊，以了解如何重新建立遺失的交易記錄檔。
   - 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 嘗試存取任何磁碟或網路位置 [例如 iSCSI 磁碟] 上的資料庫檔案之前，請先確保這些位置是可供使用的。 如果必要，請在叢集系統管理員或服務控制管理員中建立必要的相依性。
1. 如果您收到 `The process cannot access the file because it is being used by another process` 作業系統錯誤 = 32：
   - 請使用來自 Windows Sysinternals 的 [Process Explorer](/sysinternals/downloads/process-explorer) \(英文\) 或 [Handle](/sysinternals/downloads/handle) \(英文\) 之類的工具，來找出是否有另一個處理序或服務已取得此資料庫檔案的獨佔鎖定。
   - 停止該處理序存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫檔案。 常見的範例包括防毒程式 (請參閱後續[知識庫文章](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server)中針對檔案排除的指導方針)
   - 在叢集環境中，請確保來自先前擁有節點的 sqlservr.exe 處理序已確實釋放資料庫檔案的控制代碼。 雖然通常並不會發生此情況，但叢集或 I/O 路徑設定錯誤可能會導致此類問題。

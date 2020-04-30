---
title: MSSQLSERVER_5228 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5120 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: ff8fb262b643390f2914a4a5e6c42dcc887206f8
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728615"
---
# <a name="mssqlserver_5120"></a>MSSQLSERVER_5120
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|5120|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DSK_FCB_FAILURE|  
|訊息文字|資料表錯誤：無法開啟實體檔案 "%.*ls"。 作業系統錯誤 %d: "%ls"。|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法開啟資料庫檔案。  訊息中所提供的作業系統錯誤能更明確地指出造成失敗的根本原因。 您通常會和其他錯誤 (例如 [17204](mssqlserver-17204-database-engine-error.md) 或 [17207](mssqlserver-17207-database-engine-error.md)) 一起看見此錯誤
  
## <a name="user-action"></a>使用者動作  
  
  診斷並更正作業系統錯誤，然後重試此作業。 有多個狀態可協助 Microsoft 縮小產品中正在發生錯誤的區域。 
  
### <a name="access-is-denied"></a>存取被拒 
如果您接收到 ```Access is Denied``` 作業系統錯誤 = 5，請考慮這些方法：
   -  透過在 Windows 檔案總管中查看檔案的內容，來檢查針對檔案所設定的權限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 Windows 群組來佈建各種檔案資源上的存取控制。 確定適當的群組 [具有如 SQLServerMSSQLUser$ComputerName$MSSQLSERVER 或 SQLServerMSSQLUser$ComputerName$InstanceName 的名稱] 針對錯誤訊息中所述的資料庫檔案具有必要的權限。 如需詳細資料，請檢閱[設定資料庫引擎對檔案系統的存取權限](../../2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md)。 確定 Windows 群組確實包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶或服務 SID。
   -  檢閱正在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的使用者帳戶。 您可以使用 Windows 工作管理員來取得此資訊。 尋找可執行檔 "sqlservr.exe" 的 [使用者名稱]。 此外，如果您最近已變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶，請記住執行此作業的支援方式是使用 [SQL Server 組態管理員](../sql-server-configuration-manager.md)公用程式。 
   -  取決於作業的類型 (在伺服器啟動時開啟資料庫、附加資料庫、資料庫還原等)，用來進行模擬和存取資料庫檔案的帳戶可能會有所不同。 請檢閱[保護資料和記錄檔](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN)主題，以了解哪個作業會設定哪一種權限，以及會針對哪些帳戶設定。 使用如 Windows SysInternals [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) \(英文\) 之類的工具，來了解檔案存取是否正在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體服務啟動帳戶 [或服務 SID] 或模擬帳戶的資訊安全內容底下發生。

      如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在模擬執行 ALTER DATABASE 或 CREATE DATABASE 作業之登入的使用者認證，您將會在 Process Monitor 工具 (作為範例) 中注意到下列資訊：
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
  
  
### Attaching Files that Reside on a Network-attached storage  
If you cannot re-attach a database that resides on network-attached storage, a message like this may be logged in the Application log:

```Msg 5120, Level 16, State 101, Line 1 Unable to open the physical file "\\servername\sharename\filename.mdf". Operating system error 5: (Access is denied.).```

This problem occurs because [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resets the file permissions when the database is detached. When you try to reattach the database, a failure occurs because of limited share permissions.

To resolve, follow these steps:
1. Use the -T startup option to start [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use this startup option to turn on trace flag 1802 in [SQL Server Configuration Manager](../sql-server-configuration-manager.md) (see [Trace Flags](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md) for information on 1802). For more information about how to change the startup parameters, see [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)

2. Use the following command to detach the database.
```tsql
 exec sp_detach_db DatabaseName
 go 
```

3. 使用下列命令來重新附加資料庫。
```tsql
exec sp_attach_db DatabaseName, '\\Network-attached storage_Path\DatabaseMDFFile.mdf', '\\Network-attached storage_Path\DatabaseLDFFile.ldf'
go
```
 

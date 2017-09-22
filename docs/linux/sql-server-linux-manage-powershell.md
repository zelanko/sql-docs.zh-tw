---
title: "管理 SQL Server on Linux 的 PowerShell |Microsoft 文件"
description: "本主題提供與 SQL Server on Linux 的 Windows 上使用 PowerShell 的總覽。"
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: e2c1a69f81bafe3f1165c50950bb10fbfc87b579
ms.contentlocale: zh-tw
ms.lasthandoff: 09/21/2017

---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>在 Windows 上使用 PowerShell 來管理 SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本主題將介紹[SQL Server PowerShell](https://msdn.microsoft.com/en-us/library/mt740629.aspx)及如何使用 SQL Server 2017 RC2 on Linux 會逐步引導您透過提供幾個範例。 PowerShell 支援的 SQL Server 是在 Windows 中，目前可用，因此您可以使用它時可以連線到遠端的 SQL Server 執行個體，在 Linux 上的 Windows 電腦。

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>在 Windows 上安裝最新版的 SQL PowerShell

[SQL PowerShell](https://msdn.microsoft.com/en-us/library/mt740629.aspx)上 Windows 隨附於[SQL Server Management Studio (SSMS)](/sql-docs/docs/ssms/sql-server-management-studio-ssms)。 當使用 SQL Server，您應該一律使用最新版本的 SSMS 和 SQL PowerShell。 SSMS 的最新版本而不斷更新和經過最佳化，而目前適用於 SQL server on Linux 2017 RC2。 若要下載並安裝最新版本，請參閱[下載 SQL Server Management Studio](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms)。 若要保持最新狀態，最新版本的 SSMS 會提示您有新的版本可供下載時。 

## <a name="before-you-begin"></a>開始之前

讀取[已知問題](sql-server-linux-release-notes.md)Linux 上的 SQL Server 2017 rc2。

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>啟動 PowerShell 並匯入*sqlserver*模組

讓我們開始啟動 windows PowerShell。 開啟*命令提示字元*您 Windows 電腦上，而型別**PowerShell**啟動新的 Windows PowerShell 工作階段。

```
PowerShell
```

SQL Server 提供名為 Windows PowerShell 模組**SqlServer**您可以使用匯入 SQL Server 元件 （SQL Server 提供者和 cmdlet） 的 PowerShell 環境或指令碼。

複製並貼到匯入 PowerShell 命令提示字元下面的命令**SqlServer**到目前的 PowerShell 工作階段的模組：

```powershell
Import-Module SqlServer
```

輸入下列命令在 PowerShell 提示字元中，可讓您確認**SqlServer**已正確匯入模組：

```powershell
Get-Module -Name SqlServer
```

PowerShell 應該會顯示類似下面資訊：

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     0.0        SqlServer
Manifest   20.0       SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>連接到 SQL Server，並取得伺服器資訊

連接到您在 Linux 上的 SQL Server 2017 執行個體，並顯示幾個伺服器屬性，讓我們在 Windows 上使用 PowerShell。

複製並貼上以下命令，在 PowerShell 提示字元。 當您執行這些命令時，PowerShell 會：
- 顯示*Windows PowerShell 認證要求*對話方塊，提示您輸入認證 (*SQL 使用者名稱*和*SQL 密碼*) 連接到您在 Linux 上的 SQL Server 2017 RC2 執行個體
- 載入 SQL Server 管理物件 (SMO) 組件
- 建立的執行個體[伺服器](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.server.aspx)物件
- 連接到**伺服器**及顯示幾個屬性

請記得要取代** \<your_server_instance\> **與 IP 位址或您在 Linux 上的 SQL Server 2017 RC2 執行個體的主機名稱。

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Load the SMO assembly and create a Server object
[System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SMO') | out-null
$server = New-Object ('Microsoft.SqlServer.Management.Smo.Server') $serverInstance

# Set credentials
$server.ConnectionContext.LoginSecure=$false
$server.ConnectionContext.set_Login($credential.UserName)
$server.ConnectionContext.set_SecurePassword($credential.Password)

# Connect to the Server and get a few properties
$server.Information | Select-Object Edition, HostPlatform, HostDistribution | Format-List
# done
```

PowerShell 應該會顯示類似下面顯示的內容資訊：

```
Edition          : Developer Edition (64-bit)
HostPlatform     : Linux
HostDistribution : Ubuntu
```
> [!NOTE]
> 如果沒有顯示，這些值，連線到目標 SQL Server 執行個體最有可能會失敗。 請確定您可以從 SQL Server Management Studio 連接使用相同的連接資訊。 然後檢閱[連線疑難排解建議](sql-server-linux-troubleshooting-guide.md#connection)。

## <a name="examine-sql-server-error-logs"></a>檢查 SQL Server 錯誤記錄檔

讓我們將使用上檢查錯誤記錄檔的 Windows PowerShell 連接您在 Linux 上的 SQL Server 2017 執行個體。 我們也會使用**Out-gridview** cmdlet 來顯示資訊從錯誤記錄中的方格檢視顯示。

複製並貼上以下命令，在 PowerShell 提示字元。 它們可能需要幾分鐘才能完成。 這些命令執行下列作業：
- 顯示*Windows PowerShell 認證要求*對話方塊，提示您輸入認證 (*SQL 使用者名稱*和*SQL 密碼*) 連接到您在 Linux 上的 SQL Server 2017 RC2 執行個體
- 使用**Get SqlErrorLog** cmdlet 來連接到在 Linux 上的 SQL Server 2017 執行個體，並擷取錯誤記錄檔自**昨天**
- 將輸出輸送至**Out-gridview** cmdlet

請記得要取代** \<your_server_instance\> **與 IP 位址或您在 Linux 上的 SQL Server 2017 RC2 執行個體的主機名稱。

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>另請參閱
- [SQL Server PowerShell](/sql-docs/docs/relational-databases/scripting/sql-server-powershell)


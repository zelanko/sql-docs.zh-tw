---
title: 管理使用 PowerShell 在 Linux 上的 SQL Server |Microsoft Docs
description: 本文提供 Windows 與 Linux 上的 SQL Server 上使用 PowerShell 的概觀。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: a1b6b4bb4c99a3b991120d57b8cf25cc91686957
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982140"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Windows 上使用 PowerShell 來管理 SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章介紹[SQL Server PowerShell](https://msdn.microsoft.com/library/mt740629.aspx)並逐步指導您有幾個範例有關如何使用 Linux 上的 SQL Server 2017。 PowerShell 支援的 SQL Server 上目前已 Windows，因此您可以使用它時可以連線到 Linux 上的遠端 SQL Server 執行個體的 Windows 電腦。

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Windows 上安裝最新版的 SQL PowerShell

[SQL PowerShell](https://msdn.microsoft.com/library/mt740629.aspx)在 Windows 上是隨附[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)。 當使用 SQL Server，您應該一律使用最新版的 SSMS 和 SQL PowerShell。 最新版的 SSMS 會持續更新及最佳化和目前適用於 SQL Server 2017 on Linux。 若要下載並安裝最新版本，請參閱[下載 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 若要保持最新狀態，最新版的 SSMS 會提示您有新的版本可供下載時。

## <a name="before-you-begin"></a>開始之前

讀取[已知問題](sql-server-linux-release-notes.md)針對 Linux 上的 SQL Server 2017。

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>啟動 PowerShell 並匯入*sqlserver*模組

現在就開始啟動 PowerShell Windows。 開啟*命令提示字元*在您的 Windows 電腦和型別**PowerShell**啟動新的 Windows PowerShell 工作階段。

```
PowerShell
```

SQL Server 提供名為的 Windows PowerShell 模組**SqlServer** ，您可以使用匯入 （SQL Server 提供者和 cmdlet） 的 SQL Server 元件的 PowerShell 環境或指令碼。

複製並貼上下列命令以匯入的 PowerShell 提示字元**SqlServer**到目前的 PowerShell 工作階段的模組：

```powershell
Import-Module SqlServer
```

輸入下列命令在 PowerShell 提示字元中，確認**SqlServer**已正確匯入模組：

```powershell
Get-Module -Name SqlServer
```

PowerShell 應該會顯示類似下列輸出的資訊：

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     0.0        SqlServer
Manifest   20.0       SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>連接到 SQL Server，並取得伺服器資訊

連接到您在 Linux 上的 SQL Server 2017 執行個體，並顯示數種伺服器屬性，讓我們在 Windows 上使用 PowerShell。

複製並貼上下列命令在 PowerShell 提示字元。 當您執行這些命令時，PowerShell 將會：
- 顯示*Windows PowerShell 認證要求*會提示您輸入認證的對話方塊 (*SQL 使用者名稱*並*SQL 密碼*) 連接到 SQL Server 2017在 Linux 上的執行個體
- 載入 SQL Server 管理物件 (SMO) 組件
- 建立的執行個體[Server](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.server.aspx)物件
- 連接到**Server**並顯示幾個屬性

請記得取代**\<your_server_instance\>** 與 IP 位址或您的 SQL Server 2017 執行個體，在 Linux 上的主機名稱。

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

PowerShell 應該會顯示類似下列輸出的資訊：

```
Edition          : Developer Edition (64-bit)
HostPlatform     : Linux
HostDistribution : Ubuntu
```
> [!NOTE]
> 不會顯示這些值，如果目標 SQL Server 執行個體的連線很可能會失敗。 請確定您可以從 SQL Server Management Studio 連線使用相同的連接資訊。 然後檢閱[連線疑難排解建議](sql-server-linux-troubleshooting-guide.md#connection)。

## <a name="examine-sql-server-error-logs"></a>檢查 SQL Server 錯誤記錄檔

讓我們使用 PowerShell 來檢查錯誤記錄檔的 Windows 上連接您在 Linux 上的 SQL Server 2017 執行個體。 我們也會使用**Out-gridview** cmdlet 來顯示資訊從錯誤記錄中的方格檢視顯示。

複製並貼上下列命令在 PowerShell 提示字元。 它們可能需要幾分鐘的時間來執行。 這些命令執行下列作業：
- 顯示*Windows PowerShell 認證要求*會提示您輸入認證的對話方塊 (*SQL 使用者名稱*並*SQL 密碼*) 連接到 SQL Server 2017在 Linux 上的執行個體
- 使用**Get SqlErrorLog** cmdlet 來連線到 Linux 上的 SQL Server 2017 執行個體，並擷取錯誤記錄檔自**昨天**
- 將輸出輸送至**Out-gridview** cmdlet

請記得取代**\<your_server_instance\>** 與 IP 位址或您的 SQL Server 2017 執行個體，在 Linux 上的主機名稱。

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>另請參閱
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)

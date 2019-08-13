---
title: 使用 PowerShell 管理 Linux 上的 SQL Server
description: 本文概述 Windows 上的 PowerShell 如何用於 Linux 上的 SQL Server。
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 52db0986bb6af34e1dc034d95146a96d3fdcf246
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000126"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>使用 Windows 上的 PowerShell 管理 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介紹 [SQL Server PowerShell](../powershell/sql-server-powershell.md)，並逐步引導您了解如何用在 Linux 上的 SQL Server 的幾個範例。 SQL Server 的 PowerShell 支援目前適用於 Windows、MacOS 與 Linux。 本文將逐步引導您使用 Windows 電腦連線到 Linux 上的遠端 SQL Server 執行個體。

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>安裝 Windows 上最新版的 SQL PowerShell

Windows 上的 [SQL PowerShell](../powershell/download-sql-server-ps-module.md) 保存在 PowerShell 資源庫中。 使用 SQL Server 時，您應該一律使用最新版本的 SqlServer PowerShell 模組。

## <a name="before-you-begin"></a>開始之前

閱讀 Linux 上 SQL Server 的[已知問題](sql-server-linux-release-notes.md)。

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>啟動 PowerShell 並匯入 *sqlserver* 模組

讓我們從啟動 Windows 上的 PowerShell 開始。 在您的 Windows 電腦上使用 <kbd>Win</kbd>+<kbd>R</kbd>，然後鍵入 **PowerShell**，啟動新的 Windows PowerShell 工作階段。

```
PowerShell
```

SQL Server 提供名為 **SqlServer** 的 PowerShell 模組。 您可以使用 **SqlServer** 模組，將 SQL Server 元件 (SQL Server 提供者和 Cmdlet) 匯入 PowerShell 環境或指令碼中。

在 PowerShell 提示字元中複製並貼上下列命令，將 **SqlServer** 模組匯入到目前的 PowerShell 工作階段：

```powershell
Import-Module SqlServer
```

在 PowerShell 提示字元中鍵入下列命令，確認 **SqlServer** 模組已正確匯入：

```powershell
Get-Module -Name SqlServer
```

PowerShell 應該會顯示類似下列輸出的資訊：

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>連線到 SQL Server 並取得伺服器資訊

讓我們使用 Windows 上的 PowerShell 連線到您在 Linux 上的 SQL Server 執行個體，並顯示幾個伺服器屬性。

在 PowerShell 提示字元中複製並貼上下列命令。 當您執行這些命令時，PowerShell 將會：
- 顯示對話方塊，提示您輸入執行個體的主機名稱或 IP 位址
- 顯示 [Windows PowerShell 認證要求]  對話方塊，它會提示您輸入認證。 您可以使用「SQL 使用者名稱」  和「SQL 密碼」  連線至 Linux 上的 SQL Server 執行個體
- 使用 **Get-SqlInstance** Cmdlet 連線到**伺服器**，並顯示一些屬性

(選擇性) 您可以將 `$serverInstance` 變數取代為您 SQL Server 執行個體的 IP 位址或主機名稱。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and get a few properties
Get-SqlInstance -ServerInstance $serverInstance -Credential $credential
# done
```

PowerShell 應該會顯示類似下列輸出的資訊：

```
Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution                
-------------                   -------    ------------ -----------  ------------ ----------------                
your_server_instance            14.0.3048  RTM          CU13         Linux        Ubuntu 
```
> [!NOTE]
> 如果這些值沒有顯示任何內容，與目標 SQL Server 執行個體的連線很可能失敗。 請確定您可以使用相同的連線資訊，從 SQL Server Management Studio 連線。 然後檢閱[連線疑難排解建議](sql-server-linux-troubleshooting-guide.md#connection)。

## <a name="using-the-sql-server-powershell-provider"></a>使用 SQL Server PowerShell 提供者

連線到 SQL Server 執行個體的另一個選項是使用 [SQL Server PowerShell 提供者](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)。  此提供者可讓您巡覽 SQL Server 執行個體，如同您在物件總管中巡覽樹狀結構一樣，但是在 cmdline 上。  根據預設，此提供者會顯示為名為 `SQLSERVER:\` 的 PSDrive，您可以用來連線與巡覽您的網域帳戶可存取的 SQL Server 執行個體。  如需如何對 Linux 上的 SQL Server 設定 Active Directory 驗證的詳細資訊，請參閱 [Configuration steps](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps) (設定步驟)。

您也可以搭配 SQL Server PowerShell 提供者使用 SQL 驗證。 若要這麼做，請使用 `New-PSDrive` Cmdlet 建立新的 PSDrive，並提供適當的認證進行連線。

在下面的範例中，您會看到一個如何使用 SQL 驗證建立新 PSDrive 的範例。

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.
New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

您可以藉由執行 `Get-PSDrive` Cmdlet 確認磁碟機是否建立。

```powershell
Get-PSDrive
```

建立新的 PSDrive 之後，您就可以開始巡覽。

```powershell
dir SQLonDocker:\Databases
```

輸出可能會如下所示。  您可能會注意到，此輸出類似 SSMS 會顯示在 [資料庫] 節點上的內容。  它會顯示使用者資料庫，而不是系統資料庫。

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.76 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.57 MB Simple       140 sa
```

如果您需要查看執行個體上的所有資料庫，其中一個選項是使用 [Get-SqlDatabase](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlDatabase) Cmdlet。

## <a name="examine-sql-server-error-logs"></a>檢查 SQL Server 錯誤記錄檔

下列步驟會使用 Windows 上的 PowerShell，檢查 Linux 上 SQL Server 執行個體上的錯誤記錄檔連線。 我們也會使用 **Out-GridView** Cmdlet，以格線檢視顯示來顯示錯誤記錄檔中的資訊。

在 PowerShell 提示字元中複製並貼上下列命令。 可能需要幾分鐘的時間執行。 這些命令會執行下列動作：
- 顯示對話方塊，提示您輸入執行個體的主機名稱或 IP 位址
- 顯示 [Windows PowerShell 認證要求]  對話方塊，它會提示您輸入認證。 您可以使用「SQL 使用者名稱」  和「SQL 密碼」  連線至 Linux 上的 SQL Server 執行個體
- 使用 **Get-SqlErrorLog** Cmdlet 連線到 Linux 上的 SQL Server 執行個體，並擷取自**昨天**起的錯誤記錄檔
- 將輸出輸送至 **Out-GridView** Cmdlet

(選擇性) 您可以將 `$serverInstance` 變數取代為您 SQL Server 執行個體的 IP 位址或主機名稱。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>另請參閱
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
- [SqlServer Cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)

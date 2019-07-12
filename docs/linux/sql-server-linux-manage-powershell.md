---
title: 管理使用 PowerShell 在 Linux 上的 SQL Server
description: 本文提供 Windows 與 Linux 上的 SQL Server 上使用 PowerShell 的概觀。
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 21ce61a823281c5e6688bcfb8aee96d296cb671d
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834936"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Windows 上使用 PowerShell 來管理 SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章介紹[SQL Server PowerShell](../powershell/sql-server-powershell.md)並逐步指導您有幾個範例有關如何使用 Linux 上的 SQL Server。 PowerShell 支援的 SQL Server 在 Windows、 MacOS 和 Linux 上是目前可用的。 這篇文章會引導您使用 Windows 電腦連線到 Linux 上的遠端 SQL Server 執行個體。

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Windows 上安裝最新版的 SQL PowerShell

[SQL PowerShell](../powershell/download-sql-server-ps-module.md)在 Windows 上維護 PowerShell Gallery 中。 當使用 SQL Server，您應該一律使用 SqlServer PowerShell 模組的最新版本。

## <a name="before-you-begin"></a>開始之前

讀取[已知問題](sql-server-linux-release-notes.md)for SQL Server on Linux。

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>啟動 PowerShell 並匯入*sqlserver*模組

現在就開始啟動 PowerShell Windows。 使用<kbd>贏得</kbd>+<kbd>R</kbd>，而在您的 Windows 電腦和型別**PowerShell**啟動新的 Windows PowerShell 工作階段。

```
PowerShell
```

SQL Server 提供名為的 PowerShell 模組**SqlServer**。 您可以使用**SqlServer**模組匯入 PowerShell 環境或指令碼 （SQL Server 提供者和 cmdlet） 的 SQL Server 元件。

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
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>連接到 SQL Server，並取得伺服器資訊

連接到您在 Linux 上的 SQL Server 執行個體，並顯示數種伺服器屬性，讓我們在 Windows 上使用 PowerShell。

複製並貼上下列命令在 PowerShell 提示字元。 當您執行這些命令時，PowerShell 將會：
- 顯示一個對話方塊，提示您輸入的主機名稱或 IP 位址，您的執行個體
- 顯示*Windows PowerShell 認證要求*對話方塊，提示您輸入認證。 您可以使用您*SQL 使用者名稱*並*SQL 密碼*連接到您在 Linux 上的 SQL Server 執行個體
- 使用**Get SqlInstance** cmdlet 以連線到**Server**並顯示幾個屬性

（選擇性） 您可以直接取代`$serverInstance`的 IP 位址或您的 SQL Server 執行個體的主機名稱的變數。

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
> 不會顯示這些值，如果目標 SQL Server 執行個體的連線很可能會失敗。 請確定您可以從 SQL Server Management Studio 連線使用相同的連接資訊。 然後檢閱[連線疑難排解建議](sql-server-linux-troubleshooting-guide.md#connection)。

## <a name="using-the-sql-server-powershell-provider"></a>使用 SQL Server PowerShell 提供者

連接到您的 SQL Server 執行個體的另一個選項是使用[SQL Server PowerShell 提供者](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)。  此提供者可讓您瀏覽與類似，如果您已瀏覽樹狀結構中 [物件總管] 中，但在 cmdline 的 SQL Server 執行個體。  依預設此提供者會以名為 PSDrive 形式呈現`SQLSERVER:\`可用來進行連線與瀏覽您的網域帳戶可存取的 SQL Server 執行個體。  請參閱[設定步驟](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps)如需有關如何設定 Active Directory 驗證 Linux 上的 SQL Server 的資訊。

您也可以使用 SQL Server PowerShell 提供者使用 SQL 驗證。 若要這樣做，請使用`New-PSDrive`cmdlet 來建立新的 PSDrive，提供適當的認證，才能連線。

在此範例中，您會看到如何建立新的 PSDrive 使用 SQL 驗證的其中一個範例。

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.
New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

您可以確認磁碟機已建立執行`Get-PSDrive`cmdlet。

```powershell
Get-PSDrive
```

當您建立新的 PSDrive 之後時，您可以開始瀏覽它。

```powershell
dir SQLonDocker:\Databases
```

以下是輸出可能如下所示。  您可能會發現輸出是類似於 SSMS 會顯示在 [資料庫] 節點。  它會顯示使用者資料庫，而不是系統資料庫。

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

如果您需要在您的執行個體上看到所有資料庫，其中一個選項是使用[Get-sqldatabase](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlDatabase) cmdlet。

## <a name="examine-sql-server-error-logs"></a>檢查 SQL Server 錯誤記錄檔

下列步驟會使用在 Windows PowerShell，來檢查連接您在 Linux 上的 SQL Server 執行個體的記錄檔的錯誤。 我們也會使用**Out-gridview** cmdlet 來顯示資訊從錯誤記錄中的方格檢視顯示。

複製並貼上下列命令在 PowerShell 提示字元。 它們可能需要幾分鐘的時間來執行。 這些命令執行下列作業：
- 顯示一個對話方塊，提示您輸入的主機名稱或 IP 位址，您的執行個體
- 顯示*Windows PowerShell 認證要求*對話方塊，提示您輸入認證。 您可以使用您*SQL 使用者名稱*並*SQL 密碼*連接到您在 Linux 上的 SQL Server 執行個體
- 使用**Get SqlErrorLog** cmdlet 來連線到 Linux 上的 SQL Server 執行個體，並擷取錯誤記錄檔自**昨天**
- 將輸出輸送至**Out-gridview** cmdlet

（選擇性） 您可以取代`$serverInstance`的 IP 位址或您的 SQL Server 執行個體的主機名稱的變數。

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

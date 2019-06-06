---
title: 管理與 PowerShell Core 在 Linux 上的 SQL Server |Microsoft Docs
description: 這篇文章提供與 Linux 上的 SQL Server 中使用 PowerShell Core 的概觀。
ms.date: 04/22/2019
ms.reviewer: jroth
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: craigg
ms.openlocfilehash: 242e3ab70d41df4d774400034f361b31289d97c9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713150"
---
# <a name="manage-sql-server-on-linux-with-powershell-core"></a>管理與 PowerShell Core 在 Linux 上的 SQL Server

這篇文章介紹[SQL Server PowerShell](../powershell/sql-server-powershell.md)和在 macOS 和 Linux 上會逐步引導您一些有關如何使用 PowerShell Core （PS 核心） 的範例。 PowerShell Core 是現在的開放原始碼專案上[GitHub](https://github.com/powershell/powershell)。

## <a name="cross-platform-editor-options"></a>跨平台編輯器選項

所有步驟下方的 PowerShell Core 可在一般的終端機中，或您可以從 VS Code 或 Azure Data Studio 中的終端機中執行它們。  VS Code 和 Azure Data Studio 可在 macOS 和 Linux 上。  如需有關 Azure Data Studio 的詳細資訊，請參閱 <<c0> [ 本快速入門](https://docs.microsoft.com/sql/azure-data-studio/quickstart-sql-server)。  您也可以考慮使用[PowerShell 延伸模組](https://docs.microsoft.com/sql/azure-data-studio/powershell-extension)它。

## <a name="installing-powershell-core"></a>安裝 PowerShell Core

如需有關如何在各種支援和實驗性的平台上安裝 PowerShell Core 的詳細資訊，請參閱下列文章：

- [在 Windows 上安裝 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-6)
- [在 Linux 上安裝 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [在 macOS 上安裝 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)
- [在 ARM 上安裝 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/powershell-core-on-arm?view=powershell-6)

## <a name="install-the-sqlserver-module"></a>安裝 SqlServer 模組

`SqlServer`模組會在維護[PowerShell 資源庫](https://www.powershellgallery.com/packages/SqlServer/)。 當使用 SQL Server，您應該一律使用 SqlServer PowerShell 模組的最新版本。

若要安裝 SqlServer 模組，請開啟 PowerShell Core 工作階段並執行下列程式碼：

```powerhsell
Install-Module -Name SqlServer
```

如需有關如何從 PowerShell Gallery 安裝 SqlServer 模組的詳細資訊，請參閱此[網頁](../powershell/download-sql-server-ps-module.md)。

## <a name="using-the-sqlserver-module"></a>使用 SqlServer 模組

現在就開始啟動 PowerShell Core。  如果您是在 macOS 或 Linux，開放*終端機工作階段*在您的電腦，與型別**pwsh**啟動新的 PowerShell Core 工作階段。  在 Windows 中，使用<kbd>贏得</kbd>+<kbd>R</kbd>，然後輸入`pwsh`啟動新的 PowerShell Core 工作階段。

```
pwsh
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

下列步驟會使用 PowerShell Core，連接到您在 Linux 上的 SQL Server 執行個體，並顯示數種伺服器屬性。

複製並貼上下列命令在 PowerShell 提示字元。 當您執行這些命令時，PowerShell 將會：
- 顯示一個對話方塊，提示您輸入的主機名稱或 IP 位址，您的執行個體
- 顯示*PowerShell 認證要求*對話方塊，提示您輸入認證。 您可以使用您*SQL 使用者名稱*並*SQL 密碼*連接到您在 Linux 上的 SQL Server 執行個體
- 使用**Get SqlInstance** cmdlet 以連線到**Server**並顯示幾個屬性

（選擇性） 您可以直接取代`$serverInstance`的 IP 位址或您的 SQL Server 執行個體的主機名稱的變數。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and return a few properties
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

連接到您的 SQL Server 執行個體的另一個選項是使用[SQL Server PowerShell 提供者](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider)。  使用提供者，可讓您瀏覽與類似，如果您已瀏覽樹狀結構中 [物件總管] 中，但在 cmdline 的 SQL Server 執行個體。  依預設此提供者會以名為 PSDrive 形式呈現`SQLSERVER:\`可用來進行連線與瀏覽您的網域帳戶可存取的 SQL Server 執行個體。  請參閱[設定步驟](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps)如需有關如何設定 Active Directory 驗證 Linux 上的 SQL Server 的資訊。

您也可以使用 SQL Server PowerShell 提供者使用 SQL 驗證。 若要這樣做，請使用`New-PSDrive`cmdlet 來建立新的 PSDrive，提供適當的認證來連接。

在此範例中，您會看到如何建立新的 PSDrive 使用 SQL 驗證的範例。

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

以下是輸出可能如下所示。  您可能會注意到此輸出會類似於 SSMS 會顯示在 [資料庫] 節點。  它會顯示使用者資料庫，而不是系統資料庫。

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

如果您需要在您的執行個體上看到所有資料庫，其中一個選項是使用`Get-SqlDatabase`cmdlet。

## <a name="get-databases"></a>取得資料庫

若要了解重要的 cmdlet 是`Get-SqlDatabase`。  牽涉到資料庫或資料庫內物件的許多作業`Get-SqlDatabase`指令程式可用。  如果您同時提供值`-ServerInstance`和`-Database`會擷取參數，只有一個資料庫物件。  不過，如果您只有指定`-ServerInstance`參數，將會傳回該執行個體上的所有資料庫的完整清單。

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

# Connect to the Instance and retrieve all databases
Get-SqlDatabase -ServerInstance ServerB -Credential $credential
```

以下是範例可能會傳回上述 Get-sqldatabase 命令的內容：

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.88 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.63 MB Simple       140 sa
master               Normal        6.00 MB  600.00 KB Simple       140 sa
model                Normal       16.00 MB    5.70 MB Full         140 sa
msdb                 Normal       15.50 MB    1.14 MB Simple       140 sa
tempdb               Normal       16.00 MB    5.49 MB Simple       140 sa

```

## <a name="examine-sql-server-error-logs"></a>檢查 SQL Server 錯誤記錄檔

下列步驟會使用 PowerShell Core，請檢查的錯誤記錄檔連接您在 Linux 上的 SQL Server 執行個體。

複製並貼上下列命令在 PowerShell 提示字元。 它們可能需要幾分鐘的時間來執行。 這些命令會執行下列步驟：
- 顯示一個對話方塊，提示您輸入的主機名稱或 IP 位址，您的執行個體
- 顯示*PowerShell 認證要求*提示您輸入認證的對話方塊。 您可以使用您*SQL 使用者名稱*並*SQL 密碼*連接到您在 Linux 上的 SQL Server 執行個體
- 使用**Get SqlErrorLog** cmdlet 來連線到 Linux 上的 SQL Server 執行個體，並擷取錯誤記錄檔自**昨天**

（選擇性） 您可以取代`$serverInstance`的 IP 位址或您的 SQL Server 執行個體的主機名稱的變數。

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday
# done
```

## <a name="explore-cmdlets-currently-available-in-ps-core"></a>瀏覽目前提供的 PS 核心 cmdlet
雖然 SqlServer 模組目前的 Windows PowerShell 中可用的 106 cmdlet，就有一個唯一 59 的 106 可用於 PSCore。 目前可用的 59 cmdlet 的完整清單如下所示。  深入的 SqlServer 模組中的所有 cmdlet 的文件，請參閱 SqlServer[指令程式參考](https://docs.microsoft.com/powershell/module/sqlserver/)。

下列命令會顯示所有可用的 cmdlet 在您使用的 PowerShell 版本上。

```powershell
Get-Command -Module SqlServer -CommandType Cmdlet |
SORT -Property Noun |
SELECT Name
```

- ConvertFrom-EncodedSqlName
- ConvertTo-EncodedSqlName
- Get-SqlAgent
- Get-SqlAgentJob
- Get-SqlAgentJobHistory
- Get-SqlAgentJobSchedule
- Get-SqlAgentJobStep
- Get-SqlAgentSchedule
- Remove-SqlAvailabilityDatabase
- Resume-SqlAvailabilityDatabase
- Add-SqlAvailabilityDatabase
- Suspend-SqlAvailabilityDatabase
- New-SqlAvailabilityGroup
- Set-SqlAvailabilityGroup
- Remove-SqlAvailabilityGroup
- Switch-SqlAvailabilityGroup
- Join-SqlAvailabilityGroup
- Revoke-SqlAvailabilityGroupCreateAnyDatabase
- Grant-SqlAvailabilityGroupCreateAnyDatabase
- New-SqlAvailabilityGroupListener
- Set-SqlAvailabilityGroupListener
- Add-SqlAvailabilityGroupListenerStaticIp
- Set-SqlAvailabilityReplica
- Remove-SqlAvailabilityReplica
- New-SqlAvailabilityReplica
- Set-SqlAvailabilityReplicaRoleToSecondary
- New-SqlBackupEncryptionOption
- Get-SqlBackupHistory
- Invoke-Sqlcmd
- New-SqlCngColumnMasterKeySettings
- Remove-SqlColumnEncryptionKey
- Get-SqlColumnEncryptionKey
- Remove-SqlColumnEncryptionKeyValue
- Add-SqlColumnEncryptionKeyValue
- Get-SqlColumnMasterKey
- Remove-SqlColumnMasterKey
- New-SqlColumnMasterKey
- Get-SqlCredential
- Set-SqlCredential
- New-SqlCredential
- Remove-SqlCredential
- New-SqlCspColumnMasterKeySettings
- Get-SqlDatabase
- Restore-SqlDatabase
- Backup-SqlDatabase
- Set-SqlErrorLog
- Get-SqlErrorLog
- New-SqlHADREndpoint
- Set-SqlHADREndpoint
- Get-SqlInstance
- Add-SqlLogin
- Remove-SqlLogin
- Get-SqlLogin
- Set-SqlSmartAdmin
- Get-SqlSmartAdmin
- Read-SqlTableData
- Write-SqlTableData
- Read-SqlViewData
- Convert-UrnToPath

## <a name="see-also"></a>另請參閱
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)

---
title: 透過 PowerShell Desired State Configuration 安裝 SQL Server | Microsoft Docs
description: 了解如何使用 PowerShell Desired State Configuration (DSC) 安裝 SQL Server。
ms.custom: ''
ms.date: 10/26/2018
ms.devlang: PowerShell
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
author: randomnote1
ms.author: dareist
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 16d425d8eb66a950f432fa3ef9c68a8e68a78d22
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148474"
---
# <a name="install-sql-server-with-powershell-desired-state-configuration"></a>透過 PowerShell Desired State Configuration 安裝 SQL Server

您多常在點選 SQL Server 安裝介面時，不經思索即直接按下同樣的按鈕，然後輸入同樣的資訊？ 在安裝完成之後，才突然想到「我忘了在系統管理員角色中指定 DBA 群組」。 現在，您必須花費寶貴的時間，進入單一使用者模式、新增適當的使用者或群組、多使用者模式啟用 SQL 備份，然後進行測試。 更糟的是，現在您對整個安裝的信心都受到動搖。 「我還忘了什麼事？」 我自己經常遇到這種情況。

此時需要 [PowerShell Desired State Configuration (DSC)](https://docs.microsoft.com/powershell/dsc/overview)。 藉由 DSC，我能建置一份可在成千上百部伺服器上重複使用的設定範本。 視組建而定，我可能需要調整一些設定參數，不過這沒什麼大不了，我仍然得以保留所有標準設定。 如果我因整晚照顧小孩而睡眠不足，以至於隔天忘了輸入重要參數，這樣的設計有助於避免這類情況的發生。

在本文中，我將探討如何使用 SqlServerDsc DSC 資源，對 Windows Server 2016 上的獨立 SQL Server 2017 執行個體進行初始設定。 由於我不會探討 DSC 的運作方式，因此事先稍微了解 DSC 會很有幫助。

本逐步解說需要下列項目：

- 執行 Windows Server 2016 的電腦
- SQL Server 2017 安裝媒體
- SqlServerDsc DSC 資源 (10.0.0.0 版是本文撰寫時的版本)

## <a name="prerequisites"></a>Prerequisites

在大多數情況下，將會使用 DSC 來處理必要條件需求。 不過，基於此示範的目的，我將手動處理必要條件。

## <a name="install-the-sqlserverdsc-dsc-resource"></a>安裝 SqlServerDsc DSC 資源

您可以使用 [Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1) Cmdlet，從 [PowerShell 資源庫](https://www.powershellgallery.com/)下載 [SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc) DSC 資源。 注意：請確保 PowerShell 以「系統管理員身分」執行，以便安裝模組。

```PowerShell
Install-Module -Name SqlServerDsc
```

取得 SQL Server 2017 安裝媒體 請將 SQL Server 2017 安裝媒體下載到伺服器。 我已從我的 Visual Studio 訂用帳戶下載 SQL Server 2017 Enterprise，並將 ISO 複製到 "C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso"。

現在 ISO 必須解壓縮至目錄。

```PowerShell
New-Item -Path C:\SQL2017 -ItemType Directory
$mountResult = Mount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso' -PassThru
$volumeInfo = $mountResult | Get-Volume
$driveInfo = Get-PSDrive -Name $volumeInfo.DriveLetter
Copy-Item -Path ( Join-Path -Path $driveInfo.Root -ChildPath '*' ) -Destination C:\SQL2017\ -Recurse
Dismount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso'
```

## <a name="create-the-configuration"></a>建立設定

### <a name="configuration"></a>組態

建立組態函數，之後會呼叫此函數產生[受控物件格式 (MOF)](https://docs.microsoft.com/windows/desktop/WmiSdk/managed-object-format--mof-) 文件。

```PowerShell
Configuration SQLInstall
{...}
```

### <a name="modules"></a>模組

將模組匯入目前的工作階段。 這些模組會指示設定文件如何建置 MOF 文件，並指示 DSC 引擎如何將 MOF 文件套用至伺服器。

```PowerShell
Import-DscResource -ModuleName SqlServerDsc
```

### <a name="resources"></a>資源

#### <a name="net-framework"></a>.NET Framework

SQL Server 需要 .NET Framework，因此我們必須確保已安裝該項目，再安裝 SQL Server。 將使用 WindowsFeature 資源來安裝 Net-Framework-45-Core Windows 功能。

```PowerShell
WindowsFeature 'NetFramework45'
{
     Name = 'Net-Framework-45-Core'
     Ensure = 'Present'
}
```

#### <a name="sqlsetup"></a>SqlSetup

SqlSetup 資源可用來指示 DSC 如何安裝 SQL Server。 基本安裝所需的參數包括：

- **InstanceName**：執行個體的名稱。 若是預設執行個體，請使用 MSSQLSERVER。
- **Features**：要安裝的功能。 在此範例中，我只要安裝 SQLEngine 功能。
- **SourcePath**：SQL 安裝媒體的路徑。 在此範例中，我已將 SQL 安裝媒體儲存在 "C:\SQL2017"。 您可以利用網路共用，將伺服器上所使用的空間降到最低。
- **SQLSysAdminAccounts**：要成為系統管理員角色成員的使用者或群組。 在此範例中，我要將系統管理員存取權授與本機系統管理員群組。 注意：在高度安全的環境中不建議使用此設定。

[SqlServerDsc GitHub 存放庫](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlsetup)提供 SqlSetup 上可用參數的完整清單和描述。

SqlSetup 資源並不完全，因為它只會安裝 SQL，不會維護所套用的設定。 例如，如果在安裝時指定 SQLSysAdminAccounts，系統管理員可能會將登入新增至系統管理員角色或從中移除，SqlSetup 資源並不會在意。 如果需要 DSC 實行系統管理員角色的成員資格，則應該利用 [SqlServerRole](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlserverrole) 資源。

#### <a name="complete-configuration"></a>完成設定

```PowerShell
Configuration SQLInstall
{
     Import-DscResource -ModuleName SqlServerDsc

     node localhost
     {
          WindowsFeature 'NetFramework45'
          {
               Name   = 'NET-Framework-45-Core'
               Ensure = 'Present'
          }

          SqlSetup 'InstallDefaultInstance'
          {
               InstanceName        = 'MSSQLSERVER'
               Features            = 'SQLENGINE'
               SourcePath          = 'C:\SQL2017'
               SQLSysAdminAccounts = @('Administrators')
               DependsOn           = '[WindowsFeature]NetFramework45'
          }
     }
}
```

## <a name="build-and-deploy"></a>建置和部署

### <a name="compile-the-configuration"></a>編譯設定

對設定指令碼執行點溯源：

```PowerShell
. .\SQLInstallConfiguration.ps1
```

執行組態函數：

```PowerShell
SQLInstall
```

目錄會在名為 "SQLInstall" 的工作目錄中建立，並包含名為 "localhost.mof" 的檔案。 查看 MOF 的內容將會顯示編譯的 DSC 設定。

### <a name="deploy-the-configuration"></a>部署設定

若要啟動 SQL Server 的 DSC 部署，請呼叫 Start-DscConfiguration Cmdlet。 提供給 Cmdlet 的參數包括：

- **Path**：包含所要部署 MOF 文件的資料夾路徑。 (例如 "C:\SQLInstall")。
- **Wait**：等候設定工作完成。
- **Force**：覆寫任何現有的 DSC 設定。
- **Verbose**：顯示詳細資訊輸出。 第一次推送設定時可用來協助進行疑難排解。

```PowerShell
Start-DscConfiguration -Path C:\SQLInstall -Wait -Force -Verbose
```

套用此設定時，詳細資訊輸出會顯示目前發生的狀況，讓您欣然感受到某事正在發生。 只要沒有擲回任何錯誤 (紅色文字)，當畫面上顯示 "Operation 'Invoke CimMethod' complete." /[作業 'Invoke CimMethod' 完成/]  時，SQL 即安裝完成。

## <a name="validate-installation"></a>驗證安裝

### <a name="dsc"></a>DSC

[Test-DscConfiguration](https://docs.microsoft.com/powershell/module/psdesiredstateconfiguration/test-dscconfiguration) Cmdlet 可用來判斷伺服器 (在本例中為 SQL 安裝) 的目前狀態是否符合所需的狀態。 Test-DscConfiguration 的結果應為 "True"。

```PowerShell
PS C:\> Test-DscConfiguration
True
```

### <a name="services"></a>服務

服務清單現在應該傳回 SQL Server 服務

```PowerShell
PS C:\> Get-Service -Name *SQL*
Status  Name           DisplayName
------  ----           -----------
Running MSSQLSERVER    SQL Server (MSSQLSERVER)
Stopped SQLBrowser     SQL Server Browser
Running SQLSERVERAGENT SQL Server Agent (MSSQLSERVER)
Running SQLTELEMETRY   SQL Server CEIP service (MSSQLSERVER)
Running SQLWriter      SQL Server VSS Writer
```

### <a name="sql-server"></a>[SQL Server]

```PowerShell
PS C:\> & sqlcmd -S $env:COMPUTERNAME
1> SELECT @@SERVERNAME
2> GO
1> quit
```

## <a name="see-also"></a>另請參閱

[Windows PowerShell Desired State Configuration 概觀](https://docs.microsoft.com/powershell/dsc/overview)

[從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

[使用設定檔安裝 SQL Server](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)

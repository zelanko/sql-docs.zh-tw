---
title: 下載 SQL Server PowerShell 模組
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: carlrab
ms.custom: ''
ms.date: 01/23/2020
ms.openlocfilehash: 99976a12ae76254da5b50c5467df9d9e42fdbbce
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "76920351"
---
# <a name="install-the-sql-server-powershell-module"></a>安裝 SQL Server PowerShell 模組

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文提供安裝 **SqlServer** PowerShell 模組的指示。

## <a name="powershell-modules-for-sql-server"></a>適用於 SQL Server 的 PowerShell 模組

有兩個 SQL Server PowerShell 模組：

- **SqlServer**：SqlServer 模組包含可支援最新 SQL 功能的新 Cmdlet。 此模組也包含 **SQLPS** 中 Cmdlet 的更新版本。 若要下載 SqlServer 模組，請移至 [PowerShell 資源庫中的 SqlServer 模組](https://www.powershellgallery.com/packages/Sqlserver)。
- **SQLPS**：SQLPS 模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。

> [!NOTE]
> PowerShell 資源庫中的 **SqlServer** 模組版本支援版本設定，而且需要 PowerShell 5.0 版或更新版本。

如需說明主題，請移至：

- [SqlServer](https://docs.microsoft.com/powershell/module/sqlserver) \(英文\) Cmdlet。
- [SQLPS](https://docs.microsoft.com/powershell/module/sqlps) \(英文\) Cmdlet。

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

SQL Server Management Studio (SSMS)，從 17.0 版開始，兩個 PowerShell 模組都不會安裝。 若要搭配 SSMS 使用 PowerShell，請從 [PowerShell 資源庫](https://www.powershellgallery.com/packages/Sqlserver) \(英文\) 安裝 **SqlServer** 模組。

> [!NOTE]
> 使用版本為 16.x 的 SSMS 時，舊版的 **SqlServer** 模組會隨附於 SQL Server Management Studio (SSMS)

## <a name="azure-data-studio"></a>Azure Data Studio

Azure Data Studio 不會安裝兩個 PowerShell 模組的任何一個。 若要搭配 Azure Data Studio 使用 PowerShell，請從 [PowerShell 資源庫](https://www.powershellgallery.com/packages/Sqlserver) \(英文\) 安裝 **SqlServer** 模組。

您可以使用 [PowerShell 擴充功能](../azure-data-studio/powershell-extension.md)，在 Azure Data Studio 中提供豐富的 PowerShell 編輯器支援。

## <a name="installing-or-updating-the-sqlserver-module"></a>安裝或更新 SqlServer 模組

若要從 PowerShell 資源庫安裝 **SqlServer** 模組，請以系統管理員身分啟動 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) 工作階段。 您也會以系統管理員身分啟動 Azure Data Studio，並在整合式終端機的 PowerShell 工作階段中執行這些命令。

### <a name="install-the-sqlserver-module"></a>安裝 SqlServer 模組

在您的 PowerShell 工作階段中執行下列命令，為所有使用者安裝 SqlServer 模組：

```powershell
Install-Module -Name SqlServer
```

### <a name="to-view-the-versions-of-the-sqlserver-module-installed"></a>若要檢視已安裝 SqlServer 模組的版本

執行下列命令來查看已安裝的 SqlServer 模組版本

```powershell
Get-Module SqlServer -ListAvailable
```

### <a name="install-for-the-current-user-rather-than-as-an-administrator"></a>為目前的使用者安裝，而非以系統管理員身分安裝

如果您無法以系統管理員身分執行 PowerShell 工作階段，請使用下列命令為目前的使用者安裝：

```powershell
Install-Module -Name SqlServer -Scope CurrentUser
```

### <a name="to-overwrite-a-previous-version-of-the-sqlserver-module"></a>若要覆寫先前版本的 SqlServer 模組

您也可以使用 `Install-Module` 命令來覆寫先前的版本。

```powershell
Install-Module -Name SqlServer -AllowClobber
```

> [!Note]
> PowerShell 會一律使用已安裝的最新模組。

### <a name="update-the-installed-version-of-the-sqlserver-module"></a>更新已安裝 SqlServer 模組的版本

當 **SqlServer** 模組的更新版本可供使用時，可以使用下列命令安裝較新的版本：

```powershell
Install-Module -Name SqlServer -AllowClobber
```

您可以使用 `Update-Module` 命令安裝最新版的 SQLServer PowerShell 模組，但不會移除較舊的版本。 它會以並存方式安裝較新的版本，讓您能夠試驗最新版本，但仍保留已安裝的舊版模組。

不過，如果您不想要保留較舊的模組版本，可以使用 `Uninstall-Module` 命令來移除先前的版本。

如果安裝了一個以上的版本，可以使用下列命令來列出：

```powershell
Get-Module SqlServer -ListAvailable
```

您可以使用下列命令移除較舊的版本：

```powershell
Uninstall-module -Name SQLServer -RequiredVersion "<version number>" -AllowClobber
```

### <a name="troubleshooting"></a>疑難排解

如果安裝時遇到問題，請參閱 [Install-Module 文件](https://www.powershellgallery.com/packages/PowerShellGet/2.2.1)和 [Install-Module 參考](https://docs.microsoft.com/powershell/module/powershellget/Install-Module)。

## <a name="using-a-specific-version-of-the-sqlserver-module"></a>使用特定版本的 SqlServer 模組

若要使用特定版本的模組，可以使用類似下列命令匯入具有特定版本號碼的模組：

```powershell
Import-Module SqlServer -Version 21.1.18080
```

## <a name="pre-release-versions-of-the-sqlserver-module"></a>SqlServer 模組的發行前版本

SqlServer 模組的發行前 (或「預覽」) 版本可在 PowerShell 資源庫取得。

> [!IMPORTANT]
> 您可以透過傳遞 *-AllowPrerelease* 切換參數，使用已更新的 *Find-Module* 與 *Install-Module* Cmdlet (屬於 [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) 模組) 來探索並安裝這些版本。 若要使用這些 Cmdlet，請安裝 PowerShellGet 模組，然後開啟新的工作階段。

### <a name="to-discover-pre-release-versions-of-the-sqlserver-module"></a>探索 SqlServer 模組的發行前版本

若要探索 SqlServer 模組的發行前 (預覽) 版本，請執行下列命令：

```powershell
Find-Module SqlServer -AllowPrerelease
```

### <a name="to-install-a-specific-pre-release-version-of-the-sqlserver-module"></a>若要安裝 SqlServer 模組的特定發行前版本

若要安裝模組的特定發行前版本，請使用特定版本號碼來安裝。

您可以嘗試使用下列命令：

```powershell
Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease
```

## <a name="sql-server-powershell-on-linux"></a>Linux 上的 SQL Server PowerShell

如需了解如何在 Linux 上安裝 SQL Server PowerShell，請瀏覽[使用 PowerShell Core 管理 Linux 上的 SQL Server](../linux/sql-server-linux-manage-powershell-core.md)。

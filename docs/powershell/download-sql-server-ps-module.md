---
title: 下載 SQL Server PowerShell 模組 | Microsoft Docs
ms.custom: ''
ms.date: 10/08/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
keywords:
- 安裝 SQL Server Powershell, 下載 SQL Server Powershell
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40873fe63b897da52fc9a7d440a8568872431d72
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851753"
---
# <a name="install-sql-server-powershell-module"></a>安裝 SQL Server PowerShell 模組
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文提供安裝 **SqlServer** PowerShell 模組的指示。
> [!NOTE]
> 有兩個 SQL Server PowerShell 模組： 
> * **SQLPS**：此模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。
> * **SqlServer**：此模組包含可支援最新 SQL 功能的新 Cmdlet。 此模組也包含 **SQLPS** 中 Cmdlet 的更新版本。 

舊版 **SqlServer** 模組隨附於 SQL Server Management Studio (SSMS)，但僅限 SSMS 16.x 版。 若要搭配 SSMS 17.0 和更新版本使用 PowerShell，則必須從 [PowerShell 資源庫](https://www.powershellgallery.com/packages/Sqlserver)安裝 **SqlServer** 模組。
最新版 **SqlServer** 模組是 21.0.17279。 這是以 Microsoft.SQLServer.SMO v140 版為基礎。  
如果您要尋找支援下一版 SQL Server (根據 Microsoft.SQLServer.SMO v150 版) 的模組版本，請參閱此頁面底部有關如何取得模組發行前版本的章節。 模組的最新發行前版本 21.1.18040-preview。

若要從 PowerShell 資源庫安裝 **SqlServer** 模組，請啟動 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) 工作階段並使用下列命令。 如果安裝時遇到問題，請參閱 [Install-Module 文件](https://docs.microsoft.com/powershell/gallery/psget/module/psget_install-module)和 [Install-Module 參考](https://docs.microsoft.com/powershell/module/powershellget/Install-Module)。

若要安裝 **SqlServer** 模組：

```Install-Module -Name SqlServer```

如果電腦上未安裝舊版 **SqlServer** 模組，您可以使用 `Update-Module` (如本文稍後所述)，或提供 `-AllowClobber` 參數：  

```Install-Module -Name SqlServer -AllowClobber```

如果您無法以系統管理員身分執行 PowerShell 工作階段，您可以針對目前使用者安裝：

```Install-Module -Name SqlServer -Scope CurrentUser```

若更新版的 **SqlServer** 模組已可使用，就可以使用 `Update-Module` 來更新版本：

```Update-Module -Name SqlServer```

若要檢視已安裝模組的版本：

```Get-Module SqlServer -ListAvailable```

若要使用特定版本的模組，您可以使用類似如下的特定版本號碼將它匯入：

```Import-Module SqlServer -Version 21.0.17178```

> [!NOTE]
> 模組的發行前版本 (或「預覽」) 版本可在 PowerShell 資源庫取得。 它們可能使用已更新的 *Find-Module* 和 *Install-Module* Cmdlet (屬於 [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) 模組) 探索，方法是傳遞 *-AllowPrerelease* 切換。
>
> 若要探索模組的發行前版本/預覽版本，您可以執行下列命令：
>
> ```Find-Module SqlServer -AllowPrerelease```
>
> 若要安裝模組的特定發行前版本/預覽版本，您可以使用類似如下的特定版本號碼來安裝它：
>
> ```Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease```
> 

PowerShell 資源庫中的 **SqlServer** 模組版本支援版本設定，而且需要 PowerShell 5.0 版或更新版本。 

* [PowerShell 資源庫中的 SqlServer 模組](https://www.powershellgallery.com/packages/Sqlserver) 
* [SqlServer Cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS Cmdlet](https://docs.microsoft.com/powershell/module/sqlps)

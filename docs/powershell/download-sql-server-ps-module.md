---
title: 下載 SQL Server PowerShell 模組 | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
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
ms.openlocfilehash: d41d03c3bba51b919a71f195de75a7ec29f51b7e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621556"
---
# <a name="install-sql-server-powershell-module"></a>安裝 SQL Server PowerShell 模組
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文提供安裝 **SqlServer** PowerShell 模組的指示。

> [!NOTE]
> 有兩個 SQL Server PowerShell 模組：**SqlServer** 和 **SQLPS**。 **SQLPS** 模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。 **SqlServer** 模組包含 **SQLPS** 中 Cmdlet 的更新版本，此外還加入新的 Cmdlet 以支援最新版 SQL 功能。 舊版 **SqlServer** 模組隨附於 SQL Server Management Studio (SSMS)，但僅限 SSMS 16.x 版。 若要搭配 SSMS 17.0 和更新版本使用 PowerShell，則必須從 PowerShell 資源庫安裝 **SqlServer** 模組。

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


PowerShell 資源庫中的 **SqlServer** 模組版本支援版本設定，而且需要 PowerShell 5.0 版或更新版本。 

* [PowerShell 資源庫中的 SqlServer 模組](https://www.powershellgallery.com/packages/Sqlserver) 
* [SqlServer Cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS Cmdlet](https://docs.microsoft.com/powershell/module/sqlps)

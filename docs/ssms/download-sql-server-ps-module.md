---
title: "下載 SQL Server PowerShell 模組 | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords: "安裝 SQL Server Powershell, 下載 SQL Server Powershell"
ms.assetid: 
caps.latest.revision: "113"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 208bf291819a3e847e784e76611acdec0bf2f2d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="download-sql-server-powershell-module"></a>下載 SQL Server PowerShell 模組
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] SQL Server PowerShell 模組是 SQL Server Management Studio 17.0 版的一部分，因此現在透過 PowerShell 資源庫來提供。  模組不再隨附於 SSMS 安裝封裝。 若要搭配使用 PowerShell 與 SSMS 17.0 及更新版本，SQL Server 模組必須以額外步驟的方式安裝在電腦上。

有關安裝最新版本的 Windows Management Framework 和如何安裝 PowerShell 模組的完整文件通常位於 [PowerShell 資源庫](https://www.powershellgallery.com/)網站上。

安裝 SQL Server 模組的 PowerShell 命令如下：

> Install-Module -Name SqlServer

此命令會安裝適用於電腦上所有使用者的模組。 您必須以系統管理員身分執行 PowerShell 處理序。

> Install-Module -Name SqlServer -Scope CurrentUser

此命令會安裝適用於執行 PowerShell 目前處理序之使用者的模組。 您無須使用系統管理員權限執行 PowerShell 處理序。

如果電腦上有舊版的 SQL Server PowerShell 模組，可能需要提供 "-AllowClobber" 參數。  

如果以系統管理員身分執行，且要安裝適用於電腦上所有使用者的模組

> Install-Module -Name SqlServer -AllowClobber

如果無法以系統管理員身分執行，或要安裝僅適用於目前使用者的模組

> Install-Module -Name SqlServer -Scope CurrentUser -AllowClobber

若更新版的 SqlServer 模組已可使用，就可以使用 Update-Module 命令來更新版本

> Update-Module -Name SqlServer

若要檢視安裝在電腦上的模組版本，可以使用

> Get-Module SqlServer -ListAvailable

若要在指令碼中使用特定版本的模組，可以使用此命令將其匯入

> Import-Module SqlServer -Version 21.0.17178

提供給 PowerShell 資源庫的 SQL Server PowerShell 模組版本支援版本設定，而且需要 PowerShell 5.0 版或更新版本。 您可以在 [PowerShell 資源庫](https://www.powershellgallery.com/packages/Sqlserver/)找到 SqlServer 模組 

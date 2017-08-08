---
title: "下載 SQL Server PowerShell 模組 | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安裝 SQL Server Powershell, 下載 SQL Server Powershell"
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="download-sql-server-powershell-module"></a>下載 SQL Server PowerShell 模組
作為 SQL Server Management Studio 17.0 版的一部分，SQL Server PowerShell 模組現在透過 PowerShell 資源庫提供。  模組不再隨附於 SSMS 安裝封裝。 若要搭配使用 PowerShell 與 SSMS 17.0 及更新版本，SQL Server 模組必須以額外步驟的方式安裝在電腦上。

有關安裝最新版本的 Windows Management Framework 和如何安裝 PowerShell 模組的完整文件通常位於 [PowerShell 資源庫](https://www.powershellgallery.com/)網站上。

安裝 SQL Server 模組的 PowerShell 命令如下：

> Install-module -Name SqlServer -Scope CurrentUser

如果電腦上有舊版的 SQL Server PowerShell 模組，可能需要提供 "-AllowClobber" 參數。  

提供給 PowerShell 資源庫的 SQL Server PowerShell 模組版本支援版本設定，而且需要 PowerShell 5.0 版或更新版本。


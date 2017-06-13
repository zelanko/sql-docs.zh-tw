---
title: "下載 SQL Server PowerShell 模組 |Microsoft 文件"
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
- "安裝 sql server powershell，請下載 sql server powershell"
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: zh-tw
ms.lasthandoff: 04/26/2017

---
# <a name="download-sql-server-powershell-module"></a>下載 SQL Server PowerShell 模組
過程 17.0 發行版本的 SQL Server Management Studio 中，SQL Server PowerShell 模組現在提供了透過 PowerShell 資源庫。  模組不再隨附於 SSMS 安裝套件。 若要使用 SSMS 17.0 及更新版本，請使用 PowerShell，SQL Server 模組必須安裝在電腦上做為額外的步驟。

完整的文件中有關安裝最新版本的 Windows Management Framework 和如何安裝 PowerShell 模組在一般情況下可以找到上[PowerShell 資源庫](https://www.powershellgallery.com/)站台。

若要安裝 SQL Server 單元的 PowerShell 命令為：

> Install-module-名稱 SqlServer-範圍 CurrentUser

如果您有舊版的電腦上的 SQL Server PowerShell 模組，它可能需要提供 「-AllowClobber"參數。  

出貨至 PowerShell Gallery 的 SQL Server PowerShell 模組版本支援版本控制，而且需要 PowerShell 5.0 或更新版本。


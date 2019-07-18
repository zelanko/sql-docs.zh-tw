---
title: 安裝 SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 1a2e4099350d72cbab6a91b75664ee031ee35a60
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794935"
---
# <a name="install-sql-server-powershell"></a>安裝 SQL Server PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會自動設定 PowerShell 元件。  

您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式安裝提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows PowerShell 支援的軟體。 當您選取需要 PowerShell 支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能時，安裝程式會安裝下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 元件：  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 嵌入式管理單元。這些嵌入式管理單元是可實作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之兩種 Windows PowerShell 支援的 dll 檔案：  
  
  - 一組 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令程式。 指令程式是實作特定動作的命令。 例如 **Invoke-Sqlcmd** 會執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 XQuery 指令碼 (此指令碼也可使用 **sqlcmd** 公用程式加以執行)，而 **Invoke-PolicyEvaluation** 則會報告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件是否符合原則型管理原則。  
  
  - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供者。 此提供者可讓您使用類似於檔案系統路徑的路徑來導覽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件階層。 每一個物件都與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件模型中的類別有關聯。 您可以使用此類別的方法和屬性來針對物件執行工作。 例如，如果您執行 cd 切換到路徑中的資料庫物件，您可以使用 Microsoft.SqlServer.Managment.SMO.Database 類別的方法和屬性來管理資料庫。  
 
- 將 **sqlps** 模組匯入 Windows PowerShell 工作階段以載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 嵌入式管理單元。  
 
- [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 支援從物件總管樹狀結構啟動 Windows PowerShell 工作階段。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式支援 Windows PowerShell 作業步驟。  
  
Windows Server 2012 及更新版本和 Windows 8 及更新版本，會安裝並設定 PowerShell。 如需安裝 Windows PowerShell 的資訊，請參閱[安裝 Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell)。  

如需詳細資訊，請參閱：   

- [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  

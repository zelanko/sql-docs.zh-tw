---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c7181877fcc1fa7553b5e11508bc1c9425166ccd
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援 Windows PowerShell，它是功能強大的指令碼處理介面，可讓系統管理員和開發人員將伺服器管理和應用程式部署自動化。 Windows PowerShell 語言可支援比 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼更複雜的邏輯，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員能夠建立功能強大的管理指令碼。 Windows PowerShell 指令碼也可用來管理其他 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 伺服器產品。 如此可為管理員提供跨伺服器的通用指令碼語言。  
  
## <a name="sql-server-powershell-components"></a>SQL Server PowerShell 元件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供名稱為 **sqlps** 的 Windows PowerShell 模組，用來將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件匯入 Windows PowerShell 環境或指令碼。 **sqlps** 模組載入兩個 Windows PowerShell 嵌入式管理單元，可用來實作：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供者，可啟用類似於檔案系統路徑的簡單導覽機制。 您可以建立類似於檔案系統路徑的路徑，其中的磁碟機與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件模型有關聯，而且節點是根據物件模型類別。 然後，您可以使用熟悉的命令 (例如 **cd** 和 **dir** ) 來巡覽路徑，其方式類似於在命令提示字元視窗中巡覽資料夾。 您可以使用其他命令 (例如 **ren** 或 **del**)，在路徑中的節點上執行動作。  
  
-   一組 Cmdlet，這些是 Windows PowerShell 指令碼中用來指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 動作的命令。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cmdlet 可支援一些動作，例如執行包含 **或 XQuery 陳述式的** sqlcmd [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。  
  
 若要了解 Windows PowerShell，請參閱 [開始使用 Windows PowerShell](https://msdn.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell)。  
  
## <a name="sql-server-versions"></a>SQL Server 版本  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] PowerShell 元件可用來管理 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 或更新版本的執行個體。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的執行個體必須執行 SP2 或更新版本。 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的執行個體必須執行 SP4 或更新版本。 當 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] PowerShell 元件搭配舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用時，其功能限制為這些版本中的可用功能。  
     
## <a name="sql-server-powershell-tasks"></a>SQL Server PowerShell 工作  
  
|工作描述|主題|  
|----------------------|-----------| 
|安裝 Microsoft® Windows PowerShell Extensions for Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時預設會安裝 PowerShell 模組。  您可以安裝下列 Microsoft® SQL Server® 2016 Feature Pack 元件，手動安裝 PowerShell Extensions for SQL Server 2016：<br/>     Microsoft® System CLR Types for Microsoft SQL Server® 2016 (SQLSysClrTypes.msi)<br/>Microsoft® SQL Server® 2016 共用管理物件 (SharedManagementObjects.msi)<br/> Microsoft® Windows PowerShell Extensions for Microsoft SQL Server® 2016 (PowerShellTools.msi)|[Microsoft® SQL Server® 2016 Feature Pack](https://www.microsoft.com/en-us/download/details.aspx?id=52676)。   | 
|描述用於執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 元件的慣用機制、開啟 PowerShell 工作階段，以及載入 **sqlps** 模組。 **sqlps** 模組會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 提供者和 Cmdllet，以及提供者和 Cmdllet 所使用的 SQL Server 管理物件 (SMO) 組件中載入。|[匯入 SQLPS 模組](../../relational-databases/scripting/import-the-sqlps-module.md)|  
|描述如何在沒有提供者或 Cmdllet 的情況下，只載入 SMO 組件。|[載入 Windows PowerShell 中的 SMO 組件](../../relational-databases/scripting/load-the-smo-assemblies-in-windows-powershell.md)|  
|描述如何以滑鼠右鍵按一下 **物件總管**中的節點，來執行 Windows PowerShell 工作階段。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 會啟動 Windows PowerShell 工作階段、載入 **sqlps** 模組，以及將 SQL Server 提供者路徑設為選取的物件。|[從 SQL Server Management Studio 執行 Windows PowerShell](../../relational-databases/scripting/run-windows-powershell-from-sql-server-management-studio.md)|  
|描述如何建立可執行 Windows PowerShell 指令碼的 SQL Server Agent 作業步驟。 然後，就可以排程在特定時間或為回應事件而執行作業。|[在 SQL Server Agent 中執行 Windows PowerShell 步驟](../../relational-databases/scripting/run-windows-powershell-steps-in-sql-server-agent.md)|  
|描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供者來導覽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件的階層。|[SQL Server PowerShell 提供者](../../relational-databases/scripting/sql-server-powershell-provider.md)|  
|描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cmdllet，以指定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 動作 (例如，執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼)。|[使用 Database Engine Cmdlet](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)|  
|描述如何指定含有 Windows PowerShell 不支援字元的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分隔識別碼。|[PowerShell 中的 SQL Server 識別碼](../../relational-databases/scripting/sql-server-identifiers-in-powershell.md)|  
|描述如何進行 SQL Server 驗證連接。 依預設，SQL Server PowerShell 元件會以執行 Windows PowerShell 之處理序的 Windows 認證來使用 Windows 驗證連接。|[管理 Database Engine PowerShell 中的驗證](../../relational-databases/scripting/manage-authentication-in-database-engine-powershell.md)|  
|描述如何使用 SQL Server PowerShell 提供者所實作的變數來控制使用 Windows PowerShell Tab 完成時列出的物件數目。 這對於處理包含大量物件的資料庫特別有用。|[管理 TAB 鍵自動完成 &#40;SQL Server PowerShell&#41;](../../relational-databases/scripting/manage-tab-completion-sql-server-powershell.md)|  
|描述如何使用 Get-Help 取得 Windows PowerShell 環境中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的詳細資訊。|[取得 SQL Server PowerShell 說明](../../relational-databases/scripting/get-help-sql-server-powershell.md)|  
  
  


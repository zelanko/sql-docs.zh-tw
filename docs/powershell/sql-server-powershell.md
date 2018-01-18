---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
caps.latest.revision: "10"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: ab19a8a86bba6cbdacbc0c7de1b44d42a263b692
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2018
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**[安裝 SQL Server PowerShell](download-sql-server-ps-module.md)**

> [!NOTE]
> 有兩個 SQL Server PowerShell 模組：**SqlServer** 和 **SQLPS**。 **SQLPS** 模組隨附於 SQL Server 安裝 (基於回溯相容性)，但不再更新。 最新版 PowerShell 模組是 **SqlServer** 模組。 **SqlServer** 模組包含 **SQLPS** 中 Cmdlet 的更新版本，此外還加入新的 Cmdlet 以支援最新版 SQL 功能。  
> 舊版 **SqlServer** 模組隨附於 SQL Server Management Studio (SSMS)，但僅限 SSMS 16.x 版。 若要搭配 SSMS 17.0 和更新版本使用 PowerShell，則必須從 PowerShell 資源庫安裝 **SqlServer** 模組。
> 若要安裝 **SqlServer** 模組，請參閱[安裝 SQL Server PowerShell](download-sql-server-ps-module.md)。

**為什麼模組未從 SQLPS 變更為 SqlServer？**

為了提供 SQL PowerShell 更新，我們必須變更 SQL PowerShell 模組的識別，以及稱為 *SQLPS.exe* 的包裝函式。 由於這項項變更，現在有兩個 SQL PowerShell 模組：**SqlServer** 模組和 **SQLPS** 模組。  

**如果您的 PowerShell 指令碼匯入 SQLPS 模組，請更新指令碼。**

如果您有任何執行 `Import-Module -Name SQLPS` 的 PowerShell 指令碼，並想充分利用新的提供者功能和新的 Cmdlet，您必須將其變更為 `Import-Module -Name SqlServer`。 新的模組會安裝到 `%Program Files\WindowsPowerShell\Modules\SqlServer`。 因此，您不需要更新 $env:PSModulePath 變數。 如果您有使用名為 **SqlServer** 之第三方或社群版模組的指令碼，請使用 Prefix 參數來避免發生名稱衝突。 SQL Server Agent 所使用的模組沒有任何變更。 

  
## <a name="sql-server-powershell-components"></a>SQL Server PowerShell 元件  
**SqlServer** 模組載入兩個 Windows PowerShell 嵌入式管理單元：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者，可啟用類似於檔案系統路徑的簡單導覽機制。 您可以建立類似於檔案系統路徑的路徑，其中的磁碟機與 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理物件模型有關聯，而且節點是根據物件模型類別。 然後，您可以使用熟悉的命令 (例如 **cd** 和 **dir** ) 來巡覽路徑，其方式類似於在命令提示字元視窗中巡覽資料夾。 您可以使用其他命令 (例如 **ren** 或 **del**)，在路徑中的節點上執行動作。  
  
-   一組 Cmdlet，可支援一些動作，例如執行包含 [!INCLUDE[tsql](../includes/tsql-md.md)] 或 XQuery 陳述式的 **sqlcmd** 指令碼。  
  
  
## <a name="sql-server-versions"></a>SQL Server 版本  
SQL PowerShell Cmdlet 可用來管理 Azure SQL Database、Azure SQL 資料倉儲及所有[支援的 SQL Server 產品](https://support.microsoft.com/lifecycle/search/1044)執行個體。  


## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>含有 PowerShell 路徑不支援之字元的 SQL Server 識別碼  
 
**Encode-Sqlname** 和 **Decode-Sqlname** Cmdlet 可協助您指定內含 PowerShell 路徑所不支援之字元的 SQL Server 識別碼。 如需詳細資訊，請參閱 [SQL Server Identifiers in PowerShell](sql-server-identifiers-in-powershell.md)。  
  
使用 **Convert-UrnToPath** Cmdlet 將 [!INCLUDE[ssDE](../includes/ssde-md.md)] 物件的唯一資源名稱轉換為 SQL Server PowerShell 提供者的路徑。 如需詳細資訊，請參閱 [Convert URNs to SQL Server Provider Paths](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath)。  
  
## <a name="query-expressions-and-unique-resource-names"></a>查詢運算式和唯一的資源名稱  

查詢運算式是使用類似 XPath 語法的一些字串，可用以指定在物件模型階層中列舉一個或多個物件的準則集合。 唯一的資源名稱 (URN) 是可唯一識別單一物件的特定查詢運算式字串類型。 如需詳細資訊，請參閱 [Query Expressions and Uniform Resource Names](query-expressions-and-uniform-resource-names.md)。       


## <a name="cmdlet-reference"></a>Cmdlet 參考
* [SqlServer Cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS Cmdlet](https://docs.microsoft.com/powershell/module/sqlps)

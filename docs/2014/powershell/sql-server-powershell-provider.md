---
title: SQL Server PowerShell 提供者 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- PowerShell [SQL Server], provider
- PowerShell [SQL Server], SQL Server PowerShell Provider
- Providers [PowerShell]
- SMO [SQL Server], PowerShell
- PowerShell [SQL Server], SMO
- SQL Server Management Objects, PowerShell
ms.assetid: b97acc43-fcd2-4ae5-b218-e183bab916f9
caps.latest.revision: 60
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: ddf348be91cd8f3a298d1ef4fcd2711a81a6f275
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132208"
---
# <a name="sql-server-powershell-provider"></a>SQL Server PowerShell 提供者
  適用於 Windows PowerShell 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者會公開類似於檔案系統路徑之路徑中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件階層。 您可以使用路徑來尋找物件，然後使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理物件 (SMO) 模型中的方法來針對物件執行動作。  
  
## <a name="benefits-of-the-sql-server-powershell-provider"></a>SQL Server PowerShell 提供者的優點  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者所實作的路徑可以輕鬆並以互動方式檢閱 SQL Server 執行個體中所有的物件。 您可以使用 Windows PowerShell 別名來導覽路徑，而別名類似於一般用來導覽檔案系統路徑的命令。  
  
## <a name="the-sql-server-powershell-hierarchy"></a>SQL Server PowerShell 階層  
 可以在階層中表示資料或物件模型的產品會使用 Windows PowerShell 提供者來公開階層。 這個階層是使用與 Windows 檔案系統所使用之磁碟機和路徑結構類似的結構公開。  
  
 每個 Windows PowerShell 提供者都會實作一或多個磁碟機， 每一個磁碟機都是相關物件階層的根節點。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者會實作 SQLSERVER: 磁碟機。 該提供者也會針對 SQLSERVER: 磁碟機定義一組主要資料夾。 每個資料夾及其子資料夾都代表可使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理物件模型存取的一組物件。 當您將焦點放在以其中一個主資料夾為開頭之路徑的子資料夾上時，就可以使用相關聯物件模型中的方法，針對此節點所表示的物件來執行動作。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 提供者實作的 Windows PowerShell 資料夾列在下表中。  
  
|資料夾|SQL Server 物件模型命名空間|物件|  
|------------|---------------------------------------|-------------|  
|SQLSERVER:\SQL|<xref:Microsoft.SqlServer.Management.Smo><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Agent><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Broker><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Mail>|資料庫物件，例如資料表、檢視表和預存程序。|  
|SQLSERVER:\SQLPolicy|<xref:Microsoft.SqlServer.Management.Dmf><br /><br /> <xref:Microsoft.SqlServer.Management.Facets>|以原則為基礎的管理物件，例如原則和 Facet。|  
|SQLSERVER:\SQLRegistration|<xref:Microsoft.SqlServer.Management.RegisteredServers><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>|已註冊的伺服器物件，例如伺服器群組和已註冊的伺服器。|  
|SQLSERVER:\Utility|<xref:Microsoft.SqlServer.Management.Utility>|公用程式物件，例如， [!INCLUDE[ssDE](../includes/ssde-md.md)]的受管理的執行個體。|  
|SQLSERVER:\DAC|<xref:Microsoft.SqlServer.Management.DAC>|資料層應用程式物件 (如 DAC 封裝) 與作業 (如部署 DAC)。|  
|SQLSERVER:\DataCollection|<xref:Microsoft.SqlServer.Management.Collector>|資料收集器物件，例如收集組和組態存放區。|  
|SQLSERVER:\IntegrationServices|<xref:Microsoft.SqlServer.Management.IntegrationServices>|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件，例如專案、封裝和環境。|  
|SQLSERVER:\SQLAS|<xref:Microsoft.AnalysisServices>|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件，例如 Cube、彙總和維度。|  
  
 例如，您可以使用 SQLSERVER:\SQL 資料夾來當做可代表 SMO 物件模型所支援之任何物件的路徑開頭。 SQLSERVER:\SQL 路徑的前置部分是 SQLSERVER:\SQL\\*ComputerName*\\*InstanceName*。 執行個體名稱之後的節點會在物件集合 (例如「資料庫」或「檢視」) 和物件名稱 (例如 AdventureWorks2012) 之間輪替。 結構描述不會表示為物件類別。 當您在結構描述中指定最上層物件的節點 (如資料表或檢視表) 時，必須使用 *SchemaName.ObjectName*格式來指定物件名稱。  
  
 這是本機電腦上預設 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體中 AdventureWorks2012 資料庫之 Purchasing 結構描述的 Vendor 資料表路徑：  
  
```  
SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```  
  
 如需有關 SMO 物件模型階層的詳細資訊，請參閱 [SMO 物件模型圖表](../relational-databases/server-management-objects-smo/smo-object-model-diagram.md)。  
  
 路徑中的集合節點會與相關聯物件模型中的集合類別產生關聯。 物件名稱節點會與相關聯物件模型中的物件類別產生關聯，如下表所示。  
  
|路徑|SMO 類別|  
|----------|---------------|  
|SQLSERVER:\SQL\MyComputer\DEFAULT\Databases|<xref:Microsoft.SqlServer.Management.Smo.DatabaseCollection>|  
|SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012|<xref:Microsoft.SqlServer.Management.Smo.Database>|  
  
## <a name="sql-server-provider-tasks"></a>SQL Server 提供者工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何使用 Windows PowerShell 指令程式導覽路徑中的節點，而且至少每個節點都會取得該節點的物件清單。|[導覽 SQL Server PowerShell 路徑](navigate-sql-server-powershell-paths.md)|  
|描述如何使用 SMO 方法和屬性，針對透過路徑中的節點所代表的物件來報告和執行工作。 同時描述如何取得該節點的 SMO 方法和屬性清單。|[使用 SQL Server PowerShell 路徑](work-with-sql-server-powershell-paths.md)|  
|描述如何將 SMO 統一資源名稱 (URN) 轉換為 SQL Server 提供者路徑。|[將 URN 轉換成 SQL Server 提供者路徑](../database-engine/convert-urns-to-sql-server-provider-paths.md)|  
|描述如何使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者來開啟 SQL Server 驗證連接。 提供者預設會使用的 Windows 驗證連接是使用執行 Windows PowerShell 工作階段之 Windows 帳戶的認證來進行。|[管理資料庫引擎 PowerShell 中的驗證](manage-authentication-in-database-engine-powershell.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
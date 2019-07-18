---
title: 工具和 Analysis Services 中使用的應用程式 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d3ecb5de4c70c09bc367b9008f5d62c6a23faef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162292"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Analysis Services 中使用的工具和應用程式
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  尋找您需要建立 Analysis Services 模型的應用程式與工具，並管理部署的資料庫。  
  
## <a name="analysis-services-model-designers"></a>Analysis Services 模型設計師  
 使用專案範本在 SQL Server Data Tools (SSDT)，Visual Studio shell，被撰寫模型。 專案範本會提供模型設計工具用於建立組成 Analysis Services 方案的資料模型物件。 SSDT 是更新每個月的免費 web 下載。

 **[下載 SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)** 
  
 模型具有相容性層級設定，可決定功能可用性以及哪個版本的 Analysis Services 執行該模型。  是否可以指定給定的相容性層級取決於在部分模型設計工具。  
  
 表格式模型使用的最新的功能，例如 BIM 檔案，表格式 JSON 格式，雙向交叉篩選，必須建立或升級相容性層級 1200年或更高版本。  
  
 如果您需要較低的相容性層級，可能是因為您想要部署的模型是舊版的 Analysis Services，您可以仍然使用模型設計師在 SSDT 中。 較新版本的工具支援建立任何模型類型 （表格式或多維度），在任何相容性層級。   

## <a name="administrative-tools"></a>系統管理工具  
  
 SQL Server Management Studio (SSMS) 是所有的 SQL Server 功能，包括 Analysis Services 的主要系統管理工具。 SSMS 是免費的 web 下載項目每月更新。 
  
**[下載 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)** 
  
 SSMS 包含擴充的事件 (xEvents)，以提供用於監視的活動和診斷的問題，SQL Server 2016 和 Azure Analysis Services 伺服器上的 SQL Server Profiler 追蹤的輕量型替代方案。 如需詳細資訊，請參閱 [使用 SQL Server 擴充事件監視 Analysis Services](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 。  
  
### <a name="sql-server-profiler"></a>SQL Server Profiler  
 雖然 SQL Server Profiler 已正式取代為 xEvents，但是它是監視連接、MDX 查詢執行和其他伺服器作業的熟悉方式。 SQL Server Profiler 是預設會安裝的元件。 您可以發現與應用程式上的 SQL Server 應用程式在 Windows 中。  
  
### <a name="powershell"></a>PowerShell  
 您可以使用 PowerShell 命令來執行許多系統管理工作。 請參閱[PowerShell 參考](../analysis-services/powershell/analysis-services-powershell-reference.md)如需詳細資訊。  
  
### <a name="community-and-third-party-tools"></a>社群與協力廠商工具  
 如需社群程式碼範例，請造訪 [Analysis Services codeplex 頁面](http://sqlsrvanalysissrvcs.codeplex.com/) 。 當您在尋找支援 Analysis Services 之協力廠商工具的建議時，[論壇](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) 是相當實用的資源。  
  
## <a name="see-also"></a>另請參閱  
 [多維度資料庫的相容性層級](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [表格式模型的相容性層級](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  

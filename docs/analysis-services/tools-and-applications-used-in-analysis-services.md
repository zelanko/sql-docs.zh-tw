---
title: "工具和 Analysis Services 中使用的應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 05/11/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: cedca243acc9608e2d3855b2ee7ee2aa183c1d73
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Analysis Services 中使用的工具和應用程式
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]尋找工具和應用程式所需的建立 Analysis Services 模型和管理部署資料庫。  
  
## <a name="analysis-services-model-designers"></a>Analysis Services 模型設計師  
 使用專案範本中 SQL Server Data Tools (SSDT)，Visual Studio shell 中撰寫模型。 專案範本提供模型設計人員建立組成 Analysis Services 方案的資料模型物件。 SSDT 是更新每個月的免費 web 下載。

 **[下載 SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)** 
  
 模型具有相容性層級設定，可決定功能可用性以及哪個版本的 Analysis Services 執行該模型。  是否可以指定給定的相容性層級是取決於在部分由模型設計師。  
  
 表格式模型使用的最新的功能，例如 BIM 檔案，表格式 JSON 格式和雙向交叉篩選，必須建立或升級相容性層級 1200年或更高。  
  
 如果您需要較低的相容性層級，可能是因為您想要部署的模型是舊版的 Analysis Services，您仍然可以使用模型設計師在 SSDT 中。 較新版本的工具支援建立任何模型類型 （表格式或多維度），在任何相容性層級。   

## <a name="administrative-tools"></a>系統管理工具  
  
 SQL Server Management Studio (SSMS) 是所有的 SQL Server 功能，包括 Analysis Services 的主要系統管理工具。 SSMS 是更新每個月的免費 web 下載。 
  
**[下載 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)** 
  
 SSMS 包括擴充的事件 (xEvents)，提供用於監視活動和診斷的問題，SQL Server 2016 和 Azure Analysis Services 伺服器上的 SQL Server Profiler 追蹤的輕量型替代品。 如需詳細資訊，請參閱 [使用 SQL Server 擴充事件監視 Analysis Services](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 。  
  
### <a name="sql-server-profiler"></a>SQL Server Profiler  
 雖然 SQL Server Profiler 已正式取代為 xEvents，但是它是監視連接、MDX 查詢執行和其他伺服器作業的熟悉方式。 SQL Server Profiler 是預設會安裝的元件。 您可以使用 SQL Server 應用程式在應用程式上找到它在 Windows 中。  
  
### <a name="powershell"></a>PowerShell  
 您可以使用 PowerShell 命令來執行許多系統管理工作。 請參閱[PowerShell 參考](../analysis-services/powershell/analysis-services-powershell-reference.md)如需詳細資訊。  
  
### <a name="community-and-third-party-tools"></a>社群與協力廠商工具  
 如需社群程式碼範例，請造訪 [Analysis Services codeplex 頁面](http://sqlsrvanalysissrvcs.codeplex.com/) 。 當您在尋找支援 Analysis Services 之協力廠商工具的建議時，[論壇](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) 是相當實用的資源。  
  
## <a name="see-also"></a>請參閱  
 [多維度資料庫的相容性層級](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [相容性層級的表格式模型](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  

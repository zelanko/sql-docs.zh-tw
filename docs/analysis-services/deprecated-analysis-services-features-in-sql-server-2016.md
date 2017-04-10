---
title: "SQL Server 2016 中已被取代的 Analysis Services 功能 | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services, 回溯相容性"
  - "SSAS, 回溯相容性"
  - "SQL Server Analysis Services, backward compatibility"
  - "已被取代的功能 [Analysis Services]"
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
caps.latest.revision: 52
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 52
---
# SQL Server 2016 中已被取代的 Analysis Services 功能
  *「已被取代的功能」* (Deprecated Feature) 是指產品的未來版本中將會移除，但目前版本為了維持回溯相容性仍會支援並包含的功能。 一般而言，已被取代的功能會在主要版本中移除，通常是在原始宣告的兩個版本內。 例如， [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 可能不會支援 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]中所宣告之已被取代的功能。  
  
 **SQL Server 的下一個主要版本不支援下列項目**  
  
|||  
|-|-|  
|**類別目錄**|**功能**|  
|多維度|遠端分割區|  
|多維度|遠端連結量值群組|  
|多維度|維度回寫|  
|多維度|連結維度|  
  
 **SQL Server 的未來版本不支援下列項目**  
  
|||  
|-|-|  
|**類別目錄**|**功能**|  
|多維度|用於主動式快取的 SQL Server 資料表通知。  <br />取代為使用輪詢進行主動式快取。 <br />請參閱[主動式快取 &#40;維度&#41;](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md) 和[主動式快取 &#40;資料分割&#41;](../Topic/Proactive%20Caching%20\(Partitions\).md)。|  
|多維度|工作階段 Cube。 沒有取代項目。|  
|多維度|本機 Cube。 沒有取代項目。|  
|表格式|未來版本將不支援表格式模型 1100 和 1103 相容性層級。 取代為在相容性層級 1200 設定模型，並將模型定義轉換成表格式中繼資料。 請參閱 [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。|  
|工具|SQL Server Profiler for Trace Capture<br /><br /> 取代為使用 SQL Server Management Studio 內嵌的擴充事件分析工具。  <br /> 請參閱 [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)。|  
|工具|Server Profiler for Trace Replay <br />取代。 沒有取代項目。|  
|追蹤管理物件和 Trace API|Microsoft.AnalysisServices.Trace 物件 (包含 Analysis Services Trace 和 Replay 物件的 API)。 取代為多部分：<br /><br /> -   追蹤組態︰ Microsoft.SqlServer.Management.XEvent<br />-   追蹤讀取︰ Microsoft.SqlServer.XEvent.Linq<br />-   追蹤重新執行：無|  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中所宣告之先前已被取代的功能仍然有效。 因為尚未從產品中移除支援這些功能的程式碼，所以許多功能仍會在此版本中。 雖然您可能無法存取先前已被取代的功能，但這些功能仍視為已被取代，並且可能會在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 發行期間的任何時候從產品中實際移除。 強烈建議您避免在以 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 之 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]為基礎的任何新模型或應用程式中，使用已被取代的功能。  
  
## 請參閱＜  
 [Analysis Services Backward Compatibility](../analysis-services/analysis-services-backward-compatibility.md)   
 [SQL Server 2016 中已停止的 Analysis Services 功能](../analysis-services/discontinued-analysis-services-functionality-in-sql-server-2016.md)  
  
  
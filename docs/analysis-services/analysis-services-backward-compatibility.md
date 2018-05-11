---
title: SQL Server 2016 Analysis Services 回溯相容性 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4906f3aec097b0bbdf63187cd760aa17a450316a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="analysis-services-backward-compatibility-sql-server-2016"></a>Analysis Services 回溯相容性 (SQL Server 2016)
[!INCLUDE[ssas-appliesto-sql2016](../includes/ssas-appliesto-sql2016.md)]

這篇文章描述功能可用性及目前的版本和舊版之間的行為變更。

## <a name="deprecated-features"></a>已被取代的功能
A*已被取代功能*會停止從產品在未來版本中，但仍支援，且包含在目前版本為了維持回溯相容性。 建議您停止在新的和現有的專案中使用已被取代的功能，為了維持與未來發行版本的相容性。
  
在此版本中已被取代的下列功能：
  
|||  
|-|-|  
|**模式/類別**|**功能**|  
|多維度|遠端分割區|  
|多維度|遠端連結量值群組|  
|多維度|維度回寫|  
|多維度|連結維度|   
|多維度|用於主動式快取的 SQL Server 資料表通知。  <br />取代為使用輪詢進行主動式快取。 <br />請參閱[主動式快取 &#40;維度&#41;](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md) 和[主動式快取 &#40;資料分割&#41;](../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|多維度|工作階段 Cube。 沒有取代項目。|  
|多維度|本機 Cube。 沒有取代項目。|  
|表格式|未來版本將不支援表格式模型 1100 和 1103 相容性層級。 取代為 1200年或更高版本，將模型定義轉換成表格式中繼資料，在相容性層級設定模型。 請參閱 [Analysis Services 中表格式模型的相容性層級](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。|  
|工具|SQL Server Profiler for Trace Capture<br /><br /> 取代為使用 SQL Server Management Studio 內嵌的擴充事件分析工具。  <br /> 請參閱 [使用 SQL Server 擴充事件監視 Analysis Services](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)。|  
|工具|Server Profiler for Trace Replay <br />取代。 沒有取代項目。|  
|追蹤管理物件和 Trace API|Microsoft.AnalysisServices.Trace 物件 (包含 Analysis Services Trace 和 Replay 物件的 API)。 取代為多部分：<br /><br /> 追蹤組態： Microsoft.SqlServer.Management.XEvent<br />追蹤讀取： Microsoft.SqlServer.XEvent.Linq<br />-   追蹤重新執行：無|  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中所宣告之先前已被取代的功能仍然有效。 因為尚未從產品中移除支援這些功能的程式碼，所以許多功能仍會在此版本中。 先前已被取代的功能時可能會存取，他們仍會視為已被取代，而實際上可能會移除從產品在任何時間。  

## <a name="discontinued-features"></a>已停止的功能
A*已停止的功能*先前的版本中已被取代。 它包含在目前版本中，可以繼續，但已不再支援。 已停止的功能可能會移除整個未來版本或更新。

下列功能已被取代的舊版本，並且不再支援此版本中。

|||  
|-|-|  
|**功能**|**取代或因應措施**|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|無。 此功能在 SQL Server 2005 中已遭取代。|  
|[CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)|無。 此功能在 SQL Server 2005 中已遭取代。|  
|NON_EMPTY_BEHAVIOR 查詢最佳化工具提示|無。 此功能在 SQL Server 2008 中已遭取代。|  
|COM 組件|無。 此功能在 SQL Server 2008 中已遭取代。|  
|CELL_EVALUATION_LIST 內建資料格屬性|無。 此功能在 SQL Server 2005 中已遭取代。|  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中所宣告之先前已被取代的功能仍然有效。 因為尚未從產品中移除支援這些功能的程式碼，所以許多功能仍會在此版本中。 先前已被取代的功能時可能會存取，他們仍會視為已被取代，而實際上可能會移除從產品在任何時間。  

## <a name="breaking-changes"></a>重大變更
「重大變更」會導致資料模型、應用程式程式碼或指令碼在升級模型或伺服器之後無法運作。
  
### <a name="net-40-version-upgrade"></a>.NET 4.0 版本升級  
 Analysis Services 管理物件 (AMO)、 ADOMD.NET 和表格式物件模型 (TOM) 用戶端程式庫現在 runtime 為目標的.NET 4.0。 這可能是以 .NET 3.5 為目標之應用程式的重大變更。 使用這些組件之更新版本的應用程式現在必須以 .NET 4.0 或更新版本為目標。  
  
### <a name="amo-version-upgrade"></a>AMO 版本升級  
 此版本是版本升級為[Analysis Services 管理物件&#40;AMO&#41; ](https://msdn.microsoft.com/library/mt436122.aspx)和在某些情況下是重大變更。  現有可呼叫 AMO 的程式碼和指令碼將會繼續執行，就和從舊版升級之前一樣。 不過，如果您需要*重新編譯*您應用程式，以及設為目標的 SQL Server 2016 Analysis Services 執行個體，您必須新增下列命名空間，讓您的程式碼或指令碼運作：  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 每當您參考程式碼中的 Microsoft.AnalysisServices 組件，就會需要 [Microsoft.AnalysisServices.Core](https://msdn.microsoft.com/library/microsoft.analysisservices.core.aspx) 命名空間。 如果物件在表格式和多維度狀況中依相同的方式使用，則先前僅存在於 **Microsoft.AnalysisServices** 命名空間內的物件，在此版本中將會移至核心命名空間。  例如，與伺服器相關的 API 將重新放置到核心命名空間。  
  
 雖然現在有多個命名空間，且都存在於相同的組件中 (Microsoft.AnalysisServices.dll)。  
  
### <a name="xevent-discover-changes"></a>XEvent DISCOVER 變更  
 若要更妥善支援 XEvent 會探索 SQL Server 2016 Analysis services，資料流在 SSMS 中`DISCOVER_XEVENT_TRACE_DEFINITION`取代為下列 XEvent 追蹤：  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  

## <a name="behavior-changes"></a>行為變更
*「行為變更」* (behavior change) 會影響功能在目前版本中，與舊版 SQL Server 相較之下的運作或互動方式。
  
預設值修訂、完成升級或還原功能所需的手動組態或現有功能的新實作，全部都是產品中的行為變更範例。
  
這裡會列出本版本中的已變更但不會中斷現有模型或程式碼後置升級的功能行為。
  
### <a name="analysis-services-in-sharepoint-mode"></a>SharePoint 模式的 Analysis Services
 不再需要執行 [Power Pivot 組態精靈] 作為後續安裝工作。 這是適用於所有支援的 SharePoint 版本，從目前的 SQL Server 2016 Analysis Services 載入模型。
  
### <a name="directquery-mode-for-tabular-models"></a>表格式模型的 DirectQuery 模式
 *DirectQuery* 是表格式模型的資料存取模式，其中，會對後端關聯式資料庫執行查詢執行，以即時擷取結果集。 這通常用於無法放入記憶體的極大型資料集，或是資料是暫時性的而且您想要有表格式模型的查詢中所傳回的最新資料時。
  
 DirectQuery 已是最後數個版本的資料存取模式。 SQL Server 2016 Analysis Services 中已稍微修訂實作，假設表格式模型為 1200年或更高的相容性層級。 DirectQuery 的限制比以前少。 它也有不同的資料庫屬性。
  
 如果您在現有表格式模型中使用 DirectQuery，則可以保留模型的目前相容性層級 1100 或 1103，並繼續使用 DirectQuery 作為這些層級的實作。 或者，您可以升級為 1200年或更高受益於 DirectQuery 進行的增強功能。
  
 為 DirectQuery 模型沒有就地升級，因為從舊版的相容性層級設定的較新的 1200年 （含） 以上的相容性層級中沒有確切對應項目。 如果您有現有的表格式模型在 DirectQuery 模式下執行，您應該在 SQL Server Data Tools 中開啟模型、 關閉 DirectQuery、 將設定**相容性層級**屬性為 1200年或更高，，然後重新設定 DirectQuery屬性。 請參閱[DirectQuery 模式](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)如需詳細資訊。


## <a name="see-also"></a>另請參閱
[Analysis Services 回溯相容性 (SQL Server 2017)](analysis-services-backward-compatibility-sql2017.md)

---
title: "SQL Server 2017 Analysis Services 回溯相容性 |Microsoft 文件"
ms.date: 07/11/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing Analysis Services, backward compatibility
- backward compatibility [Analysis Services]
- compatibility [Analysis Services]
- Analysis Services, backward compatibility
- upgrading Analysis Services
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
ms.assetid: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 6419c75df8a5b6742b102a3f56adfa7e2efd9ef1
ms.openlocfilehash: 630c835cf7be720ad235b0f33bb093ac5a1ed926
ms.contentlocale: zh-tw
ms.lasthandoff: 10/03/2017

---
# <a name="analysis-services-backward-compatibility-sql-2017"></a>Analysis Services 回溯相容性 (SQL 2017)
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

這篇文章描述功能可用性及目前的版本和舊版之間的行為變更。

## <a name="deprecated-features"></a>已被取代的功能
A*已被取代功能*會停止從產品在未來版本中，但仍支援，且包含在目前版本為了維持回溯相容性。 建議您停止在新的和現有的專案中使用已被取代的功能，為了維持與未來發行版本的相容性。

在此版本中已被取代的下列功能：
  
|||  
|-|-|  
|**模式/類別**|**功能**|
|多維度|資料採礦|
|多維度|遠端連結量值群組|
|表格式|模型 1100年和 1103年相容性層級|
|表格式|表格式物件模型的屬性： Column.TableDetailPosition，Column.IsDefaultLabel，Column.IsDefaultImage|


## <a name="discontinued-features"></a>已停止的功能
A*已停止的功能*先前的版本中已被取代。 它包含在目前版本中，可以繼續，但已不再支援。 已停止的功能可能會移除整個未來版本或更新。

下列功能已被取代的舊版本，並且不再支援此版本中。
  
|||  
|-|-|  
|**模式/類別**|**功能**|  
|表格式|VertipaqPagingPolicy 記憶體屬性值 (2)，啟用分頁至磁碟使用記憶體對應檔案。|
|多維度|遠端分割區|  
|多維度|遠端連結量值群組|  
|多維度|維度回寫|  
|多維度|連結維度|
|工具|SQL Server Profiler for Trace Capture<br /><br /> 取代為使用 SQL Server Management Studio 內嵌的擴充事件分析工具。  <br /> 請參閱 [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)。|  
|工具|Server Profiler for Trace Replay <br />取代。 沒有取代項目。|  
|追蹤管理物件和 Trace API|Microsoft.AnalysisServices.Trace 物件 (包含 Analysis Services Trace 和 Replay 物件的 API)。 取代為多部分：<br /><br /> -   追蹤組態︰ Microsoft.SqlServer.Management.XEvent<br />-   追蹤讀取︰ Microsoft.SqlServer.XEvent.Linq<br />-   追蹤重新執行：無|  

## <a name="breaking-changes"></a>重大變更
A*中斷變更*升級至目前的版本之後造成功能、 資料模型、 應用程式程式碼或指令碼會無法再運作。

在此版本中有任何重大變更。

## <a name="behavior-changes"></a>行為變更
A*行為變更*都會影響在目前的版本相較於舊版的相同功能的運作方式。 描述重要行為所做的變更。 不包含使用者介面中的變更。

MDSCHEMA_MEASUREGROUP_DIMENSIONS 和 DISCOVER_CALC_DEPENDENCY，變更中詳述[的新功能 Analysis Services 的 SQL Server 2017 CTP 2.1](https://blogs.msdn.microsoft.com/analysisservices/2017/05/18/whats-new-in-sql-server-2017-ctp-2-1-for-analysis-services/)公告。


## <a name="see-also"></a>另請參閱
[Analysis Services 回溯相容性 (SQL Server 2016)](analysis-services-backward-compatibility.md)


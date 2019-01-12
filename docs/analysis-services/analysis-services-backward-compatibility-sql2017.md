---
title: SQL Server 2017 Analysis Services 回溯相容性 |Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 411fa78bada76c79d4a869d68c94abf752b8466a
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2019
ms.locfileid: "54185074"
---
# <a name="analysis-services-backward-compatibility-sql-2017"></a>Analysis Services 回溯相容性 (SQL 2017)
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

這篇文章說明功能可用性和目前的版本與舊版之間的行為變更。

## <a name="deprecated-features"></a>即將淘汰的功能
A*已被取代功能*將不再從產品在未來的版本中，但仍支援且包含在目前版本為了維持回溯相容性。 建議您停止使用新的和現有的專案中的已被取代的功能，為了相容於未來的版本。 文件不會更新已被取代的功能。

在此版本中已被取代的下列功能：
  
|||  
|-|-|  
|**模式/類別**|**功能**|
|多維度|資料採礦|
|多維度|遠端連結量值群組|
|表格式|模型 1100年和 1103年相容性層級|
|表格式|表格式物件模型屬性：Column.TableDetailPosition，Column.IsDefaultLabel，Column.IsDefaultImage|
|工具|SQL Server Profiler for Trace Capture<br /><br /> 取代為使用 SQL Server Management Studio 內嵌的擴充事件分析工具。  <br /> 請參閱 [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)。|  
|工具|Server Profiler for Trace Replay <br />取代。 沒有取代項目。|  
|追蹤管理物件和 Trace API|Microsoft.AnalysisServices.Trace 物件 (包含 Analysis Services Trace 和 Replay 物件的 API)。 取代為多部分：<br /><br /> -追蹤組態︰Microsoft.SqlServer.Management.XEvent<br />-追蹤讀取︰Microsoft.SqlServer.XEvent.Linq<br />-追蹤重新執行：None|  


## <a name="discontinued-features"></a>已停止的功能
A*已停止的功能*先前的版本中已被取代。 它可能會繼續包含在目前的版本中，但不受支援。 已停止的功能可能會移除完全在未來版本或更新。

下列功能先前的版本中已被取代，並且不再支援此版本中。
  
|||  
|-|-|  
|**模式/類別**|**功能**|  
|表格式|VertipaqPagingPolicy 記憶體屬性值 (2)，啟用分頁至磁碟使用記憶體對應檔案。|
|多維度|遠端分割區|  
|多維度|遠端連結量值群組|  
|多維度|維度回寫|  
|多維度|連結維度|


## <a name="breaking-changes"></a>重大變更
A*重大變更*導致後面的升級至目前版本的功能、 資料模型、 應用程式程式碼或指令碼無法再運作。

在此版本中有任何重大變更。

## <a name="behavior-changes"></a>行為變更
A*行為變更*會影響相同的功能相較於舊版的目前版本中的運作方式。 說明只有重大行為變更。 找不到包含的使用者介面中的變更。

MDSCHEMA_MEASUREGROUP_DIMENSIONS 和 DISCOVER_CALC_DEPENDENCY，變更詳述[的新功能 Analysis Services 的 SQL Server 2017 CTP 2.1](https://blogs.msdn.microsoft.com/analysisservices/2017/05/18/whats-new-in-sql-server-2017-ctp-2-1-for-analysis-services/)公告。


## <a name="see-also"></a>另請參閱
[Analysis Services 回溯相容性 (SQL Server 2016)](analysis-services-backward-compatibility.md)

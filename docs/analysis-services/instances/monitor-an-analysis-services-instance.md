---
title: 監視 Analysis Services 執行個體概觀 |Microsoft Docs
ms.date: 11/16/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 39cc5a22165d07aafce29e4216548c4e8d226892
ms.sourcegitcommit: b51edbe07a0a2fdb5f74b5874771042400baf919
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/28/2019
ms.locfileid: "55087627"
---
# <a name="monitoring-overview"></a>監視概觀
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services 有數個不同的工具，可協助您監視與微調伺服器的效能。 要選擇的工具依據要做的監視或微調類型，以及要監視的特殊事件而定。

如需有關如何監視 SQL Server Analysis Services 的詳細資訊，請參閱 < [SQL Server 2008 R2 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)。  
  
## <a name="monitoring-tools"></a>監視工具  

|工具  |描述  |
|---------|---------|
|[SQL Server Profiler](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)      |   會追蹤引擎處理事件。 它也會擷取這些事件，讓您監視伺服器和資料庫活動相關資料。      |
| [擴充事件](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)     |   輕量型追蹤和效能監視系統，其會使用系統資源非常少，因此診斷生產與測試伺服器上的問題的理想工具。       |
| [動態管理檢視&#40;Dmv&#41;](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)      |   傳回模型物件、 伺服器作業和伺服器健全狀況的相關資訊的查詢。 查詢中，SQL，基礎是結構描述資料列集介面。      |
| [追蹤事件](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)     |  透過擷取然後分析執行個體所產生的追蹤事件，請遵循活動的執行個體。 追蹤事件已分組，因此您可以更輕鬆地找到相關追蹤事件。        |
|   [效能計數器](../../analysis-services/instances/performance-counters-ssas.md)\*    |    使用效能監視器可以透過效能計數器來監視 Microsoft SQL Server Analysis Services (SSAS) 執行個體的效能。     |
|[記錄作業](../../analysis-services/instances/performance-counters-ssas.md)\*|SQL Server Analysis Services 執行個體會記錄伺服器通知、 錯誤和警告至 msmdsrv.log 檔案-一個用於您所安裝的每個執行個體。 |

\* 只適用於 SQL Server 分析服務。

## <a name="see-also"></a>另請參閱

[監視 Azure Analysis Services 伺服器計量](https://docs.microsoft.com/azure/analysis-services/analysis-services-monitor)   
[設定 Azure Analysis services 的診斷記錄](https://docs.microsoft.com/azure/analysis-services/analysis-services-logging)

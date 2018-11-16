---
title: 使用 SQL Server Profiler 監視 Analysis Services |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 190ae82b43f7a4f311d358ea9597a10cd5cc39dc
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51704033"
---
# <a name="use-sql-server-profiler-to-monitor-analysis-services"></a>Use SQL Server Profiler to Monitor Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 會追蹤引擎處理事件 (例如批次或交易的開始) 和擷取關於這些事件的資料，如此可讓您監視伺服器和資料庫活動 (例如，使用者查詢或登入活動)。 您可將 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料擷取至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或檔案供稍後進行分析，也可以在相同或其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上重新執行擷取的事件以查看確實發生的狀況。 您可以即時或逐步重新執行事件。 在相同電腦上執行追蹤事件以及 Performance 計數器也很有用。 Profiler 可以依據時間建立這兩者的相互關聯，並沿著時間軸線將它們一起顯示。 Performance 計數器提供的是彙總檢視，而追蹤事件則會提供詳細資料。 如需如何建立和執行追蹤的相關資訊，請參閱 [建立 Profiler 追蹤以重新執行 &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)。  
  
 下表描述此章節的主題。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[使用 SQL Server Profiler 監視 Analysis Services 簡介](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)|描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來監視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。|  
|[建立 Profiler 追蹤以重新執行 &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)|描述使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]建立重新執行之追蹤的需求。|  
|[Analysis Services 追蹤事件](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)|描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 事件類別。 這些事件類別會對應到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 產生的動作，並用於追蹤重新執行。|  
  

  
  

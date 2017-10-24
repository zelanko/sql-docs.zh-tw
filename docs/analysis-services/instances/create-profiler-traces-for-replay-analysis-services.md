---
title: "建立 Profiler 追蹤以重新執行 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- replaying queries
- replaying discovers
- events [Analysis Services]
- replaying commands
- Profiler [SQL Server Profiler], Analysis Services
- performance [Analysis Services], replays
- traces [Analysis Services]
ms.assetid: 93b2fc46-7cfb-4ab5-abeb-1475a7d6f0f2
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c992aa2f5d666b38290b928bf44e6e5680ba701e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-profiler-traces-for-replay-analysis-services"></a>建立 Profiler 追蹤以重新執行 (Analysis Services)
  若要重新執行由使用者提交到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的查詢、探索和命令，[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 必須蒐集所需的事件。 若要起始收集這些事件，必須在 [追蹤屬性] 對話方塊的 [事件選取範圍] 索引標籤中選取適當的事件類別。 例如，若選取 Query Begin 事件類別，則會收集包含查詢的事件並用於重新執行。 另外，在分散式環境中，追蹤檔案包含足夠的資訊來支援以原始交易順序重新執行伺服器交易。  
  
## <a name="replay-for-queries"></a>查詢的重新執行  
 若要重新執行查詢， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 必須擷取下列事件：  
  
-   Audit Login 事件類別及其所有資料行。 此事件類別提供有關登入的使用者與工作階段設定的資訊。 伺服器處理序識別碼 (SPID) 提供對使用者工作階段的參考。 如需詳細資訊，請參閱 [安全性稽核資料行](../../analysis-services/trace-events/security-audit-data-columns.md)。  
  
-   Query Begin 事件類別及其所有資料行。 此事件類別提供有關提交給 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之查詢的資訊。 事件子類別資料行提供有關查詢類型的資訊。 TextData 資料行提供查詢的實際文字。 RequestParameters 資料行提供用於參數化查詢的參數，而 RequestProperties 資料行則提供 XML for Analysis (XMLA) 要求的屬性。 如需詳細資訊，請參閱 [查詢事件資料行](../../analysis-services/trace-events/queries-events-data-columns.md)。  
  
-   Query End 事件類別及其所有資料行。 此事件類別會確認查詢執行的狀態。 如需詳細資訊，請參閱 [查詢事件資料行](../../analysis-services/trace-events/queries-events-data-columns.md)。  
  
## <a name="replay-for-discovers"></a>探索的重新執行  
 若要重新執行探索， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 必須擷取下列事件：  
  
-   Audit Login 事件類別及其所有資料行。 此事件類別提供有關登入的使用者與工作階段設定的資訊。 SPID 提供對使用者工作階段的參考。 如需詳細資訊，請參閱 [安全性稽核資料行](../../analysis-services/trace-events/security-audit-data-columns.md)。  
  
-   Discover Begin 事件類別及其所有資料行。 TextData 資料行提供\<RequestType > discover 要求中，部分 RequestProperties 資料行提供\<屬性 > 探索要求的一部分。 EventSubclass 資料行提供探索類型。 如需詳細資訊，請參閱 [探索事件資料行](../../analysis-services/trace-events/discover-events-data-columns.md)。  
  
-   Discover End 事件類別及其所有資料行。 此事件類別會確認探索要求的狀態。 如需詳細資訊，請參閱 [探索事件資料行](../../analysis-services/trace-events/discover-events-data-columns.md)。  
  
## <a name="replay-for-commands"></a>命令的重新執行  
 若要重新執行命令， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 必須擷取下列事件：  
  
-   Command Begin 事件類別及其所有資料行。 TextData 資料行提供命令詳細資料，例如處理類型、資料庫識別碼和 Cube 識別碼。 RequestParameters 資料行提供用於參數化命令的參數，而 RequestProperties 資料行則提供 XMLA 要求的屬性。 如需詳細資訊，請參閱 [命令事件資料行](../../analysis-services/trace-events/command-events-data-columns.md)。  
  
-   Command End 事件類別及其所有資料行。 此事件類別會確認命令的狀態。 如需詳細資訊，請參閱 [命令事件資料行](../../analysis-services/trace-events/command-events-data-columns.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md)   
 [使用 SQL Server Profiler 監視 Analysis Services 簡介](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  


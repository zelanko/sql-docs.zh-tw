---
title: 建立 Profiler 追蹤以重新執行 (Analysis Services) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 64e32e2fb933d0dd11df06ae0283d165cfd8d351
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="create-profiler-traces-for-replay-analysis-services"></a>建立 Profiler 追蹤以重新執行 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

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
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md)   
 [監視 Analysis Services with SQL Server Profiler 簡介](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)  
  
  

---
title: Analysis Services 追蹤事件 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 69d7e1a435a6e2d5e0d831802680aeb9a8ad60f1
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2018
---
# <a name="analysis-services-trace-events"></a>Analysis Services 追蹤事件
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以透過擷取然後分析執行個體所產生的追蹤事件，來追蹤 Microsoft SQL Server Analysis Services (SSAS) 執行個體的活動。  追蹤事件已分組，因此您可以更輕鬆地找到相關追蹤事件。  每個追蹤事件都包含與該事件相關的一組資料；並不是所有資料片段都與所有事件相關。  
  
 追蹤事件可透過 **[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]** 來啟動和擷取 (請參閱 [使用 SQL Server Profiler 監視 Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md))，也可以從 XMLA 命令啟動做為 **SQL Server 擴充事件** 並在稍後分析 (請參閱 [使用 SQL Server 擴充事件監視 Analysis Services](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md))。  
  
 下表描述每個事件類別目錄以及類別目錄中的事件。 每個表格包含下列資料行：  
  
**事件識別碼**  
 可唯一識別事件類型的整數值。 在您讀取轉換為資料表或 XML 檔案的追蹤以篩選事件類型時，此值會很實用。  
  
**事件名稱**  
 在 Analysis Services 用戶端應用程式中指定給事件的名稱。  
  
**事件描述**  
 事件的簡短描述  
  
 **[命令事件的事件類別目錄](../../analysis-services/trace-events/command-events-event-category.md)**  
  
 命令之事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|15|命令開始|命令開始。|  
|16|命令結束|命令結束。|  
  
 **[探索事件的事件類別目錄](../../analysis-services/trace-events/discover-events-event-category.md)**  
  
 探索要求之事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|36|探索開始|探索要求開始。|  
|38|探索結束|探索要求結束。|  
  
 **[探索伺服器狀態事件類別目錄](../../analysis-services/trace-events/discover-server-state-event-category.md)**  
  
 伺服器狀態探索之事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|33|伺服器狀態探索的開始|伺服器狀態探索的開始。|  
|34|伺服器狀態探索資料|伺服器狀態探索回應的內容。|  
|35|伺服器狀態探索的結束|伺服器狀態探索的結束。|  
  
 **[錯誤和警告事件類別目錄](../../analysis-services/trace-events/errors-and-warnings-event-category.md)**  
  
 伺服器錯誤之事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|17|錯誤|伺服器錯誤。|  
  
 **[檔案載入及儲存事件目錄](../../analysis-services/trace-events/file-load-and-save-event-category.md)**  
  
 用於檔案載入及儲存作業報告之事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|90|檔案載入開始|檔案載入開始。|  
|91|檔案載入結束|檔案載入結束。|  
|92|檔案儲存開始|檔案儲存開始。|  
|93|檔案儲存結束|檔案儲存結束|  
|94|PageOut 開始|PageOut 開始。|  
|95|PageOut 結束|PageOut 結束|  
|96|PageIn 開始|PageIn 開始。|  
|97|PageIn 結束|PageIn 結束|  
  
 **[Lock 事件類別目錄](../../analysis-services/trace-events/lock-events-category.md)**  
  
 鎖定相關事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|50|死結|中繼資料鎖定死結。|  
|51|鎖定逾時。|中繼資料鎖定逾時。|  
|52|取得的鎖定|取得的鎖定|  
|53|釋放的鎖定|釋放的鎖定|  
|54|正在等候的鎖定|正在等候的鎖定|  
  
 **[通知事件的事件類別目錄](../../analysis-services/trace-events/notification-events-event-category.md)**  
  
 通知事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|39|通知|通知事件。|  
|40|使用者定義|使用者定義事件。|  
  
 **[進度報表事件類別目錄](../../analysis-services/trace-events/progress-reports-event-category.md)**  
  
 進度報表事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|5|進度報表開始|進度報表開始。|  
|6|進度報表結束|進度報表結束。|  
|7|進度報表目前事件|目前的進度報表。|  
|8|進度報表錯誤|進度報表錯誤。|  
  
 **[查詢事件類別目錄](../../analysis-services/trace-events/queries-events-category.md)**  
  
 查詢之事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|9|查詢開始|查詢開始。|  
|10|查詢結束|查詢結束。|  
  
 **[查詢處理事件類別目錄](../../analysis-services/trace-events/query-processing-events-category.md)**  
  
 查詢執行過程中主要事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|70|查詢 Cube 開始|查詢 Cube 開始。|  
|71|查詢 Cube 結束|查詢 Cube 結束。|  
|72|計算非空白開始|計算非空白開始。|  
|73|計算非空白目前|計算非空白目前。|  
|74|計算非空白結束|計算非空白結束。|  
|75|序列化結果開始|序列化結果開始。|  
|76|序列化結果目前|序列化結果目前。|  
|77|序列化結果結束|序列化結果結束。|  
|78|執行 MDX 指令碼開始|執行 MDX 指令碼開始。|  
|79|執行 MDX 指令碼目前|執行 MDX 指令碼目前。 已被取代。|  
|80|執行 MDX 指令碼結束|執行 MDX 指令碼結束。|  
|81|查詢維度|查詢維度。|  
|11|查詢 Subcube|查詢 Subcube 以用於基於使用方式的最佳化。|  
|12|查詢 Subcube 詳細資訊|查詢 Subcube 的詳細資訊。 開啟時，這個事件可能會對效能造成負面影響。|  
|60|從彙總取得資料|藉由從彙總取得資料來回答查詢。 開啟時，這個事件可能會對效能造成負面影響。|  
|61|從快取取得資料|藉由從其中一個快取取得資料來回答查詢。 開啟時，這個事件可能會對效能造成負面影響。|  
|82|VertiPaq SE 查詢開始|VertiPaq SE 查詢|  
|83|VertiPaq SE 查詢結束|VertiPaq SE 查詢|  
|84|資源使用狀況|在命令和查詢結束後報告讀取、寫入和 CPU 使用情況。|  
|85|VertiPaq SE 查詢快取比對|VertiPaq SE 查詢快取使用|  
|98|直接查詢開始|直接查詢開始。|  
|99|直接查詢結束|直接查詢結束。|  
  
 **[安全性稽核事件類別目錄](../../analysis-services/trace-events/security-audit-event-category.md)**  
  
 資料庫稽核事件類別的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|1|稽核登入|收集自啟動追蹤後的所有新連接事件，例如當用戶端要求連接到執行 SQL Server 執行個體的伺服器時。|  
|2|稽核登出|收集自啟動追蹤後的所有新中斷連接事件，例如當用戶端發出中斷連接命令時。|  
|4|稽核伺服器的啟動和停止|記錄服務關閉、啟動與暫停活動。|  
|18|稽核物件權限事件|記錄物件權限之變更。|  
|19|稽核管理作業事件|記錄伺服器備份/還原/同步處理/附加/卸離/影像載入/影像儲存。|  
  
 [工作階段事件的事件類別目錄](../../analysis-services/trace-events/session-events-event-category.md)  
  
 工作階段事件的集合。  
  
|**事件識別碼**|**事件名稱**|**事件描述**|  
|------------------|--------------------|---------------------------|  
|41|Existing Connection|現有的使用者連接。|  
|42|現有的工作階段|現有的工作階段。|  
|43|工作階段初始化|工作階段初始化。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Profiler 監視 Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
  

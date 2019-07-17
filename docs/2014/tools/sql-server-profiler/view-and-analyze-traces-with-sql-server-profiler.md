---
title: 使用 SQL Server Profiler 檢視和分析追蹤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], viewing traces
- SQL Server Profiler, viewing traces
- traces [SQL Server], viewing
- SQL Server Profiler, troubleshooting
- troubleshooting [SQL Server], traces
- events [SQL Server], finding inside trace
- Profiler [SQL Server Profiler], troubleshooting
- traces [SQL Server], events
ms.assetid: 17e821ca-a12e-4192-acc1-96765d9ae266
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd9b95821ee673e259273f880aefe8606fe81d71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211020"
---
# <a name="view-and-analyze-traces-with-sql-server-profiler"></a>使用 SQL Server Profiler 檢視和分析追蹤
  可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來檢視追蹤中擷取的事件資料。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 會根據定義的追蹤屬性來顯示資料。 分析 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的方法之一，是將資料複製到另一個程式，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 如果追蹤內包含 **Text** 資料行，則 Tuning Advisor 可以使用包含了 SQL 批次和遠端程序呼叫 (RPC) 事件的追蹤檔案。 為了確保能擷取正確的事件和資料行，以便用於 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor，請使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]隨附的預先定義「微調」範本。  
  
 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]開啟追蹤時，如果檔案是由 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 或「SQL 追蹤」系統預存程序建立，則追蹤檔案的副檔名不需要是 .trc。  
  
> [!NOTE]  
>  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 也可以讀取「SQL 追蹤」的 .log 檔案與泛用的 SQL 指令碼檔案。 開啟副檔名不是 .log 的「SQL 追蹤」 .log 檔 (例如 trace.txt) 時，請將檔案格式指定成 **SQLTrace_Log** 。  
  
 您可以設定 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 日期和時間的顯示格式，以協助追蹤分析。  
  
## <a name="troubleshooting-data"></a>疑難排解資料  
 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以使用 **Duration**、 **CPU**、 **Reads**或 **Writes** 資料行來分組追蹤或追蹤檔案，以針對資料進行疑難排解。 例如，執行效率差或邏輯讀取作業數過高的查詢，可能需要進行資料的疑難排解。  
  
 可透過將追蹤儲存到資料表，並使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來查詢事件資料而找出額外的資訊。 例如，若要判斷有哪些 **SQL:BatchCompleted** 事件的等候時間過量，請執行以下陳述式：  
  
```  
SELECT  TextData, Duration, CPU  
FROM    trace_table_name  
WHERE   EventClass = 12 -- SQL:BatchCompleted events  
AND     CPU < (Duration * 1000)  
```  
  
> [!NOTE]  
>  伺服器會以百萬分之一秒為單位 (百萬分之一秒，或 10<sup>-6</sup> 秒) 報告事件的持續時間，並以毫秒為單位 (千分之一秒，或 10<sup>-3</sup> 秒) 報告事件使用的 CPU 時間量。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 圖形化使用者介面依預設會以毫秒為單位來顯示 **Duration** 資料行，但是當追蹤儲存到檔案或資料庫資料表時，會以百萬分之一秒為單位來寫入 **Duration** 資料行值。  
  
## <a name="displaying-object-names-when-viewing-traces"></a>檢視追蹤時顯示物件名稱  
 如果想要顯示物件名稱而非物件識別碼 (**Object ID**)，則必須同時擷取 **Server Name** 、 **Database ID** 與 **Object Name** 資料行。  
  
 如果選擇要以 **Object ID** 資料行分組，請一定要先將 **Server Name** 與 **Database ID** 資料行分組，再以 **Object ID** 資料行來分組。 同樣地，如果選擇要以 **Index ID** 資料行分組，請一定要先將 **Server Name**、 **Database ID**與 **Object ID** 資料行分組，再以 **Index ID** 資料行來分組。 您必須採用這種分組順序，因為物件識別碼與索引識別碼在伺服器與資料庫 (以及在索引識別碼的物件) 之間並不是唯一的。  
  
## <a name="finding-specific-events-within-a-trace"></a>在追蹤中找出特定事件  
 若要在追蹤中尋找和分組事件，請遵循這些步驟：  
  
1.  建立您的追蹤。  
  
    -   定義追蹤時，請擷取 **Event Class**、**ClientProcessID** 與 **Start Time** 資料行，以及您想要擷取的其他資料行。 如需詳細資訊，請參閱[建立追蹤 &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)。  
  
    -   依照 **Event Class** 資料行來將擷取的資料分組，並將追蹤擷取到檔案或資料表中。 若要將擷取的資料分組，請在 [追蹤屬性] 對話方塊的 [事件選取範圍]  索引標籤上，按一下 [組織資料行]  。 如需詳細資訊，請參閱[組織追蹤內顯示的資料行 &#40;SQL Server Profiler&#41;](organize-columns-displayed-in-a-trace-sql-server-profiler.md)。  
  
    -   啟動追蹤，並在超過指定的時間或所擷取的事件數已達上限後停止追蹤。  
  
2.  找出目標事件。  
  
    -   開啟追蹤檔案或資料表，然後展開想要的事件類別節點；例如， **Deadlock Chain**。 如需詳細資訊，請參閱 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) 或 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)隨附的預先定義「微調」範本。  
  
    -   搜尋整個追蹤資料直到您找到要查看的事件為止 (請使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 之 [編輯]  功能表上的 [尋找]  命令來協助您在追蹤中尋找值)。 請注意位於追蹤事件之 **ClientProcessID** 與 **Start Time** 資料行的值。  
  
3.  在內容中顯示事件。  
  
    -   顯示追蹤屬性，並以 **ClientProcessID**資料行分組，而非以 **Event Class** 資料行。  
  
    -   將您要檢視的每一個用戶端處理序識別碼節點展開。 手動搜尋整個追蹤，或使用 [尋找]  直到您找出先前標註為目標事件之 [開始時間]  的值為止。 這些事件與屬於每一個選取之用戶端程序識別碼的其他事件，會依時間先後順序顯示出來。 例如，在追蹤內擷取的 **Deadlock** 和 **Deadlock Chain**事件，會緊接在所展開之用戶端處理序識別碼內的 **SQL:BatchStarting**事件後面出現。  
  
 要尋找任何已分組的事件可以使用相同的技術。 您找到要搜尋的事件之後，請依 **ClientProcessID**、 **ApplicationName**或是另一個事件類別來分組，以便按照事件的發生先後順序來檢視相關的活動。  
  
## <a name="see-also"></a>另請參閱  
 [檢視已儲存的追蹤 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-a-saved-trace-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)   
 [檢視篩選資訊 &#40;SQL Server Profiler&#41;](view-filter-information-sql-server-profiler.md)   
 [檢視篩選資訊 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-filter-information-transact-sql.md)   
 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md)   
 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)  
  
  

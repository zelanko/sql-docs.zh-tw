---
title: "修改追蹤範本 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "範本 [SQL Server], SQL Server Profiler"
  - "Profiler [SQL Server Profiler], 範本"
  - "追蹤範本 [SQL Server]"
  - "修改追蹤範本"
  - "SQL Server Profiler, 範本"
ms.assetid: 75b62a54-8d16-4599-bd2d-c42cfcc209f4
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# 修改追蹤範本
  您可以在執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的本機電腦上，修改儲存於檔案中的範本。 您也可以修改從這些檔案中衍生的範本。 當您修改現有的範本時，可在 [追蹤屬性] 對話方塊的 [事件選取範圍] 索引標籤上，以原本設定屬性的相同順序來編輯範本屬性，如事件類別與資料行。 事件類別與資料行可以新增或移除，且篩選也可以變更。 範本遭修改後，即會建立使用者特定範本，而原始系統範本則不受影響。 如需詳細資訊，請參閱[儲存追蹤及追蹤範本](../../tools/sql-server-profiler/save-traces-and-trace-templates.md)。  
  
 如果您不記得用來建立追蹤的原始範本 (或未儲存)，或者您日後想要執行相同的追蹤時，您可能需要從現有的追蹤檔中衍生範本。 使用現有的追蹤時，您可以檢視屬性，但是不能修改屬性。 若要修改屬性，請停止或暫停追蹤。 如需詳細資訊，請參閱[從追蹤檔案或追蹤資料表衍生範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md) 和[從執行中的追蹤衍生範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)。  
  
 **若要建立追蹤範本**  
  
 [建立追蹤範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
 **從追蹤範本執行追蹤**  
  
 [建立追蹤 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 **若要修改追蹤範本**  
  
 [使用 SQL Server Profiler](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)  
  
 [使用 Transact-SQL](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
 **若要從追蹤範本或追蹤檔中新增或移除事件**  
  
 [使用 SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [使用 Transact-SQL](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
## 另請參閱  
 [啟動追蹤](../../tools/sql-server-profiler/start-a-trace.md)  
  
  
---
title: "修改追蹤範本 (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "範本 [SQL Server], 追蹤"
  - "追蹤範本 [SQL Server]"
  - "修改追蹤"
ms.assetid: b81df2a1-e202-43d8-92b0-0beb145f0116
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 26
---
# 修改追蹤範本 (SQL Server Profiler)
  本主題說明如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來修改追蹤範本。  
  
### 若要修改追蹤範本  
  
1.  在 [檔案] 功能表上，指向 [範本]，再按一下 [編輯範本]。  
  
2.  在 [追蹤範本屬性] 對話方塊的 [一般] 索引標籤上，您可以修改伺服器類型和範本名稱，或選擇使用該伺服器類型的預設範本。  
  
3.  在 [事件選取範圍]索引標籤上，使用方格控制項，在追蹤檔案中新增或移除事件和資料行，如下所示：  
  
    -   若要加入事件，請在 **[事件]** 資料行中展開適當的事件類別目錄，然後選取事件名稱。  
  
    -   當您加入事件時，依預設將包含所有有關的資料行。 若要從追蹤中移除某個事件的資料行，請清除該事件在資料行中的核取方塊。  
  
    -   若要加入篩選，在 **[編輯篩選]** 對話方塊中按一下資料行名稱，然後指定篩選準則。 您也可以用滑鼠右鍵按一下資料行名稱，然後按一下 [編輯資料行篩選] 以啟動 [編輯篩選] 對話方塊。 按一下 **[確定]** 以加入篩選。  
  
4.  按一下 [儲存]，或按一下 [另存新檔]，以另一個名稱儲存追蹤範本。  
  
## 另請參閱  
 [指定追蹤檔案的事件及資料行 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [從執行中追蹤衍生範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [從追蹤檔案或追蹤資料表衍生範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler 範本和權限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
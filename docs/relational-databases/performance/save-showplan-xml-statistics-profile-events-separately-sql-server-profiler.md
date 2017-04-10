---
title: "個別儲存 Showplan XML 統計資料設定檔事件 (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Showplan XML 事件"
  - "儲存 Showplan XML 事件"
  - "事件 [SQL Server], 執行程序表 XML"
ms.assetid: df393f13-d538-4d94-8155-9c2fdf5f755d
caps.latest.revision: 20
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# 個別儲存 Showplan XML 統計資料設定檔事件 (SQL Server Profiler)
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，將在追蹤中所擷取的 **Showplan XML Statistics Profile** 事件，儲存至個別的 .SQLPlan 檔案中。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中開啟 **Showplan XML Statistics Profile** 事件檔案，以便檢視每個事件的圖形執行計畫。  
  
### 若要個別儲存 Showplan XML Statistics 事件  
  
1.  在 [檔案] 功能表上按一下 [新增追蹤]，然後連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
     會出現 [追蹤屬性]  對話方塊。  
  
    > [!NOTE]  
    >  若選取了 [進行連接後立即啟動追蹤]，則不會出現 [追蹤屬性] 對話方塊，而會開始進行追蹤。 於 [工具] 功能表，按一下 [選項]，並清除 [連接後立即啟動追蹤] 核取方塊，以關閉這項設定。  
  
2.  在 **[追蹤屬性]** 對話方塊的 **[追蹤名稱]** 方塊中，輸入追蹤的名稱。  
  
3.  在 [使用範本] 清單中，選取追蹤所依據的追蹤範本，若不使用範本則選取 [空白]。  
  
4.  執行下列其中之一：  
  
    -   按一下 [儲存至檔案]，將追蹤擷取至檔案。 在 **[設定最大檔案大小]**中指定一個值。  
  
         (選擇性) 選取 [啟用檔案換用] 及 [伺服器處理追蹤資料]。  
  
    -   按一下 [儲存至資料表]，將追蹤擷取至資料庫的資料表。  
  
         (選擇性) 按一下 **[設定最大資料列數]**，然後指定一個值。  
  
5.  (選擇性) 選取 [啟用追蹤停止時間] 核取方塊，然後指定停止日期和時間。  
  
6.  按一下 [事件選取範圍] 索引標籤。  
  
7.  在 [事件] 資料行中，展開 [效能] 事件類別目錄，然後選取 [Showplan XML Statistics Profile] 核取方塊。 如果沒有看到 **[Performance]** 事件類別目錄，請選取 **[顯示所有事件]** 來顯示它。  
  
     [事件擷取設定] 索引標籤會加入 [追蹤屬性] 對話方塊中。  
  
8.  在 [事件擷取設定] 索引標籤上，按一下 [個別儲存 XML 執行程序表事件]。  
  
9. 在 [另存新檔] 對話方塊中，輸入檔案名稱以儲存 **Showplan XML Statistics Profile** 事件。  
  
10. 按一下 [All batches in a single file (所有批次都在單一檔案中)]，將所有 **Showplan XML Statistics Profile** 事件儲存在單一 XML 檔案中；或按一下 [每一個 XML 執行程序表批次都在相異檔案中]，為每一個 **Showplan XML Statistics Profile** 事件個別建立新的 XML 檔案。  
  
11. 若要在 SQL Server Management Studio 中檢視 **Showplan XML Statistics Profile** 事件檔案，請在 [檔案] 功能表上指向 [開啟]，然後按一下 [檔案]。 導覽至您儲存 **Showplan XML Statistics Profile** 事件檔案的目錄，然後選取其中一個檔案並加以開啟。 **Showplan XML Statistics Profile** 事件檔案的副檔名為 .SQLPlan。  
  
## 另請參閱  
 [在 SQL Server Profiler 中使用 SHOWPLAN 結果分析查詢](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
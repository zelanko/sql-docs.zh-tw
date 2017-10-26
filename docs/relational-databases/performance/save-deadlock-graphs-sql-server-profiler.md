---
title: "儲存死結圖形 (SQL Server Profiler) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deadlocks [SQL Server], saving deadlock graphs
- graphs [SQL Server]
- saving deadlock graphs
ms.assetid: bf1fc906-abd6-4a89-842e-da0d66b2defe
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c89c0ed24b52d89c36fb1f1cce29717988a0d798
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="save-deadlock-graphs-sql-server-profiler"></a>儲存死結圖形 (SQL Server Profiler)
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]儲存死結圖表。 死結圖表會儲存為 XML 檔。  
  
### <a name="to-save-deadlock-graph-events-separately"></a>若要個別儲存死結圖表事件  
  
1.  在 **[檔案]** 功能表上按一下 **[新增追蹤]**，然後連接到 SQL Server 的執行個體。  
  
     會出現 [追蹤屬性] **[追蹤屬性]**對話方塊。  
  
    > [!NOTE]  
    >  如果選取 [進行連接後立即啟動追蹤]，將不會顯示 [追蹤屬性] 對話方塊，而是開始追蹤。 在 [工具] 功能表上，按一下 [選項]，並清除 [進行連接後立即啟動追蹤] 核取方塊，以關閉這項設定。  
  
2.  在 [追蹤屬性] 對話方塊的 [追蹤名稱] 方塊中，輸入追蹤的名稱。  
  
3.  在 **[使用範本]** 清單中，選取追蹤使用為基礎的追蹤範本；若不想要使用範本，請選取 **[空白]** 。  
  
4.  執行下列其中之一：  
  
    -   選取 [儲存至檔案] 核取方塊，將追蹤擷取至檔案。 在 **[設定最大檔案大小]**中指定一個值。  
  
         (選擇性) 選取 [啟用檔案換用] 及 [伺服器處理追蹤資料]。  
  
    -   選取 [儲存至資料表] 核取方塊，將追蹤擷取至資料庫資料表。  
  
         (選擇性) 按一下 **[設定最大資料列數]**，然後指定一個值。  
  
5.  (選擇性) 選取 **[啟用追蹤停止時間]** 核取方塊，然後指定停止日期和時間。  
  
6.  按一下 [事件選取範圍] 索引標籤。  
  
7.  在 [事件] 資料行中，展開 [Locks] 事件類別目錄，然後選取 [Deadlock Graph] 核取方塊。 如果看不到 Locks 事件類別目錄，請核取 [顯示所有事件] 來顯示它。  
  
     [事件擷取設定] 索引標籤會加入 [追蹤屬性] 對話方塊。  
  
8.  在 [事件擷取設定] 索引標籤上，按一下 [個別儲存死結 XML 事件]。  
  
9. 在 [另存新檔] 對話方塊中，輸入要儲存 Deadlock Graph 事件的檔案名稱。  
  
10. 按一下 [所有死結 XML 批次都在單一檔案中]，將所有 Deadlock Graph 事件儲存在單一 XML 檔案中，或按一下 [每一個死結 XML 批次都在相異檔案中]，為每一個 Deadlock Graph 建立新的 XML 檔案。  
  
 在儲存了死結檔案之後，您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中開啟檔案。 如需詳細資訊，請參閱[開啟、檢視及列印死結檔案 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/open-view-and-print-a-deadlock-file-sql-server-management-studio.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Profiler 分析死結](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)  
  
  


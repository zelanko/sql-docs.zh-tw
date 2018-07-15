---
title: 相互關聯追蹤與 Windows 效能記錄資料 (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], logs
ms.assetid: e1b3072c-8daf-49a7-9895-c8cccd2adb95
caps.latest.revision: 31
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d5517f2962bef05e560697c55348a5372a80aa62
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37245348"
---
# <a name="correlate-a-trace-with-windows-performance-log-data-sql-server-profiler"></a>使追蹤與 Windows 效能記錄資料產生相互關聯 (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 可以將 Microsoft Windows 系統監視器計數器與相互關聯[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]或是[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]事件。 Windows 系統監視器可將指定計數器的系統活動記錄在效能記錄中。  
  
> [!NOTE]  
>  如需有關在不同 Windows 版本之間共用記錄的詳細資訊，請參閱本主題結尾處的程序。  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>使追蹤與效能記錄資料產生相互關聯  
  
1.  在 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]中，開啟儲存的追蹤檔案或追蹤資料表。 您無法與仍在收集事件資料的執行中追蹤產生相互關聯。 為了與系統監視器資料保持正確的相互關聯，追蹤必須同時包含 [StartTime] 與 [EndTime] 資料行。  
  
2.  在[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]**檔案**功能表上，按一下 **匯入效能資料**。  
  
3.  在 [開啟] 對話方塊中，選取含有效能記錄的檔案。 擷取效能記錄資料的期間必須與擷取追蹤資料的期間相同。  
  
4.  在 [效能計數器限制] 對話方塊中，針對要顯示在追蹤旁的系統監視器物件與計數器，選取其對應的核取方塊。 按一下 **[確定].**  
  
5.  選取追蹤事件視窗中的事件，或使用方向鍵來瀏覽追蹤事件視窗中相鄰的幾個資料列。 [系統監視器資料] 視窗中的紅色直條，代表已與所選追蹤事件產生相互關聯的效能記錄資料。  
  
6.  在系統監視器圖表中，按一下您所需的時間點。 系統會選取時間最接近的對應追蹤資料列。 若要放大時間範圍，請按住滑鼠指標並在系統監視器圖表中加以拖曳。  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>若要建立可在不同的 Windows 版本間共用的效能記錄  
  
1.  在 [控制台] 中，開啟 [系統管理工具]，然後按兩下 [效能]。  
  
2.  在 [效能] 對話方塊中，展開 [效能記錄檔及警示]，以滑鼠右鍵按一下 [計數器記錄檔]，然後按一下 [新記錄檔設定]。  
  
3.  輸入計數器記錄檔的名稱，再按一下 [確定]。  
  
4.  在 [一般] 索引標籤上，按一下 [新增計數器]。  
  
5.  在 [效能物件] 清單中，選取您要監視的效能物件。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 預設執行個體的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 效能物件名稱會以 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 作為開頭，而具名執行個體則會以 MSSQL$*instanceName* 作為開頭。  
  
6.  盡可能為您的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體加入所需的計數器以及其他重要的值，如處理器時間與磁碟時間。  
  
7.  完成新增計數器後，請按一下 [關閉]。  
  
8.  設定 [Sample data every (依下列週期進行資料取樣)] 的間隔值。 一開始請使用適度的抽樣間隔，例如 5 分鐘，然後再視需要調整間隔。  
  
9. 在 [記錄檔] 索引標籤上，從 [記錄檔案類型] 清單中選擇 [TextFile (Comma delimited) (文字檔案 (以逗號分隔))]。 以逗號分隔的文字記錄檔可在不同的 Windows 版本間共用，並且稍後可在諸如 Microsoft Excel 的報告工具中加以檢視。  
  
10. 在 [排程] 索引標籤上，指定監視排程。  
  
11. 按一下 [確定] 建立效能記錄。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler 範本和權限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [啟動 SQL Server Profiler](../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  

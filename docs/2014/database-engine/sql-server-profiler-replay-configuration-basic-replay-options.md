---
title: SQL Server Profiler-重新執行組態 （基本重新執行選項） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: 85a1dec6-9bbc-477a-86c5-b463db9ebb31
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ea9517047321f54734b3ccd8d072ba8f3f23152
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089723"
---
# <a name="sql-server-profiler---replay-configuration-basic-replay-options"></a>SQL Server Profiler - 重新執行組態 (基本重新執行選項)
  在 **[重新執行組態]** 對話方塊中，使用 **[基本重新執行選項]** 頁面來指定如何重新執行追蹤檔案或資料表。  
  
 若要檢視這個視窗，請使用 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 開啟包含用以重新執行的適當事件之追蹤檔案或資料表。 如需詳細資訊，請參閱 [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md)。 在追蹤檔案或資料表開啟期間，請在 **[重新執行]** 功能表上按一下 **[啟動]** ，然後連接到想要重新執行追蹤的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體。  
  
## <a name="options"></a>選項  
 **重新執行伺服器**  
 顯示要連接以重新執行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體。  
  
 **變更...**  
 啟動 [連接到伺服器]  對話方塊，以連接到另一部伺服器。  
  
 **儲存至檔案**  
 將重新執行結果儲存至檔案。 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 會顯示標準檔案對話方塊，您可以在此指定檔案的儲存位置。  
  
 **儲存至資料表**  
 將重新執行結果儲存至資料表。 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 會顯示資料表選取項目對話方塊，您可以在此指定資料表的儲存位置。  
  
 **重新執行執行緒的數目**  
 指定要同時使用的重新執行執行緒的數目。 較高的數目會在重新執行期間消耗較多資源，但是重新執行速度較快而且更並行。  
  
 **依照追蹤的順序重新執行事件**  
 循序重新執行事件。 如果您正在重新執行追蹤以偵錯，請使用此選項。  
  
 **使用多執行緒重新執行事件**  
 並行重新執行事件。 此選項比循序重新執行事件還快，但是會停用偵錯。 事件會依其系統處理序識別碼 (SPID) 來排序。  
  
 **顯示重新執行結果**  
 在 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]中顯示重新執行結果。  
  
## <a name="see-also"></a>另請參閱  
 [重新執行追蹤資料表 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [重新執行追蹤檔案 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [重新執行追蹤](../tools/sql-server-profiler/replay-traces.md)  
  
  

---
title: 根據事件結束時間篩選事件 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- event end times [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: 74628f9e-2d39-496a-a443-0a3887db223d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1e6f27e50121261baa17409f67c5d70bde0f1cba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930010"
---
# <a name="filter-events-based-on-the-event-end-time-sql-server-profiler"></a>根據事件結束時間篩選事件 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]根據事件結束時間篩選追蹤事件。  
  
### <a name="to-filter-events-based-on-the-event-end-time"></a>若要根據事件結束時間篩選事件  
  
1.  在 [檔案]  功能表上，按一下 [新增追蹤]  ，接著連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
     會出現 [追蹤屬性] **[追蹤屬性]** 對話方塊。  
  
    > [!NOTE]  
    >  如果選取 [進行連接後立即啟動追蹤]  ，將不會顯示 [追蹤屬性]  對話方塊，而是開始追蹤。 於 [工具]  功能表，按一下 [選項]  ，並清除 [連接後立即啟動追蹤]  核取方塊，以關閉這項設定。  
  
2.  在 [追蹤屬性]  對話方塊中，請確定已選取 [一般]  索引標籤，並在 [追蹤名稱]  文字方塊中輸入名稱。  
  
3.  在 [使用範本]  清單中，選取追蹤範本。  
  
4.  選擇性，指定要儲存追蹤結果的目的地檔案或資料表。  
  
5.  在 [事件選取範圍]  索引標籤上，按一下 [結束時間]  資料行，以啟動 [編輯篩選]  對話方塊。 您也可以用滑鼠右鍵按一下資料行標題，然後選取 [編輯資料行篩選]  。  
  
6.  展開 [大於]  或 [小於]  ，然後在比較運算子下方的欄位中輸入 **datetime**值。  
  
## <a name="see-also"></a>另請參閱  
 [[SQL Server Profiler]](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

---
title: "重新執行至中斷點 (SQL Server Profiler) |Microsoft 文件"
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
- breakpoints [SQL Server]
- traces [SQL Server], replaying
ms.assetid: 3caf751e-df3b-40c7-b5e8-4490ae178e0c
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 795eaf0f1e2ac0079dd6387d6b15395d4a26704e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="replay-to-a-breakpoint-sql-server-profiler"></a>重新執行至中斷點 (SQL Server Profiler)
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，在您要重新執行的追蹤檔案或資料表中設定中斷點。 開始重新執行追蹤之前，在追蹤檔案或資料表中設定中斷點，可以讓您在特定事件上暫停重新執行追蹤。 在重新執行追蹤時使用中斷點可以支援偵錯，因為您可以將很長的追蹤指令碼的重新執行過程，分解為可累加分析的短片段。  
  
### <a name="to-replay-to-a-breakpoint"></a>若要重新執行至中斷點  
  
1.  開啟您要重新執行的追蹤檔案或追蹤資料表。 如需詳細資訊，請參閱[開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或[開啟追蹤資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)。  
  
     確定您開啟的追蹤檔案或資料表包含重新執行所需的事件類別。 如需詳細資訊，請參閱 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
2.  在追蹤視窗中，按一下您要做為中斷點的事件。 使用下列三種方式之一來設定中斷點：  
  
    -   按 F9 鍵。  
  
    -   在 **[重新執行]** 功能表上，按一下 **[切換中斷點]**。  
  
    -   以滑鼠右鍵按一下事件，然後按一下 [切換中斷點]。  
  
     選取的追蹤事件旁邊會出現紅色項目符號，表示此為追蹤中斷點。  
  
     重複這個步驟來設定多個中斷點。  
  
3.  在 **[重新執行]** 功能表，按一下 **[開始]**，連接到您要重新執行追蹤的伺服器。  
  
4.  在 **[重新執行組態]** 對話方塊中確認設定，然後按一下 **[確定]**。  
  
     開始重新執行，到達中斷點時會暫停。  
  
5.  按 F5 繼續重新執行，繼續到下一個中斷點。  
  
6.  重複步驟 5 至追蹤結束。  
  
## <a name="see-also"></a>另請參閱  
 [重新執行至資料指標 &#40;SQL Server Profiler &#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)   
 [重新執行追蹤](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

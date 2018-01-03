---
title: "重新執行至中斷點 (SQL Server Profiler) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- breakpoints [SQL Server]
- traces [SQL Server], replaying
ms.assetid: 3caf751e-df3b-40c7-b5e8-4490ae178e0c
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2feefa23b61938103d68f848df28b76436a87892
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="replay-to-a-breakpoint-sql-server-profiler"></a>重新執行至中斷點 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]本主題描述如何設定追蹤檔案或您想要重新執行所使用的資料表中的中斷點[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。 開始重新執行追蹤之前，在追蹤檔案或資料表中設定中斷點，可以讓您在特定事件上暫停重新執行追蹤。 在重新執行追蹤時使用中斷點可以支援偵錯，因為您可以將很長的追蹤指令碼的重新執行過程，分解為可累加分析的短片段。  
  
### <a name="to-replay-to-a-breakpoint"></a>若要重新執行至中斷點  
  
1.  開啟您要重新執行的追蹤檔案或追蹤資料表。 如需詳細資訊，請參閱 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)隨附的預先定義「微調」範本。  
  
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
  
## <a name="see-also"></a>請參閱  
 [重新執行至資料指標處 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)   
 [重新執行追蹤](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

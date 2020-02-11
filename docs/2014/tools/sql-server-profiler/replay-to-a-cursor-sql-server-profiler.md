---
title: 重新執行至資料指標（SQL Server Profiler） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7c4c4b9d2e2e07c53f850fe545d803fa411dbbc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63267493"
---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>重新執行至資料指標處 (SQL Server Profiler)
  此主題描述如何利用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，來重新執行已在到達資料指標時暫停的追蹤檔或資料表。 在資料指標暫停追蹤可以支援偵錯，因為您可以將較長追蹤指令碼的重新執行過程分解為可累加分析的較短片段。  
  
### <a name="to-replay-to-the-cursor"></a>若要重新執行至資料指標處  
  
1.  開啟您要重新執行的追蹤檔案或追蹤資料表。 如需詳細資訊，請參閱 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) 或 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)隨附的預先定義「微調」範本。  
  
     確定您開啟的追蹤檔案或資料表包含重新執行所需的事件類別。 如需詳細資訊，請參閱 [Replay Requirements](replay-requirements.md)。  
  
2.  在追蹤視窗中按一下事件。  
  
3.  在 [重新執行]  功能表上，按一下 [執行至資料指標處]  ，然後連接您要重新執行追蹤的伺服器。  
  
4.  在 **[重新執行組態]** 對話方塊中確認設定，然後按一下 **[確定]** 。  
  
     開始重新執行，並在到達第一個資料指標時暫停。  
  
5.  按 F5 可繼續追蹤。  
  
6.  重複步驟 5 至追蹤結束。  
  
## <a name="see-also"></a>另請參閱  
 [重新執行至中斷點 &#40;SQL Server Profiler&#41;](replay-to-a-breakpoint-sql-server-profiler.md)   
 [重新執行追蹤](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  

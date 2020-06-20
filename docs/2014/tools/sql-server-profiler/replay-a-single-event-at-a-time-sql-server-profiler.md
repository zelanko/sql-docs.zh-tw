---
title: 一次重新執行一個事件 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], replaying single event at a time
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
author: stevestein
ms.author: sstein
ms.openlocfilehash: 457bc94d9d8eae470fb60b450d30441c07e676df
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040227"
---
# <a name="replay-a-single-event-at-a-time-sql-server-profiler"></a>一次重新執行一個事件 (SQL Server Profiler)
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，在重新執行追蹤檔案或資料表中，一次重新執行一個事件。  
  
### <a name="to-replay-a-single-event-at-a-time"></a>若要一次只重新執行一個事件  
  
1.  開啟您要重新執行的追蹤檔案或追蹤資料表。 如需詳細資訊，請參閱 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) 或 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)隨附的預先定義「微調」範本。  
  
     確定您開啟的追蹤檔案或資料表包含重新執行所需的事件類別。 如需詳細資訊，請參閱 [Replay Requirements](replay-requirements.md)。  
  
2.  在 **[重新執行]** 功能表上，按一下 **[步驟]** ，然後連接到要重新執行追蹤的伺服器執行個體。  
  
3.  在 **[重新執行組態]** 對話方塊中確認設定，然後按一下 **[確定]** 。 如需在 [重新執行組態]  對話方塊中指定設定的詳細資訊，請參閱[重新執行追蹤檔案 &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md) 或[重新執行追蹤資料表 &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md)。  
  
4.  若要重新執行第一個事件，請在 **[重新執行組態]** 對話方塊上，按一下 **[確定]** 。  
  
5.  若要重新執行後續事件，請在 **[重新執行]** 功能表上，按一下 **[步驟]** 或按 F10。 每個事件都重複按一下 **[步驟]** 或按 F10。  
  
## <a name="see-also"></a>另請參閱  
 [重新執行追蹤](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  

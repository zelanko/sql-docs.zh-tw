---
title: 一次重新執行一個事件 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], replaying single event at a time
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c82ba2cfcfbefed2569c1f0e9fed9ff5637bc908
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993010"
---
# <a name="replay-a-single-event-at-a-time-sql-server-profiler"></a>一次重新執行一個事件 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，在重新執行追蹤檔案或資料表中，一次重新執行一個事件。  
  
### <a name="to-replay-a-single-event-at-a-time"></a>若要一次只重新執行一個事件  
  
1.  開啟您要重新執行的追蹤檔案或追蹤資料表。 如需詳細資訊，請參閱 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)隨附的預先定義「微調」範本。  
  
     確定您開啟的追蹤檔案或資料表包含重新執行所需的事件類別。 如需詳細資訊，請參閱 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
2.  在 **[重新執行]** 功能表上，按一下 **[步驟]**，然後連接到要重新執行追蹤的伺服器執行個體。  
  
3.  在 **[重新執行組態]** 對話方塊中確認設定，然後按一下 **[確定]**。 如需在 [重新執行組態] 對話方塊中指定設定的詳細資訊，請參閱[重新執行追蹤檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md) 或[重新執行追蹤資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)。  
  
4.  若要重新執行第一個事件，請在 **[重新執行組態]** 對話方塊上，按一下 **[確定]** 。  
  
5.  若要重新執行後續事件，請在 **[重新執行]** 功能表上，按一下 **[步驟]** 或按 F10。 每個事件都重複按一下 **[步驟]** 或按 F10。  
  
## <a name="see-also"></a>另請參閱  
 [重新執行追蹤](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

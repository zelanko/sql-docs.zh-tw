---
title: 重新執行 Transact-SQL 指令碼 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b85c31fcaad26d6cc8604764e37d8aa32d58610
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62712346"
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>重新執行 Transact-SQL 指令碼 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  當測試效能問題的可能方案時，請使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來重新執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼，並比較變更前後的效能。  
  
### <a name="to-replay-a-transact-sql-script"></a>若要重新執行 Transact-SQL 指令碼  
  
1.  在 [檔案]  功能表上，指向 [開啟]  ，然後按一下 [指令碼檔案]  。  
  
2.  選取您要開啟的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案。 確定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼包含重新執行所需的事件。 如需詳細資訊，請參閱 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
3.  在 [重新執行]  功能表上，按一下 [啟動]  ，然後連接到您要重新執行指令碼的伺服器。  
  
4.  在 **[重新執行組態]** 對話方塊中確認設定，然後按一下 **[確定]** 。  
  
## <a name="see-also"></a>另請參閱  
 [重新執行追蹤](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

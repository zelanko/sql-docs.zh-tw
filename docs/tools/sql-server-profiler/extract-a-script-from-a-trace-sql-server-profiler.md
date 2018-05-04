---
title: 從追蹤中擷取指令碼 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], traces
- extracting script from trace [SQL Server]
ms.assetid: 431126a6-ff91-4818-8763-4442152bd571
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1a6b1c13fce71dc29f332e1b85abfca0378f6f2b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="extract-a-script-from-a-trace-sql-server-profiler"></a>從追蹤中擷取指令碼 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何從追蹤檔案或資料表中擷取 [!INCLUDE[tsql](../../includes/tsql-md.md)] 事件，並利用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 將它們儲存為 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]指令碼檔案。  
  
### <a name="to-extract-a-transact-sql-script-from-a-trace-file-or-table"></a>若要從追蹤檔案或資料表中擷取 Transact-SQL 指令碼  
  
1.  開啟包含您要儲存到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 事件的追蹤檔案或資料表。 如需詳細資訊，請參閱 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)隨附的預先定義「微調」範本。  
  
2.  在 [檔案] 功能表上，依序指向 [匯出] 和 [擷取 SQL Server 事件]，然後按一下 [擷取 Transact-SQL 事件]。  
  
3.  在 **[另存新檔]** 對話方塊中，輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 檔案的名稱，然後按一下 **[儲存]**。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

---
title: "建立 TRANSACT-SQL 指令碼以執行追蹤 (SQL Server Profiler) |Microsoft 文件"
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
- traces [SQL Server], running
- scripts [SQL Server], traces
ms.assetid: 6b0e2519-998d-40d5-b8ba-5e6a773f91a6
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4cd2934ea52aa38d7f8e558ecf93d2b92e349a6b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="create-a-transact-sql-script-for-running-a-trace-sql-server-profiler"></a>建立 Transact-SQL 指令碼以執行追蹤 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]本主題描述如何從現有的追蹤檔案或資料表建立 TRANSACT-SQL 指令碼，使用[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。  
  
### <a name="to-create-a-transact-sql-script-to-run-a-trace"></a>若要建立 Transact-SQL 指令碼以執行追蹤  
  
1.  開啟追蹤檔或資料表。 如需詳細資訊，請參閱 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)隨附的預先定義「微調」範本。  
  
2.  在 [檔案] 功能表上，依序指向 [匯出] 和 [指令碼追蹤定義]，然後按一下對應至您想要追蹤之伺服器的版本。  
  
3.  在 [另存新檔] 對話方塊中，輸入指令碼檔案的名稱，然後按一下 [儲存]。  
  
## <a name="see-also"></a>請參閱  
 [SQL Server Profiler 範本和權限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

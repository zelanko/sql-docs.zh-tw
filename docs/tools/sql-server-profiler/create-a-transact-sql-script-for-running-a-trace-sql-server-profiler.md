---
title: 建立 Transact-SQL 指令碼以執行追蹤 (SQL Server Profiler) | Microsoft Docs
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
- traces [SQL Server], running
- scripts [SQL Server], traces
ms.assetid: 6b0e2519-998d-40d5-b8ba-5e6a773f91a6
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b2612d34dcd7796721ec4822cee42db7829a3220
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38048300"
---
# <a name="create-a-transact-sql-script-for-running-a-trace-sql-server-profiler"></a>建立 Transact-SQL 指令碼以執行追蹤 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，從現有的追蹤檔或資料表建立 Transact-SQL 指令碼。  
  
### <a name="to-create-a-transact-sql-script-to-run-a-trace"></a>若要建立 Transact-SQL 指令碼以執行追蹤  
  
1.  開啟追蹤檔或資料表。 如需詳細資訊，請參閱 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)隨附的預先定義「微調」範本。  
  
2.  在 [檔案] 功能表上，依序指向 [匯出] 和 [指令碼追蹤定義]，然後按一下對應至您想要追蹤之伺服器的版本。  
  
3.  在 [另存新檔] 對話方塊中，輸入指令碼檔案的名稱，然後按一下 [儲存]。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler 範本和權限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

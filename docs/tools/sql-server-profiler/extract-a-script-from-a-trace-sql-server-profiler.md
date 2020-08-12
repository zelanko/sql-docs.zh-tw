---
title: 從追蹤擷取指令碼
titleSuffix: SQL Server Profiler
description: 了解如何在 SQL Server Profiler 中，從追蹤檔案或資料表擷取 Transact-SQL 事件，並將其儲存為 Transact-SQL 指令檔。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 431126a6-ff91-4818-8763-4442152bd571
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 2495eb7c020e6fb64fb894d4d6bb7614707f84bc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774861"
---
# <a name="extract-a-script-from-a-trace-sql-server-profiler"></a>從追蹤中擷取指令碼 (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

此主題描述如何從追蹤檔案或資料表中擷取 [!INCLUDE[tsql](../../includes/tsql-md.md)] 事件，並利用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 將它們儲存為 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]指令碼檔案。  
  
### <a name="to-extract-a-transact-sql-script-from-a-trace-file-or-table"></a>若要從追蹤檔案或資料表中擷取 Transact-SQL 指令碼  
  
1.  開啟包含您要儲存到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 事件的追蹤檔案或資料表。 如需詳細資訊，請參閱 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 或 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)隨附的預先定義「微調」範本。  
  
2.  在 [檔案] 功能表上，依序指向 [匯出] 和 [擷取 SQL Server 事件]，然後按一下 [擷取 Transact-SQL 事件]。  
  
3.  在 **[另存新檔]** 對話方塊中，輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 檔案的名稱，然後按一下 **[儲存]** 。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

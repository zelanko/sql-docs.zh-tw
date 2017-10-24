---
title: "將追蹤結果儲存至資料表 (SQL Server Profiler) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 41505214d2ae9e53cc9cd45433183d3250650313
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>將追蹤結果儲存到資料表 (SQL Server Profiler)
  此主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 將追蹤結果儲存到資料庫資料表。  
  
### <a name="to-save-trace-results-to-a-table"></a>若要將追蹤結果儲存至資料表  
  
1.  在 [檔案] 功能表上，按一下 [新增追蹤]，接著連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
     會出現 [追蹤屬性] **[追蹤屬性]**對話方塊。  
  
    > [!NOTE]  
    >  如果選取 [進行連接後立即啟動追蹤]，將不會顯示 [追蹤屬性] 對話方塊，而是開始追蹤。 在 [工具] 功能表，按一下 [選項]，並清除 [進行連接後立即啟動追蹤] 核取方塊，以關閉這項設定。  
  
2.  在 [追蹤名稱] 方塊中，輸入追蹤的名稱，然後按一下 [儲存至資料表]。  
  
3.  在 [連接至伺服器] 對話方塊中，連接至將包含追蹤資料表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
4.  在 [目的地資料表] 對話方塊中，從 [資料庫] 清單中選取資料庫。  
  
5.  在 [擁有者] 清單中，選取追蹤的擁有者。  
  
6.  在 [資料表] 清單中，輸入或選取追蹤結果的資料表名稱。 按一下 **[確定].**  
  
7.  在 [追蹤屬性] 對話方塊中，選取 [設定最大資料列數 (單位：千)] 核取方塊，以指定要儲存的最大資料列數。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  


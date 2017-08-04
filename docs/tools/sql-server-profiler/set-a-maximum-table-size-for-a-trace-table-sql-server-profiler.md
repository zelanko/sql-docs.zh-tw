---
title: "設定追蹤資料表 (SQL Server Profiler) 的資料表大小上限 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- size [SQL Server], trace tables
- maximum table size for traces
ms.assetid: d0ae83e5-1c88-4a2e-be05-2c341280b978
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 733cbc9e74e9e9e56c7bcb918f8c695dd1304a7e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="set-a-maximum-table-size-for-a-trace-table-sql-server-profiler"></a>設定追蹤資料表的資料表大小上限 (SQL Server Profiler)
  本主題說明如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來設定追蹤資料表的資料表大小上限。  
  
### <a name="to-set-a-maximum-table-size-for-a-trace-table"></a>若要設定追蹤資料表的大小上限  
  
1.  在 **[檔案]** 功能表上按一下 **[新增追蹤]**，然後連接到 SQL Server 的執行個體。  
  
     會出現 [追蹤屬性] **[追蹤屬性]**對話方塊。  
  
    > [!NOTE]  
    >  如果選取 [進行連接後立即啟動追蹤]，將不會顯示 [追蹤屬性] 對話方塊，而是開始追蹤。 在 [工具] 功能表上，按一下 [選項]，並清除 [進行連接後立即啟動追蹤] 核取方塊，以關閉這項設定。  
  
2.  在 **[追蹤名稱]** 方塊中，輸入追蹤的名稱。  
  
3.  在 [範本名稱] 清單中，選取追蹤範本。  
  
4.  選取 [儲存至資料表] 核取方塊。  
  
5.  連接到您要儲存追蹤的伺服器。  
  
     畫面上出現 [目的地資料表] 對話方塊。  
  
6.  從 [資料庫] 清單中選取追蹤的資料庫。  
  
7.  在 [資料表] 方塊中，輸入或選取資料表名稱。  
  
8.  選取 [設定最大資料列數] 核取方塊，並指定追蹤資料表的最大資料列數。  
  
    > [!NOTE]  
    >  當資料表的資料列數超過您所指定的最大值時，就不會再記錄追蹤事件。 不過，仍會繼續追蹤。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  

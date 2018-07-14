---
title: 啟動 SQL Server Profiler |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f5b752dfc31fd83530a773370551b88589fc2f4b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246138"
---
# <a name="start-sql-server-profiler"></a>啟動 SQL Server Profiler
  您可以利用多種不同的方式來啟動 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，以支援在各種狀況中收集追蹤輸出。 啟動 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的方式包括：從 **[開始]** 功能表、從 **Tuning Advisor 中的** [工具] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 功能表，以及從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的數個位置。  
  
 當您第一次啟動 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，且從 **[檔案]** 功能表中選取 **[新增追蹤]** 時，應用程式會顯示一個 **[連接到伺服器]** 對話方塊，供您指定要連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
### <a name="to-start-sql-server-profiler-from-the-start-menu"></a>從 [開始] 功能表啟動 SQL Server Profiler  
  
1.  在 **[開始]** 功能表中，依序指向 **[所有程式]**、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[效能工具]**，然後按一下 **[SQL Server Profiler]**。  
  
### <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>在 Database Engine Tuning Advisor 中啟動 SQL Server Profiler  
  
1.  在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 的 **[工具]** 功能表上，按一下 **[SQL Server Profiler]**。  
  
## <a name="starting-sql-server-profiler-in-management-studio"></a>在 Management Studio 中啟動 SQL Server Profiler  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會在自己的執行個體中啟動每個分析工具工作階段，並在關閉 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]後繼續執行。  
  
 您可以從 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 中的數個位置啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，如下列程序所示。 當 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 啟動時，它會載入連接內容、追蹤範本及其啟動點的篩選內容。  
  
#### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>從工具功能表啟動 SQL Server Profiler  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Tuning Advisor 中的** 功能表上，按一下 **[SQL Server Profiler]**。  
  
#### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>從查詢編輯器啟動 SQL Server Profiler  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 功能表列上，按一下 **[新增查詢]**。  
  
2.  在查詢編輯器中按一下滑鼠右鍵，然後選取 [在 SQL Server Profiler 中追蹤查詢]。  
  
    > [!NOTE]  
    >  連接內容是編輯器連接、追蹤範本為 TSQL_SPs，而套用的篩選為 SPID = 查詢視窗 SPID。  
  
#### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>若要從活動監視器啟動 SQL Server Profiler  
  
1.  在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，然後按一下 [活動監視器]。  
  
2.  按一下 [處理序] 窗格，以滑鼠右鍵按一下您要分析的處理序，然後按一下 [在 SQL Server Profiler 中追蹤處理序]。  
  
    > [!NOTE]  
    >  選取處理序時，如果有開啟 [活動監視器]，則連接內容為 [物件總管] 連接。 追蹤範本是以伺服器類型為基礎的預設值，而且 SPID 等於所選處理序的 SPID。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 在 Windows 驗證模式中，執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的使用者帳戶必須有連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的權限。  
  
 若要利用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]來執行追蹤，使用者也必須有 ALTER TRACE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](sql-server-profiler.md)   
 [使用 SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)  
  
  

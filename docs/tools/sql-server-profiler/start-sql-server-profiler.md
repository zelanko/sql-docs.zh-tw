---
title: 執行 SQL Server Profiler |Microsoft Docs
ms.custom: ''
ms.date: 7/7/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
- Profiler [SQL Server Profiler], running
- SQL Server Profiler, running
- running SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 303f97e5a2fb4599bde5c17fee056a3572491ad0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51655970"
---
# <a name="run-sql-server-profiler"></a>執行 SQL Server Profiler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以使用多種不同的方式來執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，以支援在各種狀況中收集追蹤輸出。 您可以從 Windows 10 的 [開始] 功能表、[!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 的 [工具] 功能表，以及 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的數個位置啟動 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。  
  
當您第一次啟動 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，且從 [檔案] 功能表中選取 [新增追蹤] 時，應用程式會顯示一個 [連線到伺服器] 對話方塊，您可在此指定要連線的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>從 Windows 10 的 [開始] 功能表啟動 SQL Server Profiler  
-  按一下 Windows**啟動**圖示或按下 Windows 鍵，並開始輸入 「 SQL Server Profiler 17 」。 當**SQL Server Profiler 17**  圖格出現時，按一下它。   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>在 Database Engine Tuning Advisor 中啟動 SQL Server Profiler  
-  在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 的 **[工具]** 功能表上，按一下 **[SQL Server Profiler]**。  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>若要啟動 SQL Server Management Studio 中的 SQL Server Profiler  
 您可以啟動[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]中的數個位置[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 當 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 啟動時，它會載入連線內容、追蹤範本及其啟動點的篩選內容。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 開始在自己的執行個體中的每個 SQL Server Profiler 工作階段和 Profiler 會繼續執行，如果您關閉[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>從工具功能表啟動 SQL Server Profiler  
-  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Tuning Advisor 中的** 功能表上，按一下 **[SQL Server Profiler]**。  

### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>從查詢編輯器啟動 SQL Server Profiler  
- 在查詢編輯器中按一下滑鼠右鍵，然後選取 [在 SQL Server Profiler 中追蹤查詢]。  

  > [!NOTE]  
  >  連接內容是編輯器連接、追蹤範本為 TSQL_SPs，而套用的篩選為 SPID = 查詢視窗 SPID。  
    
### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>若要從活動監視器啟動 SQL Server Profiler  
- 在活動監視器中按一下 [處理序] 窗格，以滑鼠右鍵按一下您要分析的處理序，然後按一下 [在 SQL Server Profiler 中追蹤處理序]。  

    > [!NOTE]  
    >  選取處理序時，如果有開啟 [活動監視器]，則連接內容為 [物件總管] 連接。 追蹤範本是以伺服器類型為基礎的預設值，而且 SPID 等於所選處理序的 SPID。  
    
## <a name="net-framework-security"></a>.NET Framework 安全性  
- 在 Windows 驗證模式中，執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的使用者帳戶必須有連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的權限。  
- 若要利用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]來執行追蹤，使用者也必須有 ALTER TRACE 權限。  

## <a name="next-steps"></a>後續步驟  
 [SQL Server Profiler 概觀](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [使用 SQL Server Management Studio](https://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  

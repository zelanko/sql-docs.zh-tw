---
title: "將追蹤結果儲存至檔案 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-trace
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6555bf45840676342a9df3b37fee8830bfed246f
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/19/2018
---
# <a name="save-trace-results-to-a-file"></a>將追蹤結果儲存至檔案
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以將追蹤結果儲存至檔案。 追蹤檔案是用來寫入追蹤結果的檔案。 追蹤檔案可以位於本機目錄 (例如 C:\\\\檔案名稱.trc) 或網路目錄 (例如 \\\電腦名稱\共用名稱\檔案名稱.trc)。  
  
 您可以使用追蹤檔案來執行下列動作：  
  
-   重新執行追蹤  
  
-   稽核 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   進行效能分析  
  
-   使追蹤事件與效能計數器相互關聯，以加強問題偵測  
  
-   執行 Database Engine Tuning Advisor 分析  
  
-   完成查詢最佳化。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當您指定預存程序 **@tracefile** 中 **@tracefile**引數的路徑與檔案名稱時，會將追蹤結果儲存到檔案。  
  
> [!NOTE]  
>  若要將路徑指定到 **sp_trace_create** 預存程序以儲存追蹤檔案，則其必須是伺服器可存取的目錄。 另請注意，若要在 **sp_trace_create**指定本機目錄，此目錄必須是伺服器電腦上的本機目錄。  
  
 如果使用了 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，您就可以將追蹤結果儲存到檔案或資料表。 將追蹤結果儲存到資料表與將追蹤儲存到檔案一樣，都允許稍後進行存取，但是儲存到資料表還有一項優點，就是可以透過查詢資料表來搜尋特定事件。  
  
 如需儲存追蹤結果的詳細資訊，請參閱[將追蹤結果儲存到資料表 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) 和[將追蹤結果儲存至檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [建立追蹤 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [建立追蹤 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  

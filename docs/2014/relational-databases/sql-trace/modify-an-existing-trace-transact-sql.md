---
title: 修改現有的追蹤 (Transact-SQL) | Microsoft Docs
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
- traces [SQL Server], modifying
- modifying traces
ms.assetid: 8792b43f-2510-44e3-9239-e73ad8227b89
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68d98a838fb17360997d7eb4a1db025176e322aa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37168275"
---
# <a name="modify-an-existing-trace-transact-sql"></a>修改現有的追蹤 (Transact-SQL)
  此主題描述如何使用預存程序來修改現有的追蹤。  
  
### <a name="to-modify-an-existing-trace"></a>若要修改現有的追蹤  
  
1.  如果追蹤已在執行，請執行 **sp_trace_setstatus** 並指定 **@status = 0**，以停止追蹤。  
  
2.  若要修改追蹤事件，請執行 **sp_trace_setevent** 並利用參數指定要做的變更。 這些參數依序排列如下：  
  
    -   **@traceid** (追蹤識別碼)  
  
    -   **@eventid** (事件識別碼)  
  
    -   **@columnid** (資料行識別碼)  
  
    -   **@on** (ON)  
  
     在修改 **@on** 參數時，請記住此參數與 **@columnid** 參數的互動：  
  
    |ON|資料行識別碼|結果|  
    |--------|---------------|------------|  
    |ON (**1**)|NULL|會開啟事件。 會清除所有資料行。|  
    ||NOT NULL|資料行會針對特定的事件開啟。|  
    |OFF (**0**)|NULL|會關閉事件。 會清除所有資料行。|  
    ||NOT NULL|會針對特定的事件關閉資料行。|  
  
> [!IMPORTANT]  
>  不同於一般預存程序，所有 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 預存程序的參數 (**sp_trace_* xx***) 都有強制類型，而且不支援資料類型的自動轉換。 如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [系統預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler 預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  

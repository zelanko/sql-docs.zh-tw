---
title: 修改現有的追蹤 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], modifying
- modifying traces
ms.assetid: 8792b43f-2510-44e3-9239-e73ad8227b89
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9f302d5fec4c9089d764a99e1bb4798be82d8742
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079998"
---
# <a name="modify-an-existing-trace-transact-sql"></a>修改現有的追蹤 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用預存程序來修改現有的追蹤。  
  
### <a name="to-modify-an-existing-trace"></a>若要修改現有的追蹤  
  
1.  如果追蹤已在執行，請執行 **sp_trace_setstatus** 並指定 **@status = 0**，以停止追蹤。  
  
2.  若要修改追蹤事件，請執行 **sp_trace_setevent** 並利用參數指定要做的變更。 這些參數依序排列如下：  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

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
>  與一般的預存程序不同，所有 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 預存程序 (<strong>sp_trace_*xx*</strong>) 的參數均嚴格區分類型，且不支援自動資料類型的轉換。 如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [SQL Server Profiler 預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
